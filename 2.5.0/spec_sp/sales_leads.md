# Sales leads API

Path /2.5/sp_spec/sales_leads/

Process option 1
![image](https://user-images.githubusercontent.com/48377287/114038491-3490b000-9882-11eb-8b65-7a90fb1970d0.png)

Process option 2
![image](https://user-images.githubusercontent.com/906435/83942941-70895d80-a7f8-11ea-998f-840452e222f2.png)

The sales leads API allows CO to notify SP about sales leads made by end customer. The end customer will select a service they want to order, as well as provide personal and billing information, and click to order. The CO will then send the order to SP, and the SP will either accept or deny the sales lead followed by creating an order to provision the service at requested date and time. If the order is denied, CO is able to present to end customer what went wrong. 
  
#### POST a sales lead

Request:
  
```http
POST /2.5/sp_spec/sales_leads/
Content-Type: application/json

{
	"deliveryDate": "string",
	"ssn":"string",
	"customerFirstname": "string",
	"customerLastName": "string",
	"customerPhone": "string",
	"customerMobilePhone": "string",
	"customerEmail": "string",
	"accessId": "string",
	"billingStreetName": "string",
	"billingStreetNumber": "string",
	"billingStreetLittera": "string",
	"billingEntrance": "string",
	"billingApartmentNumber": "string",
	"billingCity": "string",
	"billingZipcode": "string",
	"serviceId": "string",
	"campaignId": "string"
}
```
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
