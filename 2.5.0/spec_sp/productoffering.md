# Product offerings API

This API lists services that are available to the end customer.

To list services and campaigns that are generally available through access points from the requesting CO population.

```http 
GET /2.5/productoffering/
Content-Type: application/json
```

Add the "accessId" from the CO accesses API to list the specific services and campaigns available on that particular
access point.

Request:
```http
GET /2.5/productoffering/[accessId]
Content-Type: application/json
```

Response:
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "serviceProvider": {
    "phone": "013-212121",
    "openingHours": "07:00-16:00",
    "email": "acmeab@example.com",
    "website": "https://acmeab.example.com",
    "presentation": "Acme AB är en rikstäckande leverantör av höghastighetsinternet",
    "files": [
      {
        "type": "TermsAndConditions",
        "url": "http://example.com/allmannavilkor.pdf",
        "updated": "2007-04-05T14:30Z"
      },
      {
        "type": "PrivacyPolicy",
        "url": "http://example.com/integritetspolicy.pdf",
        "updated": "2007-04-05T14:30Z"
      },
      {
        "type": "Logo",
        "url": "http://example.com/logo_small.jpg",
        "updated": "2007-04-05T14:30Z"
      }
    ]
  },
  "productOfferings": [
    {
      "coProducts": [
        "1000/1000"
      ],
      "productId": "1f94f25b-3ae0-434f-a49e-bc4d3093e399",
      "marketingInformation": {
        "productName": "Bredband 100/100",
        "description": "Bra snabbt Internet"
      },
      "files": [
        {
          "type": "TermsAndConditions",
          "url": "http://example.com/sarskildavilkor.pdf",
          "updated": "2007-04-05T14:30Z"
        },
        {
          "type": "Logo",
          "url": "http://example.com/logo_small.jpg",
          "updated": "2007-04-05T14:30Z"
        }
      ],
      "offerings": [
        {
          "offeringId": "821cfc90-762a-4272-aacf-ba7ffed8614c",
          "marketingInformation": {
            "offeringName": "Utan bindningstid",
            "description": "Bra snabbt Internet",
            "deliveryInformation": "Vi kontaktar dig om installation av CPE krävs",
            "startPrice": "0",
            "price": "250",
            "pricePeriod": "P1M",
            "periodOfNotice": "P1M",
            "agreementLength": "P1M"
          }
        },
        {
          "offeringId": "821cfc90-762a-4272-aacf-ba7ffed8614c",
          "marketingInformation": {
            "name": "Halva priset 3 månader",
            "description": "Första tre månaderna gratis, 12 månader bindningstid",
            "startPrice": "0",
            "price": "125",
            "pricePeriod": "P1M",
            "periodOfNotice": "P1M",
            "agreementLength": "P1Y",
            "campaignLength": "P3M",
            "basePrice": "250",
            "campaignCodes": ["billig", "hemlig"],
            "campaign": true
          }
        },
        {
          "productOfferingId": "c9c47535-ffa9-4456-9706-9ef590e1ce48",
          "marketingInformation": {
            "name": "Inklusive wifi-router",
            "description": "Få en exklusiv router med abonnemanget för endast 25 kr mer i månaden, 3 månader bindningstid.",
            "startPrice": "0",
            "price": "275",
            "pricePeriod": "P1M",
            "periodOfNotice": "P1M",
            "agreementLength": "P3M",
            "campaignLength": null,
            "surplusValue": "950"
          }
        }
      ]
    }
  ]
}
```

## serviceProvider

Object describing the service provider. The intended purpose is to allow portals to present the service provider and show contact details.

## serviceProvider.phone

Phone number to sales or customer service. 

 * Data format: [text](../common/dataformats.md#text)
 * Mandatory

## serviceProvider.openingHours

Regualar opening hours when calls will be answered.

 * Data format: [text](../common/dataformats.md#text)
 * Optional
 * Times should be presented in the format HH:mm, e.g. "07:30", and the opening hours of a day include both a start and an end time separated by '-' as in "07:30-17:00"
 * Optionally, opening hours can include the day of week, or indicate a span, e.g. "Monday 07:30-17:00" or "Monday-Friday 07:30-17:00".
 * Opening hours on different days of the week should be separated by ','.
 * Special opening hours on weekends should be surrounded by parentheses, unless the day of the week is stated specifically, e.g. "07:30-17:00 (10:00-15:00)"

 Examples: "07:30-17:00 (10:00-15:00)", "Monday-Friday 07:00-17:00, Saturday 09:00-13:00", "Monday-Thursday 07:00-17:00, Friday 07:00-15:00"

## serviceProvider.email

Email address to sales or customer service.

 * Data format: [text](../common/dataformats.md#text)
 * Required

## serviceProvider.website

The web address to the service provider pages.

 * Data format: [text](../common/dataformats.md#text)
 * Required

## serviceProvider.presentation

Short presentation of the service provider.

 * Data format: [text](../common/dataformats.md#text)
 * Required

## serviceProvider.files

Various files provided by the service provider that can be used by portals, e.g. images and documents.

 * Data format: JSON array of [file](../common/dataformats.md#file)
 * Mandatory

## serviceProvider.files.type

The type of file

    Data format: enumeration
    Mandatory

Valid values

    TermsAndConditions, general terms and conditions that must be accepted by the customer
    PrivacyPolicy, privacy policy that must be accepted by the customer
    Logo, service provider logo image

## serviceProvider.files.url

The full url to the file content

 * Data format: [text](../common/dataformats.md#text)
 * Required

## serviceProvider.files.updated

The datetime when the file was last updated (ISO-8601)

  * Data format: [dateTime](../common/dataformats.md#text)
  * Mandatory

## productOfferings.productOfferingId

The unique ID of the product, used when ordering a product

## productOfferings.marketingInformation.name

Name of the service, presentable to end customer

## productOfferings.marketingInformation.description

Description of the service, presentable to end customer

## productOfferings.marketingInformation.deliveryInformation

Information concerning delivery of the product.

# startPrice

# price

The service price in SEK.

# pricePeriod

The duration for a reoccurring payment, empty string for non reoccurring services.

ISO8601 duration.

## productOfferings.marketingInformation.periodOfNotice

The length of time needed for the end customer to cancel a subscription.

ISO8601 duration

## productOfferings.marketingInformation.agreementLength

The length of time from first delivery of service to pass before the agreement can be canceled.

ISO8601 duration

## productOfferings.campaignOfferings

List of offerings with values that replaces the values from the parent product offer if the campaign is chosen. If a
value is omitted, the value of the parent offering is used.
