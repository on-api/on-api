# Invoice specification

This endpoint aims to provide the service provider (SP) with a specification of each billing item, this enables the SP 
to follow up and verify the invoice and correct service delivery.

The API provides both an CSV export and a JSON equivalent.


The CSV version is compliant with the swedish service provider organisation (SSP) specification for invoice-details.
The JSON version includes the same fields as the CSV version but in a structure with more dimensions.

Example: 

``` 
[
    {
        "address": {
            "accessID": "6748f377-0d01-49f9-ae62-f18c3a4f719b",
            "streetName": "Some street",
            "streetNumber": "6",
            "streetLittera": "A",
            "postalCode": "12345",
            "city": "Somecity",
            "apartmentNumber": 1012,
            "apartmentAddress": "apartment 15",
            "apartmentOutlet": "ABC123"
        },
        "serviceProvider": {
            "name": "Acme"
        },
        "coID": "Somecity-net",
        "invoice": {
            "listPrice": "0",
            "billingItem": "Acme 100/10",
            "rowType": "PERIODIC_FEE",
            "fromDate": "2018-09-03",
            "toDate": "2018-09-03",
            "creditAmount": "0",
            "invoicedAmount": "0"
        },
        "subscription": {
            "serviceName": "Acme 100/10",
            "connectionDate": "2018-09-03",
            "disconnectionDate": "2018-09-03",
            "spReference": "5d014d56-e86e-4ffc-bdaf-4aaab9a4f4f1",
            "spCustomerReference": "160c777f-554e-48e9-a990-4cbace468d7d",
            "coSubscriptionId": "ea3d28c0-8ab5-4c2b-81c1-4ec9f57fc3e3"
        },
        "population": "Test population"
    },
    {
        "address": {
            "accessID": "8e81db10-f10a-430f-9bac-ec361306d809",
            "streetName": "Some street",
            "streetNumber": "7",
            "streetLittera": null,
            "postalCode": "12345",
            "city": "Somecity",
            "apartmentNumber": null,
            "apartmentAddress": null,
            "apartmentOutlet": null
        },
        "serviceProvider": {
            "name": "Acme"
        },
        "coID": "Somecity-net",
        "invoice": {
            "listPrice": "0",
            "billingItem": "Acme 100/10",
            "rowType": "PERIODIC_FEE",
            "fromDate": "2018-09-03",
            "toDate": "2018-09-03",
            "creditAmount": "0",
            "invoicedAmount": "0"
        },
        "subscription": {
            "serviceName": "Acme 100/10",
            "connectionDate": "2018-09-03",
            "disconnectionDate": "2018-09-03",
            "spReference": "2fce9449-44c2-4b2d-9c8c-e8a50bacd77c",
            "spCustomerReference": "7dcb8a94-76b1-412b-a60a-0e8066fb6bf2",
            "coSubscriptionId": "f854141e-6f46-453a-9586-ef670153784c"
        },
        "population": "Test population"
    }
]
```

```$xslt
coID;Service Provider: name;Service Provider: referenceID;Address: accessID;Address: Street Name;Address: Street Number;Address: Street Littera;Address: Postal Code;Address: City;Address: Apartment number;Address: Apartment address;Address: Apartment outlet;Service: Service Name;Service: Connection Date;Service: Disconnection Date;Invoice: List price;Invoice: Billing Item;Invoice: Row Type;Invoice: From Date;Invoice: To Date;Invoice: Credit amount;Invoice: Invoiced amount;Population;SP: SubscriptionID;Customer: name
Somecity-net;Acme;Acme;5d014d56-e86e-4ffc-bdaf-4aaab9a4f4f1;Some street;6;A;12345;Somecity;1012;apartment 15;ABC123;Acme 100/10;2018-09-03;2018-09-03;0;Acme 100/10;Periodic Fee;2018-09-03;2018-09-03;0;0;Test population;ea3d28c0-8ab5-4c2b-81c1-4ec9f57fc3e3;
Somecity-net;Acme;Acme;2fce9449-44c2-4b2d-9c8c-e8a50bacd77c;Some street;7;;12345;Somecity;;;;Acme 100/10;2018-09-03;2018-09-03;0;Acme 100/10;Periodic Fee;2018-09-03;2018-09-03;0;0;Test population;f854141e-6f46-453a-9586-ef670153784c;
```