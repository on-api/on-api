## Open Networks API

Open Networks API (ON-API) is a communication protocol which enables automation of processes between Service Providers (SP) and Service Operators (SO).
This is done via a standardized machine-to-machine interface (REST api) specification with requirements of how data should be processed and presented.
The main purpose of the API is to provide automated communication as an alternative to manual processes. 

The specification includes support for areas such as:

- Addresses
- Orders
- Subscriptions
- Tickets
- Troubleshooting
- Invoicing

In summary, the API is a specification which defines how data shall be formatted and transmitted between parties, for a machine to be able to interpret the data from a set of rules, as opposed to human interpretation.  
An example is the manual order process, where the Service Provider must first activate a service in an internal system, followed by either requesting an external activation by e-mail or in an external system. This process is replaced by a machine on each end that will automatically interpret the data in an order and perform the requested operation.

### Versions

- [ON-API 2.4.0](2.4.0)


## Implementation status

Below is a set of tables describing ON-API implementation status per company.

To update your company's status, or if your company is not on the list, send a pull request, create an issue or write on Slack.

**Format:** `Yes`, `No` or ETA. eg `Q3 2020`


### ON-API 2.4

| CO | [Accesses](2.4.0/spec/accesses.md) | [Order](2.4.0/spec/orders.md) | [Tickets](2.4.0/spec/tickets.md) | [Technical information](2.4.0/spec/technical_info.md) | [Contacts](2.4.0/spec/contacts.md) | [Subscriptions](2.4.0/spec/subscriptions.md) | [Invoice Specification](2.4.0/spec/invoice_specification.md)
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

| SP | [Accesses](2.4.0/spec/accesses.md) | [Order](2.4.0/spec/orders.md) | [Tickets](2.4.0/spec/tickets.md) | [Technical information](2.4.0/spec/technical_info.md) | [Contacts](2.4.0/spec/contacts.md) | [Subscriptions](2.4.0/spec/subscriptions.md) | [Invoice Specification](2.4.0/spec/invoice_specification.md)
|-|-|-|-|-|-|-|-|
|A3| | | | | | | |
|Bahnhof| | | | | | | |
|Bredband2| | | | | | | |
|Comhem| | | | | | | |
|Junet| | | | | | | |
|Ownit| | | | | | | |
|Serverado| | | | | | | |
|Telenor|No|No|No|No|No|No|No|
|Th1ng| | | | | | | |
|Viasat| | | | | | | |

### ON-API 2.3.1

| CO | [Availability](https://github.com/on-api/on-api-release-2.3.1/blob/master/availability.md) | [Feasibility](https://github.com/on-api/on-api-release-2.3.1/blob/master/feasibility.md) | [Service Activation](https://github.com/on-api/on-api-release-2.3.1/blob/master/service_activation.md) | [Link status](https://github.com/on-api/on-api-release-2.3.1/blob/master/fm_linkstatus.md) | [Access customer info](https://github.com/on-api/on-api-release-2.3.1/blob/master/access_customer_info.md) | [CO Active services](https://github.com/on-api/on-api-release-2.3.1/blob/master/co_active_services.md)
|-|-|-|-|-|-|-|
|Bjäre Kraft| | | | | | |
|Borlänge Energi| | | | | | |
|IP-Only| | | | | | |
|Itux| | | | | | |
|Open Infra| | | | | | |
|Open Universe| | | | | | |
|Skellefteå Kraft| | | | | | |
|Zitius| | | | | | |

---

| SP | [Availability](https://github.com/on-api/on-api-release-2.3.1/blob/master/availability.md) | [Feasibility](https://github.com/on-api/on-api-release-2.3.1/blob/master/feasibility.md) | [Service Activation](https://github.com/on-api/on-api-release-2.3.1/blob/master/service_activation.md) | [Link status](https://github.com/on-api/on-api-release-2.3.1/blob/master/fm_linkstatus.md) | [Access customer info](https://github.com/on-api/on-api-release-2.3.1/blob/master/access_customer_info.md) | [CO Active services](https://github.com/on-api/on-api-release-2.3.1/blob/master/co_active_services.md)
|-|-|-|-|-|-|-|
|A3| | | | | | |
|Bahnhof| | | | | | |
|Bredband2| | | | | | |
|Comhem| | | | | | |
|Junet| | | | | | |
|Ownit| | | | | | |
|Serverado| | | | | | |
|Telenor| | |Yes| | |
|Th1ng| | | | | | |
|Viasat| | | | | | |
