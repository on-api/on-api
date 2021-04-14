# Service API

This API lists services that are available to the service providers end customer.

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
  "services": [
    {
      "serviceId": "1f94f25b-3ae0-434f-a49e-bc4d3093e399",
      "name": "Bredband 100/100",
      "description": "Bra snabbt internet",
      "startPrice": "0",
      "price": "250",
      "pricePeriod": "P1M",
      "periodOfNotice": "P1M",
      "agreementLength": "P1M",
      "documents": [
        {
          "name": "Allmänna vilkor",
          "url": "http://example.com/vilkor.pdf",
          "updated": "2007-04-05T14:30Z"
        },
        {
          "name": "Integritetspolicy",
          "url": "http://example.com/integritetspolicy.pdf",
          "updated": "2007-04-05T14:30Z"
        }
      ],
      "campaigns": [
        {
          "campaignId": "821cfc90-762a-4272-aacf-ba7ffed8614c",
          "name": "Halva priset 3 månader",
          "description": "First three months for free, 12 months binding time",
          "startPrice": "0",
          "price": "125",
          "pricePeriod": "P1M",
          "periodOfNotice": "P1M",
          "agreementLength": "P1Y"
        },
        {
          "campaignId": "c9c47535-ffa9-4456-9706-9ef590e1ce48",
          "name": "Inklusive wifi-router",
          "description": "Få en exklusiv router med abonnemanget",
          "startPrice": "0",
          "price": "275",
          "pricePeriod": "P1M",
          "periodOfNotice": "P1M",
          "agreementLength": "P3M"
        }
      ]
    }
  ]
}
```

## serviceId

The unique ID of the service, used when ordering a service.

## name

Name of the service, presentable to end customer.

## description

Description of the service, presentable to end customer.

## periodOfNotice

The length of time needed for the end customer to cancel a subscription.

ISO8601 duration.

## agreementLength

The length of time from first delivery of service to pass before the agreement can be canceled.

ISO8601 duration.

# startPrice

# price

The service price in SEK.

# pricePeriod

The duration for a reoccurring payment, empty string for non reoccurring services.

ISO8601 duration.

# campaigns

List of campaigns available on this service.

# campaign/campaignId

The unique ID of the campaign, used when ordering a service with a campaign added.

# name

Name of the campaign, presentable to end customer.

# description

Description of the campaign, presentable to the end customer.

# price

Can be omitted if unchanged from the service value. Replaces the service price.

# pricePeriod

Can be omitted if unchanged from the service value. Replaces the service price period.

## periodOfNotice

Can be omitted if unchanged from the service value. Replaces the service period of notice.

# agreementLength

Can be omitted if unchanged from the service value. Replaces the service agreement length.
