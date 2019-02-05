# Open Network API 2.4

This API aims to provide the necessary functionality to enable automation and communication between service providers (SP) 
and open access network communication operators (CO). Enabling service providers to deliver services to the end customer in a secure 
and efficient way without transmitting unnecessary personal information. 

The API exposes the available network accesses and enables the SP to manage the last mile delivery in open networks.

Some of the properties of this API includes: 

 * Provide the SP with available accesses from the CO, accesses include
   * Address
   * Network outlet
   * Deliverable services
   * Customer placed equipment
 * Manageability of deliverable services
 * Secure communications
 * GDPR safe operations
 * Support for automated processes

## Table of contents

  1. [Changelog](changelog.md)
  2. [Accesses](accesses.md)
  3. [Data formats](dataformats.md)
  4. [Endpoints](endpoints.md)
  5. [Equipment based localization](equipment_based_localization.md)
  6. [Error handling](error_handling.md)
  7. [Option82 lookup](option82_lookup.md)
  8. [Order](order.md)
  9. [Order events](orderevents.md)
 10. [Querying the service provider for service information](query_sp.md)
 11. [Querying the service provider for customer information](access_customer_info.md)
 12. [Services - list active services ](services.md)
 13. [Web portal - Forward customers to SP service portals](web_portal.md)
 
 
## General guidelines

Open Network API is a REST/JSON API and must be exposed through a secure HTTP/TLS connection.

Authentication is handled with the basic authentication scheme. (see [RFC 7617](https://tools.ietf.org/html/rfc7617))


The API URL must contain the API version number. The API subset must use the documented path in the following format.
/[api version number]/[api endpoint]

Examples: 
   * https://server.com/onapi/2.4/accesses/
   * https://server.com/2.4/accesses/
   * https://server.com/some/longer/path/2.4/accesses/