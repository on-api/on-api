# Changelog

## Changes since 2.5

 * New Endpoint - [Service](spec/services.md)
 * Accesses Endpoint
   - services sub-part has been removed into its own endpoint [Service](spec/services.md)
   - subscription sub-part has been removed into its own endpoint [Subscription](spec/subscriptions.md)
 * Subscription Endpoint - Addition of get one subscription

### Minor changes since 2.5
 * Many endpoints was incorrectly labelled as APIs. It is one API (ON-api) with many endpoints (Accesses, Services, Subscriptions etc).
 * Added "/onapi/2.6/" to paths in examples where it was missed.
 * Substituted Guids or strings of example values to instead specify the field used: for example GET /onapi/2.4/accesses/STTA0001 HTTP/1.1 was altered to GET /onapi/2.4/accesses/{accessId} HTTP/1.1 
