# Changelog

## Changes since 2.3.1

 * All documentation is translated to English
 * [Technical Info](technical_info.md) replaces [Fault Management: Link Status API](https://github.com/on-api/on-api-release-2.3.1/blob/master/fm_linkstatus.md)
 * [Accesses](accesses.md) replaces 
    * [Feasibility](https://github.com/on-api/on-api-release-2.3.1/blob/master/feasibility.md)
    * [Availability](https://github.com/on-api/on-api-release-2.3.1/blob/master/availability.md)
 * [Data formats](dataformats.md) replaces [Option82-format](https://github.com/on-api/on-api-release-2.3.1/blob/master/option82.md)
 * A separate description of [response codes](https://github.com/on-api/onapi-inprogress-2.4/blob/master/response_codes.md)  is added
 * New API - [Endpoints](endpoints.md)
 * co_active_services.md is renamed to services.md
 * [README.md](README.md) replaces 
    * index.md 
    * misc.md
 * spSubscriptionId is added to the API endpoints accesses, services and order
 * subscriptionId is added to the API endpoints accesses, services and order
 * requestedDateTime added to order API
 * expectedCompletionDate added to order API
 * characteristics added to order, subscriptions and accesses API
 * Orders can now be scheduled to run in the future
 * Orders can be updated until the requestedDateTime is reached
 * Orders can be cancelled/deleted until the requestedDateTime is reached
 * new operations is added to the order API
   * SUSPEND
   * RESUME
   * MODIFY
   * CHANGE
 * New value for premisesType in accesses MDU_TECHNICAL 
 * [order events](https://github.com/on-api/on-api-release-2.3.1/blob/master/order_events.md) is replaced by a more generic [events](events.md)
 * [DHCP-lookup](dhcplookup.md) replaces [Option82 Lookup](https://github.com/on-api/on-api-release-2.3.1/blob/master/option82_lookup.md)
 * New API - [Equipment based localization](equipment_based_localization.md)
 * [Accesses](accesses.md) - active is renamed to subscriptions
 * New API - [Invoice specification](invoice_specification.md)
 * New API - [Ticket API](tickets.md)
 * New API - [Contacts API](contacts.md)