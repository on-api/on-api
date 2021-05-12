# Order API

This API is used to order a product that the SP connects.

Path /2.5/sp_spec/order/

Process option 1
![image](https://user-images.githubusercontent.com/48377287/114038491-3490b000-9882-11eb-8b65-7a90fb1970d0.png)

Process option 2
![image](https://user-images.githubusercontent.com/906435/83942941-70895d80-a7f8-11ea-998f-840452e222f2.png)

The sales leads API allows CO to notify SP about sales leads made by end customer. The end customer will select a
service they want to order, as well as provide personal and billing information, and click to order. The CO will then
send the order to SP, and the SP will either accept or deny the sales lead followed by creating an order to provision
the service at requested date and time. If the order is denied, CO is able to present to end customer what went wrong.

## Request

```http
POST order/ HTTP/1.1
Content-Type: application/json
```

```json
{
  "coId": "Acme",
  "coAccessId": "8732c2f065e2490babce820e94b1011a",
  "operation": "ACTIVATE",
  "orderDateTime": "2021-05-03T20:31:15Z",
  "requestedDateTime": "2021-05-06T00:01:00Z",
  "products": [
    {
      "productId": "8732c2f065e2490babce820e94b1011a",
      "offeringId": "8732c2f065e2490babce820e94b1011a"
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

### coId

### coAccessId

### operation

### orderDateTime

### requestedDateTime

### products

### products.productId

### products.offeringId

### customerDetails

### customerDetails.identifiedCustomer

### customerDetails.personalIdentityNumber

### customerDetails.customerFirstname

### customerDetails.customerLastName

### customerDetails.customerPhone

### customerDetails.customerMobilePhone

### customerDetails.customerEmail

### customerDetails.invoiceDetails

### customerDetails.streetName

### customerDetails.streetNumber

### customerDetails.streetLittera

### customerDetails.postalCode

### customerDetails.city

## Response

```http
HTTP/1.1 200 OK Content-Type: application/json
```

```json
{
  "status": "",
  "message": ""
}
```

### status
One of the following values
* ACTIVATED
  * Order is accepted and completed, the services are delivered
* RECEIVED
  * Order is accepted and services will be delivered
* REJECTED
  * Order is not accepted

### message
string
A message presentable to the customer

Error handling according to [common responses](../common/responses.md) except for data input errors that are handled by 
a custom http code 400 error with the addition of a message field.

```http
HTTP/1.1 400 Bad Request Content-Type: application/json
```

```json
{
  "cause": "Bad customerDetails.personalIdentityNumber",
  "message": "Social security number is missing or incorrect."
}
```

### cause
String 
An internal message not to be presented to the customer 

### message
A human friendly message that can be presented to the customer
