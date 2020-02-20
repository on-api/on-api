## Table of contents

* [Changelog](changelog.md)
* [Accesses](spec/accesses.md)
* [Data formats](common/dataformats.md)
* [Endpoints](spec/endpoints.md)
* [Responses](common/responses.md)
* [Option82 lookup](spec/option82_lookup.md)
* [Order](spec/orders.md)
* [Order events](spec/orderevents.md)
* [SP contacts](spec/contacts.md)
* [Subscriptions - list active services](spec/subscriptions.md)
* [Web portal - Forward customers to SP service portals](spec/web_portal.md)
* [Tickets](spec/tickets.md)
* [Technical information](spec/technical_info.md)
 
## General guidelines

Open Network API is a REST/JSON API and must be exposed through a secure HTTP/TLS connection.

Authentication is handled with the basic authentication scheme. (see [RFC 7617](https://tools.ietf.org/html/rfc7617))


The API URL must contain the API version number. The API subset must use the documented path in the following format.
/[api version number]/[api endpoint]

Examples: 
   * https://server.com/onapi/2.4/accesses/
   * https://server.com/2.4/accesses/ 
   * https://server.com/some/longer/path/2.4/accesses/


## Implementation status

Below is a list of ON-API 2.4 implementation status per company.
Specified by `Yes`, `No` or ETA. eg `Q3 2020`

To update your company's status, or if your company is not on the list, send a pull request or write on Slack.

| CO | [Accesses](spec/accesses.md) | [Order](spec/orders.md) | [Tickets](spec/tickets.md) | [Technical information](spec/technical_info.md) | [Contacts](spec/contacts.md) | [Subscriptions](spec/subscriptions.md) | [Invoice Specification](spec/invoice_specification.md)
|-|-|-|-|-|-|-|-|
|Bjäre Kraft| | | | | | | |
|Borlänge Energi| | | | | | | |
|IP-Only| | | | | | | |
|Itux| | | | | | | |
|Open Infra| | | | | | | |
|Open Universe| | | | | | | |
|Skellefteå Kraft| | | | | | | |
|Zitius| | | | | | | |

---

| SP | [Accesses](spec/accesses.md) | [Order](spec/orders.md) | [Tickets](spec/tickets.md) | [Technical information](spec/technical_info.md) | [Contacts](spec/contacts.md) | [Subscriptions](spec/subscriptions.md) | [Invoice Specification](spec/invoice_specification.md)
|-|-|-|-|-|-|-|-|
|A3| | | | | | | |
|Bahnhof| | | | | | | |
|Bredband2| | | | | | | |
|Comhem| | | | | | | |
|Junet| | | | | | | |
|Ownit| | | | | | | |
|Serverado| | | | | | | |
|Telenor| | | | | | | |
|Th1ng| | | | | | | |
|Viasat| | | | | | | |
