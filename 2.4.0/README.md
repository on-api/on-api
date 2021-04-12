## Table of contents

* [Accesses](spec/accesses.md)
* [Changelog](changelog.md)
* [Data formats](common/dataformats.md)
* [Endpoints](spec/endpoints.md)
* [Invoice specification](spec/invoice_specification.md)
* [Option82 lookup](spec/option82_lookup.md)
* [Order](spec/orders.md)
* [Order events](spec/orderevents.md)
* [Responses](common/responses.md)
* [SP contacts](spec/contacts.md)
* [Subscriptions - list active services](spec/subscriptions.md)
* [Technical information](spec/technical_info.md)
* [Tickets](spec/tickets.md)
* [Web portal - Forward customers to SP service portals](spec/web_portal.md)
 
## General guidelines

Open Network API is a REST/JSON API and must be exposed through a secure HTTP/TLS connection.

Authentication is handled with the basic authentication scheme. (see [RFC 7617](https://tools.ietf.org/html/rfc7617))


The API URL must contain the API version number. The API subset must use the documented path in the following format.
/[api version number]/[api endpoint]

Examples: 
   * https://server.com/onapi/2.4/accesses/
   * https://server.com/2.4/accesses/ 
   * https://server.com/some/longer/path/2.4/accesses/
