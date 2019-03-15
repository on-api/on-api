# Contact information to end user

## Description
The API enables Communication Operators to query the Service Provider for contact details to an end user.

_**Note:**_  This API is hosted by the service provider, and the communication operator is the client.

## Specification
The fields `reason` and `spTicketReference` is used to able to track requests of personal information.
Providing spTicketReference makes `reason` unnecessary.

Request information with a reason:
```http
POST /2.4/contacts/{ spReference }

{
  "reason": "Reason for request"
}
```

Request information with a ticket reference:
```http
POST /2.4/contacts/{ spReference }

{
  "spTicketReference": "123"
}
```

|Field|Description|
|-|-|
|spReference|The spReference value for the service that the end user is using|
|spTicketReference|spTicketReference is taken from the on-api ticket, used for tracking|


Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@johndoe.com",
  "phone": "",
  "mobilePhone": ""
}
```


|Field|Description|
|-|-|
|name||
|email||
|phone||
|mobilePhone||


For data format, see [data formats](dataformats.md)
