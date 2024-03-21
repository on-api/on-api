# Changelog

## Changes since 2.5

 * New Endpoint - [Service](spec/services.md)
 * Accesses Endpoint
   - services sub-part has been removed into its own endpoint [Service](spec/services.md)
   - subscription sub-part has been removed into its own endpoint [Subscription](spec/subscriptions.md)
   - Added fields 
     - [nationalAddressUUID](spec/accesses.md#nationaladdressuuid)
     - [priceGroup](spec/accesses.md#pricegroup)
   - Removed fields
     - coNetworkAgreement
     - coFiberConverter
     - coCpeSwitch
     - coCpeRouter
 * Subscriptions Endpoint
   - Addition of get one subscription
 * Technical Info Endpoint
   - Clarification that all parameters are optional
   - Renamed parameter fiber to transceiver
   - Added parameters
     - learnAt
     - lastRenew
     - adminDown
     - transceiver.biasTx
     - transceiver.supplyVoltage
     - transceiver.vendor
     - transceiver.partNumber
     - transceiver.serialNumber
 * Invoice Specification Endpoint
   - Updated field descriptions
   - Added support for Excel option
   - Added general rules for [fields](spec/invoice_specification.md#fields)
   - Renamed fields 
     - serviceProvider/name to [spName](spec/invoice_specification.md#spname)
     - address to [access](spec/invoice_specification.md#access)
     - address/apartmentNumber [access/mduApartmentNumber](spec/invoice_specification.md#accessmduapartmentnumber)
     - address/apartmentAddress [access/mduDistinguisher](spec/invoice_specification.md#accessmdudistinguisher)
     - address/apartmentOutlet to [access/outlet](spec/invoice_specification.md#accessoutlet)
     - subscription/serviceName to [subscription/service](spec/invoice_specification.md#subscriptionservice)
   - Added fields
     - [address/premisesType](invoice_specification.md#accesspremisestype)
     - [invoice/invoiceType](spec/invoice_specification.md#invoiceinvoicetype)
     - [invoice/comment](spec/invoice_specification.md#invoicecomment)
 * Data formats
   - Added data format [number](common/dataformats.md#number)

### Minor changes since 2.5
 * Many endpoints were incorrectly labelled as APIs. It is one API (ON-API) with many endpoints (Accesses, Services, Subscriptions, etc.)
 * Added "/onapi/2.6/" to paths in examples where it was missed
 * Substituted GUIDs or strings of example values to instead specify the field used: for example GET /onapi/2.4/accesses/STTA0001 HTTP/1.1 was altered to GET /onapi/2.4/accesses/{accessId} HTTP/1.1
 * Fix broken links and typos (applied to all versions)
 
