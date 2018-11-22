# Order Notification API
Order notification API from KO->SP when customers orders new services. Services will not be activated by CO as it it SPs responsibility to activate services via the order-api.

## Example
Request:
```http
POST <url>/order-notification HTTP/1.1
Content-Type: application/json

{
  "accessId": "STTA0001",
  "offerIds": [123, 654],
  "customer": {
    "firstName": "Kalle",
    "lastName": "Anka",
    "personalIdentityNumber": "198401010101",
    "email": "karl@ankeborg.se",
    "phone": "0701010101",
    "invoiceAddress": {
       ...
    },
    "deliveryAdress": {
       ...
    }
  }
}
```

Response:
```http
HTTP/1.1 404 Forbidden
Content-Type: application/json

{
  message: Något verkar saknas på SPx sida, men var vänlig ring oss på 0812345678 för att får hjälp med din beställning.
}
```

## Request Parameters

| field                             | mandatory   | description                                                     |
|-----------------------------------|-------------|-----------------------------------------------------------------|
| `accessId`                        | *mandatory* | KO access ID.                                                   |
| `offerIds`                        | *mandatory* | [1..n] array of SP offerIds the customer wants to order.        |
| `customer`                        | *mandatory* | Customer object for SP order handling, will not be saved by KO. |
| `customer.firstName`              | *mandatory* | Customer data.                                                  |
| `customer.lastName`               | *mandatory* | Customer data.                                                  |
| `customer.personalIdentityNumber` | *mandatory* | Customer data.                                                  |
| `customer.email`                  | *optional*  | Customer data.                                                  |
| `customer.phone`                  | *optional*  | Customer data.                                                  |
| `customer.invoiceAddress`         | *optional*  |                                                                 |
| `customer.deliveryAddress`        | *optional*  |                                                                 |

## Response Parameters

| field     | mandatory   | description                                 |
|-----------|-------------|---------------------------------------------|
| `message` | *mandatory* | Customer-facing status message from SP side |

## Response HTTP codes

| Code  | Meaning                                                                  |
|-------|--------------------------------------------------------------------------|
| `200` | OK, order completed.                                                     |
| `202` | Order is pending on SP side, notification to customer is handeled by SP. |
| `400` | Malformed order-notification from KO.                                    |
| `403` | Forbidden, order not allowed by SP for Customer.                         |
| `404` | Access or Offer(s) not found.                                            |
| `500` | Error at SP Side                                                         |
| `303` | Special response code for usage with Web Portal Api, see below.          |

## 303, AKA SP-Redirect. (don't use http codes but status in reply? Other response code?)

On a response of 303 the KO will redirect the customer to the SP for final processing of the order. The returned reference will be used by SP to finalize order. See WebPortalApi specification.

The KO can attach an optional callback url. SP is expected to redirect customer to this url after finishing order.

### Example
Response:
```http
HTTP/1.1 303 See Other
Content-Type: application/json

{
  url: https://tl.com?what=ever&tl=needs&callback=www.test.se
}
```
Redirect:
https://tl.com?what=ever&tl=needs&callback=www.test.se&callback=path-to-ko-cart

### Regular order flow
```
                          +-----------+               +-----+                                           +-----+
                          | Customer  |               | CO  |                                           | TL  |
                          +-----------+               +-----+                                           +-----+
                                |                        |                                                 |
                                | Portal Order placed    |                                                 |
                                |----------------------->|                                                 |
                                |                        |                                                 |
                                |                        | POST https://tl.com/onapi/order-notification    |
                                |                        |------------------------------------------------>|
                                |                        |                                                 |
                                |                        |                                          200 OK |
                                |                        |<------------------------------------------------|
                                |                        |                                                 |
                                |           Confirmation |                                                 |
                                |<-----------------------|                                                 |
          --------------------\ |                        |                                                 |
          | Customer notified |-|                        |                                                 |
          |-------------------| |                        |                                                 |
                                |                        |                                                 |
                                |                        |     POST https://co.se/onapi/order              |
                                |                        |<------------------------------------------------|
                                |                        |                                                 |
                                |     Service activation |                                                 |
                                |<-----------------------|                                                 |
                                |                        |                                                 |
                                |                        | 200 OK                                          |
                                |                        |------------------------------------------------>|
------------------------------\ |                        |                                                 |
| Customer services activated |-|                        |                                                 |
|-----------------------------| |                        |                                                 |
                                |                        |                                                 |
```
### Webportal based order flow
```
                          +-----------+                          +-----+                                                +-----+
                          | Customer  |                          | CO  |                                                | TL  |
                          +-----------+                          +-----+                                                +-----+
                                |                                   |                                                      |
                                | Portal Order placed               |                                                      |
                                |---------------------------------->|                                                      |
                                |                                   |                                                      |
                                |                                   | POST https://tl.com/onapi/order-notification         |
                                |                                   |----------------------------------------------------->|
                                |                                   |                                                      |
                                |                                   |    303 {url: https://tl.com/portal/uuid-string-here} |
                                |                                   |<-----------------------------------------------------|
                                |                                   |                                                      |
                                |    HTTP Redirect to TL web-portal |                                                      |
                                |<----------------------------------|                                                      |
                                |                                   |                                                      |
                                | Visits TL Portal                  |                                                      |
                                |----------------------------------------------------------------------------------------->|
                                |                                   |                                                      | -------------------------------------\
                                |                                   |                                                      |-| TL Order flow however that happens |
                                |                                   |                                                      | |------------------------------------|
                                |                                   |                                                      |
                                |                                   |          POST https://co.se/onapi/order-notification |
                                |                                   |<-----------------------------------------------------|
                                |                                   |                                                      |
                                |                Service activation |                                                      |
                                |<----------------------------------|                                                      |
                                |                                   |                                                      |
                                |                                   | 200 OK                                               |
                                |                                   |----------------------------------------------------->|
------------------------------\ |                                   |                                                      |
| Customer services activated |-|                                   |                                                      |
|-----------------------------| |                                   |                                                      |
                                |                                   |                                                      |
                                |                                   |                       303 https://path-to-co-order   |
                                |                                   |<-----------------------------------------------------|
                                |                                   |                                                      |

#### ps.
```
object Customer CO TL
Customer->CO: Portal Order placed
CO->TL: POST https://tl.com/onapi/order-notification
TL->CO: 200 OK
CO->Customer:  Confirmation
note left of Customer: Customer notified
TL->CO: POST https://co.se/onapi/order-notification
CO->Customer: Service activation
CO->TL: 200 OK
note left of Customer: Customer services activated

object Customer CO TL
Customer->CO: Portal Order placed
CO->TL: POST https://tl.com/onapi/order-notification
TL->CO: 303 {url: https://tl.com/portal/uuid-string-here}
CO->Customer:  HTTP Redirect to TL web-portal
Customer->TL: Visits TL Portal
note right of TL: TL Order flow however that happens
TL->CO: POST https://co.se/onapi/order-notification
CO->Customer: Service activation
CO->TL: 200 OK
note left of Customer: Customer services activated
```
