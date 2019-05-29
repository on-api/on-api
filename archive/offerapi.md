# Offer API

crud api to create campaing and offers

## offer/post

Request:
```http
POST <url>/offer HTTP/1.1
{
  "startDate": "2018-05-23",
  "endDate": "2019-04-20",
  "isPublished": 0,
  "spOfferReference": 10,
  "products": ["iptv-ext-vod", "Transmission 100/100"],
  "population": [{
     "id": "Fastighets AB",
     "startPrice": 100,
     "monthlyFee": 100
  }],
  "campaigns": [...],
  "presentation": {
    "name": "Surfa och Ring till bra priser!",
    "description": "Lots and lots of formated text here",
    "shortDescription": "A bit shorter, unformated text here",
    "resources": [{
        "name": "testingl.png",
        "data": "<Base64>"
     }]
  },
}
```

Response:
```http
HTTP:1/1 201 Created
Location: <url>/offer/2
```
