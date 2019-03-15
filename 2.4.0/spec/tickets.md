

----------

# Tickets API


### Description
This specification provides functionality for trouble tickets to be handled between service providers and communication operators. 

Data communicated should only be related to its troubleshooting purpose or context.

See events specification for sending notifications for when a ticket has been updated.

CO = Communication Operator
SP = Service Provider

# Specification

## Reference index
### ticket
* GET [tickets](#get-tickets)
* POST [tickets](#post-tickets)
* PATCH [tickets](#patch-tickets)

## Requirements

**API Prefix:** `/ticket` 
eg: `domain.local/api/2.4/tickets/423323449`

## Endpoints


<h3 id="get-tickets">GET tickets</h3>

Fetch one or many tickets, able to filter by created timestamp or ticket status.

Request all tickets:
```http
GET /api/2.4/tickets
```

Request ticket:
```http
GET /api/2.4/tickets/{coTicketReference} 
```



Request tickets modified after timestamp:
```http
GET /api/2.4/tickets 
If-Modified-Since: Tue, 05 Feb 2019 14:03:15 GMT
```
Request tickets with status IN_PROGRESS_CO:
```http
GET /api/2.4/tickets?status=IN_PROGRESS_CO 
```

| Header | Description |
|--|--|
|If-Modified-Since|Filter by tickets modified after this timestamp|

| Query string | Type | Description |
|--|--|--|
|created|string (iso8601)|Filter by all tickets created after date|
|status|[CREATED, IN_PROGRESS_CO, IN_PROGRESS_SP, CLOSED]|Filter by status of ticket|

List response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "coTicketReference": "TT00000123456",
    "spTicketReference": "CASE#000123456",
    "status": "IN_PROGRESS_CO",
    "responsible": ""
  },
  ...
]
```

Ticket response:
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
      "createdAt": "2018-08-21T12:01:52Z"
    },
    {
      "createdBy": "Anna Andersson",
      "message": "No change in customers connection.",
      "createdAt": "2018-08-25T08:34:11Z"
    }
  ],
  "status": "IN_PROGRESS_CO",
  "responsible": "CO",
  "coSubscription": "O00000123456",
  "problemType": "NO_LINK",
  "additionalInfo": {
    "ip": "169.254.1.1",
    "mac": "AB:CD:EF:12:34:56",
    "link": "false"
  }
}
```

| Parameter | Type | Description |
|--|--|--|
|coTicketReference|string|CO Ticket Reference|
|spReference|string|SP Reference|
|spTicketReference|string|SP Ticket Reference|
|accessId|string|Unique identifier for a Access, owned by CO|
|createdBy|string|Created By User|
|createdAt|string|Created Time|
|updatedAt|string|Last Modified time|
|heading|string|Heading|
|description|string|Description|
|comments|Comments|List of Comments|
|comments.createdBy|string|Created By User|
|comments.message|string|Message|
|comments.createdAt|string|Created Time|
|status|[CREATED, IN_PROGRESS_CO, IN_PROGRESS_SP, CLOSED]|Status|
|responsible|[SP,CO]|Responsible party, used for SLA calculation|
|coSubscription|string (optional)|Unique identifier for a Subscription, owned by CO|
|problemType|[NO_LINK,NO_ACCESS,QUALITY,OTHER]|Problem Type|
|additionalInfo|object|Additional info|
|additionalInfo.ip|string|Customer IP|
|additionalInfo.mac|string|Device MAC-address|
|additionalInfo.link|boolean|Customer Link Status|


<h3 id="post-tickets">POST tickets</h3>

Create at ticket.

Request:

```http
POST /api/2.4/tickets
Content-Type: application/json

{
  "spReference": "Order#00123456",
  "spTicketReference": "CASE#000123456",
  "accessId": "51000000123456",
  "createdBy": "Anna Andersson",
  "heading": "Heading for ticket",
  "description": "This customer is experiencing issues.",
  "coSubscription": "O00000123456",
  "problemType": "NO_LINK",
  "additionalInfo": {
    "ip": "169.254.1.1",
    "mac": "AB:CD:EF:12:34:56",
    "link": "false",
  }
}
```

| Parameter | Type | Description |
|--|--|--|
|spReference|string (optional)|SP Reference|
|spTicketReference|string (optional)|SP Ticket Reference|
|accessId|string |Unique identifier for a Access, owned by CO|
|createdBy|string|Created By User|
|heading|string|Heading|
|description|string|Description|
|coSubscription|string (optional)|Unique identifier for a Subscription, owned by CO|
|problemType|[NO_LINK,NO_ACCESS,QUALITY,OTHER]|Problem Type|
|additionalInfo|object|Additional Info|
|additionalInfo.ip|string|Customer IP|
|additionalInfo.mac|string|Device MAC-address|
|additionalInfo.link|boolean|Customer Link Status|


Response:
```http
HTTP/1.1 201 CREATED
Content-Type: application/json

{
  "coTicketReference": "TT00000123456"
}
```


| Parameter | Type | Description |
|--|--|--|
|coTicketReference|string|CO Ticket Reference|


<h3 id="patch-tickets">PATCH tickets/{coTicketReference}</h3>

Update ticket status and add comments to the ticket.
This method is also used when closing a ticket.

```http
PATCH /api/2.4/tickets/{coTicketReference}
Content-Type: application/json

{
  "comment": {
    "message": "A comment.",
    "createdBy": "Anna Andersson"
  },
  "status": "IN_PROGRESS_SP",
  "responsible": "CO"
}
```
| Parameter | Type | Description |
|--|--|--|
|comment|object|Comment|
|comment.message|string|Message|
|comment.createdBy|string|Created by|
|status|[CREATED, IN_PROGRESS_CO, IN_PROGRESS_SP, CLOSED] (optional)|Change ticket status
|responsible|[SP,CO] (optional)|Responsible party, used for SLA calculation. Mandatory when closing a ticket. |

Response:
```http
HTTP/1.1 204 No Content
```
