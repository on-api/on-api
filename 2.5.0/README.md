## Table of contents

### Common documentation

* [Changelog](changelog.md)
* [Data formats](common/dataformats.md)
* [Endpoints](common/endpoints.md)
* [Responses](common/responses.md)

### API's exposed by communication operators

* [Accesses](spec/accesses.md)
* [Events](spec/events.md)
* [Invoice specification](spec/invoice_specification.md)
* [Option82 lookup](spec/option82_lookup.md)
* [Order events](spec/orderevents.md)
* [Orders](spec/orders.md)
* [Subscriptions](spec/subscriptions.md)
* [Technical information](spec/technical_info.md)
* [Tickets](spec/tickets.md)

### API's exposed by service providers

* [SP contacts](spec_sp/contacts.md)
* [CO order](spec_sp/coorder.md)
* [Order](spec_sp/order.md)
* [Order Notice](spec_sp/ordernotice.md)
* [Products](spec_sp/products.md)
* [Web portal](spec_sp/web_portal.md)

 
## General guidelines

Open Network API is a REST/JSON API and must be exposed through a secure HTTP/TLS connection.

Authentication is handled with the basic authentication scheme. (see [RFC 7617](https://tools.ietf.org/html/rfc7617))


The API URL must contain the API version number. The API subset must use the documented path in the following format.
/[api version number]/[api endpoint]

Examples: 
   * https://server.com/onapi/2.5/accesses/
   * https://server.com/2.5/accesses/ 
   * https://server.com/some/longer/path/2.5/accesses/
