# Service offerings API

This API lists services that are available to the end customer.

To list services and campaigns that are generally available through access points from the requesting CO population.

```http 
GET /2.5/service/
Content-Type: application/json
```

Add the "accessId" from the CO accesses API to list the specific services and campaigns available on that particular
access point.

```http
GET /2.5/service/[accessId]
Content-Type: application/json
```

Response:

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
      "productOfferingId": "1f94f25b-3ae0-434f-a49e-bc4d3093e399",
      "marketingInformation": {
        "name": "Bredband 100/100",
        "description": "Bra snabbt Internet",
        "deliveryInformation": "Vi kontaktar dig om installation av CPE krävs",
        "startPrice": "0",
        "price": "250",
        "pricePeriod": "P1M",
        "periodOfNotice": "P1M",
        "agreementLength": "P1M"
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
      "campaignOfferings": [
        {
          "productOfferingId": "821cfc90-762a-4272-aacf-ba7ffed8614c",
          "marketingInformation": {
            "name": "Halva priset 3 månader",
            "description": "Första tre månaderna gratis, 12 månader bindningstid",
            "startPrice": "0",
            "price": "125",
            "pricePeriod": "P1M",
            "periodOfNotice": "P1M",
            "agreementLength": "P1Y",
            "campaignLength": "P3M"
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
            "campaignLength": null
          }
        }
      ]
    }
  ]
}
```

## serviceProvider

Object describing the service provider

## serviceProvider.phone

Phone number to sales or customer service

## serviceProvider.openingHours

## serviceProvider.email

## serviceProvider.website

## serviceProvider.presentation

## serviceProvider.files

## serviceProvider.files.type

## serviceProvider.files.url

## serviceProvider.files.updated

ISO8601 date time

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
