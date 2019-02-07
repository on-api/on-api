




----------

# Ticket API


### Description
This specification provides functionality for trouble tickets to be handled between service providers and communication operators. 

Data communicated should only be related to its troubleshooting purpose or context.

CO = Comminicatoin Operator
SP = Service Provider

# Specification

## Reference index
### ticket
* GET [ticket](#get-ticket)
* POST [ticket](#post-ticket)
* PATCH [ticket](#patch-ticket)

## Requirements

**API Prefix:** `/ticket` 
eg: `domain.local/api/2.4/ticket/423323449`

## Endpoints


<h3 id="get-ticket">GET ticket</h3>

Fetch one or many tickets, able to filter by created timestamp or ticket status.

Request specific ticket:
```http
GET /api/2.4/ticket/{coTicketReference} 
```

Request tickets modified after timestamp:
```http
GET /api/2.4/ticket 
If-Modified-Since: Tue, 05 Feb 2019 14:03:15 GMT
```
Request tickets with status IN_PROGRESS_CO:
```http
GET /api/2.4/ticket?status=IN_PROGRESS_CO 
```

| Header | Description |
|--|--|
|If-Modified-Since|Filter by tickets modified after this timestamp|

| Query string | Type | Description |
|--|--|--|
|created|string (iso8601)|Filter by all tickets created after date|
|status|[CREATED, IN_PROGRESS_CO, IN_PROGRESS_SP, CLOSED]|Filter by status of ticket|

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "spReference": "Order#00123456",
  "coTicketReference": "TT00000123456",
  "spTicketReference": "CASE#000123456",
  "accessId": "51000000123456",
  "createdBy": "Anna Andersson",
  "createdAt": "2018-08-20T14:09:23Z",
  "updatedAt": "2018-08-25T08:34:11Z",
  "heading": "Heading for ticket",
  "description": "This customer is experiencing issues.",
  "comments": [
    {
      "createdBy": "Kalle Andersson",
      "message": "Configuration has been changed, please try again",
      "party": "CO",
      "createdAt": "2018-08-21T12:01:52Z"
    },
    {
      "createdBy": "Anna Andersson",
      "message": "No change in customers connection.",
      "party": "SP",
      "createdAt": "2018-08-25T08:34:11Z",
    }
  ],
  "status": "IN_PROGRESS_CO",
  "coSubscriptionId": "O00000123456",
  "problemType": "NO_LINK",
  "additionalInfo": {
    "ip": "169.254.1.1",
    "mac": "AB:CD:EF:12:34:56",
    "link": "false"
  },
  "callbackURL": "https://www.ispwebsite.se/api/ticketing/update/CASE#000123456"
}
```

| Parameter | Type | Description |
|--|--|--|
|coTicketReference|string (1-32)|CO Ticket Reference|
|spReference|string (1-32)|SP Reference|
|spTicketReference|string (1-32)|SP Ticket Reference|
|accessId|string (1-32)|Unique identifyer for a Access, owned by CO|
|createdBy|string|Created By User|
|createdAt|string (iso8601)|Created Time|
|updatedAt|string (iso8601)|Last Modified time|
|heading|string|Heading|
|description|string|Description|
|comments|Comments|List of Comments|
|comments#.createdBy|string|Created By User|
|comments#.message|string|Message|
|comments#.party|[SP,CO]|Party|
|comments#.createdTime|string (iso8601)|Created Time|
|status|[CREATED, IN_PROGRESS_CO, IN_PROGRESS_SP, CLOSED]|Status|
|problemType|[NO_LINK,NO_ACCESS,QUALITY,OTHER]|Problem Type|
|additionalInfo|additionalInfo|Additional info|
|additionalInfo.ip|string (7-19)|Customer IP|
|additionalInfo.mac|string (17)|Device MAC-address|
|additionalInfo.link|boolean|Customer Link Status|
|callbackURL|string|ISP Callback URL (OPTIONAL)|


<h3 id="post-ticket">POST ticket/{spTicketReference}</h3>

Create at ticket.

Request:

```http
POST /api/2.4/ticket
Content-Type: application/json

{
  "spReference": "Order#00123456",
  "spTicketReference": "CASE#000123456",
  "accessId": "51000000123456",
  "createdBy": "Anna Andersson",
  "heading": "Heading for ticket",
  "description": "This customer is experiencing issues.",
  "coSubscriptionId": "O00000123456",
  "problemType": "NO_LINK",
  "additionalInfo": {
    "ip": "169.254.1.1",
    "mac": "AB:CD:EF:12:34:56",
    "link": "false",
  },
  "callbackURL": "https://www.ispwebsite.se/api/ticketing/update/CASE#000123456",  
}
```

| Parameter | Type | Description |
|--|--|--|
|spReference|string (1-32)|SP Reference|
|spTicketReference|string (1-32)|SP Ticket Reference|
|accessId|string (1-32)|Unique identifyer for a Access, owned by CO|
|createdBy|string|Created By User|
|heading|string|Heading|
|description|string|Description|
|coSubscriptionId|string|Unique identifyer for a Subscription, owned by CO|
|problemtType|[NO_LINK,NO_ACCESS,QUALITY,OTHER]|Problem Type|
|additionalInfo|additionalInfo|Additional Info|
|additionalInfo#.ip|string (7-19)|Customer IP|
|additionalInfo#.mac|string (17)|Device MAC-address|
|additionalInfo#.link|boolean|Customer Link Status|
|callbackURL|string|ISP Callback URL (Optional)|


Response:
```http
HTTP/1.1 201 CREATED
Content-Type: application/json

{
  "coTicketReference": "TT00000123456",
  "status": "CREATED"
}
```


| Parameter | Type | Description |
|--|--|--|
|coTicketReference|string (1-32)|CO Ticket Reference|
|status|[CREATED]|Status|


<h3 id="patch-ticket">PATCH ticket/{coTicketReference}</h3>

Update ticket status and add comments to the ticket.
You have to close a ticket through this method.

```http
PATCH /api/2.4/ticket/{coTicketReference}
Content-Type: application/json

{
  "comment": "A comment.",
  "createdBy": "Anna Andersson",
  "status": "IN_PROGRESS_SP"
}
```
| Parameter | Type | Description |
|--|--|--|
|message|string|Message|
|createdBy|string|Created By|
|status|[CREATED, IN_PROGRESS_CO, IN_PROGRESS_SP, CLOSED]|Change ticket status


Response:
```http
HTTP/1.1 204 No Content
```

