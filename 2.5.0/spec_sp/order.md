# Order API

This API is used to order a product that the SP connects.

Path /2.5/sp_spec/sales_leads/

Process option 1
![image](https://user-images.githubusercontent.com/48377287/114038491-3490b000-9882-11eb-8b65-7a90fb1970d0.png)

Process option 2
![image](https://user-images.githubusercontent.com/906435/83942941-70895d80-a7f8-11ea-998f-840452e222f2.png)

The sales leads API allows CO to notify SP about sales leads made by end customer. The end customer will select a
service they want to order, as well as provide personal and billing information, and click to order. The CO will then
send the order to SP, and the SP will either accept or deny the sales lead followed by creating an order to provision
the service at requested date and time. If the order is denied, CO is able to present to end customer what went wrong.

#### POST a sales lead

Request:

```http
POST /2.5/sp_spec/sales_leads/
Content-Type: application/json
```

```json
{
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "coId": "Acme",
  "orderDateTime": "2021-05-03T20:31:15Z",
  "requestedDateTime": "2019-02-05T00:00:00Z",
  "products": [
    {
      "productId": "8732c2f065e2490babce820e94b1011a",
      "offeringId": "xxx"
    }
  ],
  "customerDetails": {
    "identifiedCustomer": true,
    "personalIdentityNumber": "string",
    "customerFirstname": "string",
    "customerLastName": "string",
    "customerPhone": "string",
    "customerMobilePhone": "string",
    "customerEmail": "string",
    "invoiceDetails": {
      "streetName": "string",
      "streetNumber": "string",
      "streetLittera": "string",
      "postalCode": "string",
      "city": "string"
    }
  }
}
```

```json
{
  "status": "",
  "message": ""
}
```

200

* ACTIVATED
* RECEIVED
* REJECT

400

```json
{
  "cause": "",
  "message": ""
}
```

* FAILED (kräver message)

# Responses

All error handling should be using status codes from HTTP, if possible with the free text field "cause" stating what
went wrong. If the server has an ID of the error (such as a fault number or, even better, a ticket ID) it should be
included in the cause field.

Example:

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{ "cause": "Unknown service: 'INTERNET'" }
```

Example 2:

```http
HTTP/1.1 500 Internal Server Error
Content-Type: application/json

{ "cause": "An Unknown error has occured. Error number 12345" }
```

## HTTP satus codes used (for full list, see RFC7231)

### 400 Bad request

Invalid data posted

### 401 Unauthorized

Invalid credentials

### 403 Forbidden

Not allowed with current credentials

### 404 Not found

Object not found (on valid API endpoint)

### 409 Conflict

Object is conflicting with other object (on valid API endpoint).

### 429 Too Many Requests

The client is sending too many requests to the server in too short time. If Retry-After is used in the response the
client should honor that time before sending any more requests.

### 500 Internal Server Error

Unrecoverable error

### 501 Not implemented

Response for unknown or unimplemented API endpoints

Response:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"orderId": "string"
}
```

Response if not OK

```HTTP/1.1 400 Bad request
Content-Type: application/json
{ "cause": "Social security number is missing or incorrect." }
```
