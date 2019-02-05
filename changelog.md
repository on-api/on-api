# Changelog

## Changes since 2.3.1

 * All documentation is translated to english
 * technical_info.md replaces fm_linkstatus.md
 * accesses.md replaces feasibility.md and availability.md
 * dataformats.md replaces option82.md
 * error_handling.md is added
 * endpoints.md is added
 * co_active_services.md is renamed to services.md
 * README.md replaces index.md and misc.md
 * spSubscriptionId is added to the API endpoints accesses, services and order
 * coSubscriptionId is added to the API endpoints accesses, services and order
 * requestedDateTime added to order API
 * expectedCompletionDate added to order API
 * characteristics added to order API
 * Orders can now be scheduled to run in the future
 * Orders can be updated until the requestedDateTime is reached
 * Orders can be cancelled/deleted until the requestedDateTime is reached
 * new operations is added to the order API
   * SUSPEND
   * RESUME
   * MODIFY
   * CHANGE

 * New value for premisesType in accesses MDU_TECHNICAL 