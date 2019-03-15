# Data formats
Within this document the conventions and formatting rules for all ON-API's are found. There are also descriptions of 
various data formats that are common for several API-endpoints. 

## Conventions and formatting

All use of the ON-API is expecting formatting to be according to these rules.

Personal data should not be entered as any value unless the data format is specifically intended for this. 

Valid JSON values is expected.
 
[ECMA-404 JSON Data Interchange format](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

A JSON value can be an object, array, number, string, true, false, or null.

All string values is encoded in UTF-8.

## Generic data formats

Basic guidelines for all other data formats. All specific data formats should refer to one of the following generic data
formats or a JSON value.

### ID
Used to identify a single object.

 * JSON string
 * Can not contain a personal identity number
 * Must be unique for the object type in the source system
 * Valid characters a-z, A-Z, 0-9, '-' and '.'
 * Maximum length 32 characters
 * Minimum length 1 characters
 * Matching regular expression ^[-0-9a-zA-Z]{1,32}$

Examples
 * 12345
 * ADA134312
 * 79bd7c5132cd40ea8470f91e18484962

### text
Human readable text string.

 * JSON string
 * Human readable characters
 * Max length 255

Examples
 * Internet access is blocked due to non payment.
 * A agreement with the network operator is required.
 * Data in the field service is invalid!
    
### boolean
Value that describes if a statement is true or false, this is not to be enclosed in double quotes in JSON representation.

 * JSON values true or false
 
Examples
 * true
 * false
  
### enumeration
A predefined list of values that is valid for this field is provided where it is defined. No other values can be used.

 * JSON type string
 
### object
A field with a value containing zero or more fields and values. Documentation should specify the structure of that 
object.

 * JSON type object

Examples 

 * { "field": "Some value", "otherField": "Another value" }

 
### array
A list of values or objects. Documentation should specify the type of values in the list.

  * JSON type array

Examples
 * [ "First", "Second", "Third" ]
  

## Specific data formats

### phoneNo

Phone numbers should always follow the E.164 conventions and consist of a +-sign followed by digits only. Incl country 
code such as 46 for Sweden and 1 for US/Canada.

 * JSON string
 * Follow the E.164 conventions
 * Start with a + sign
 * Includes country code such as 46 for Sweden and 1 for US/Canada
 * Matching regular expression ^\+[0-9]+$
 
Examples

 * +468214930

References
 * [Wikipedia E.164](https://en.wikipedia.org/wiki/E.164)

### option82

DHCPv4 Option82 should be hex encoded. The complete option82 TLV (typ, length, value) should be encoded. The data 
should always start with 52 which is hex for 82.
This format is deprecated in favor dhcpIdentifier.

 * Data format json string 
 * [RFC 3046](https://www.ietf.org/rfc/rfc3046.txt)

Examples
 
 * 520A01036162630203313233

### dhcpIdentifier
To better accommodate all scenarios the separate sub-options of DHCP option 82 have been split up and
also options for DHCPv6 have been added. The values is expected to have a readable text representation.
 
This replaces the old hex encoded option82 data format.

 * JSON object
 * Readable text representation of the value
 * Replaces data format [option82](dataformats.md#option82)
 * Fields with unknown or missing value is omitted
 * Fields
   * ipv4CircuitId
     * Data format json string
     * DHCP option 82 sub-option 1
     * [RFC 3046](https://www.ietf.org/rfc/rfc3046.txt)
   * ipv4RemoteId
     * Data format json string
     * DHCP option 82 sub-option 2
     * [RFC 3046](https://www.ietf.org/rfc/rfc3046.txt)
   * ipv6InterfaceId
     * Data format json string
     * DHCPv6 option 18
     * [RFC 3315](https://tools.ietf.org/html/rfc3315)
   * ipv6RemoteId
     * Data format json string
     * DHCPv6 option 37
     * [RFC 4649](https://tools.ietf.org/html/rfc4649)

Examples
```JSON
{
  "ipv4CircuitId": "ABC",
  "ipv4RemoteId": "EquipmentName",
  "ipv6InterfaceId": "ABC",
  "ipv6RemoteId": "ABC"
}
```

```JSON
{
  "ipv4CircuitId": "CO-1234"
}
```

### postalCode
 * Must be 5 digits
 * Matching regular expression ^[1-9][0-9]{4}$

### countryCode
 * According to ISO 3166-1 alpha-2 standard
 * Matching regular expression ^[A-Z]{2}$

References 
 * [Wikipedia ISO_3166-1_alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)
 

### ipAddress
Textual representation of either an IPv4 or IPv6 address with an optional netmask.

 * JSON string
 * Textual representation of IPv4 or IPv6 address
 * May contain a netmask denoted by "/[number]"
 * Without netmask single IP is assumed

Examples
 * 192.168.0.0/24
 * 192.168.10.5
 * ::ffff:c0a8:0/24
 * 2001:2::/48

References
 * [RFC 5952](https://tools.ietf.org/html/rfc5952)
 
### dateTime
Date and time according to ISO-8601 RFC-3339 in UTC time zone with up to 4 decimal places on seconds.

 * JSON string
 * ISO-8601 compliant
 * According to RFC-3339
 * Up to 4 decimal places on seconds 

Examples
 * 1985-04-12T23:20:50.52Z
 * 1985-04-12T23:20:50.0053Z
 * 1990-12-31T23:59:60Z

### date
Date according to ISO-8601 and RFC-3339 

 * ISO-8601 compliant
 * RFC-3339 compliant

Examples 
 * 2019-01-18
 
References
 * [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt)

### hexBinary
 * JSON string
 * Hexadecimal representation of a binary value
 
Examples
 * 7465737420737472696E67

### macAddress
 * JSON string
 * Formatted as 12 hexadecimal digits with a colon (":") as a separator every third character
 * Digits A to F should use capital letters
 * Matching regular expression ^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$

Examples
 * 01:02:03:04:05:06
 * AA:BB:CC:DD:EE:FF

### accessId

Identifies a single access. Used as key when fetching a single access or when ordering services.

 * Data format: [ID](dataformats.md#id)
 * References: [accesses/accessId](accesses.md#accessid)


### subscriptionId
 The CO's ID for a single subscription. 

 * Data format: [ID](dataformats.md#id)
 * References: [subscriptions/subscriptionId](subscriptions.md#subscriptionid)

 
### spReference

Reference that identifies the unique end-customer or service in the Service Provider's system.
This information can be used by the CO to lookup information about the customer or service with the 
[contacts API](contacts.md)

 * Data format: [ID](dataformats.md#id)

### spSubscriptionId

The service providers ID for a single subscription.

 * Data format: [ID](dataformats.md#id)
 
### operationalState 

The operational state of a subscription

 * Data format: [enumeration](dataformats.md#enumeration)

**Values**
  * ACTIVATED
    * Subscription is activated and service delivery is enabled
  * SUSPENDED
    * Subscription is suspended and service delivery is blocked

### service
A name of a specific service offered by the CO listed in the [accesses API](accesses.md)

 * Data format: [text](dataformats.md#text)


### equipment

List of equipment which is used to deliver a service. This can be used to tie the service to specific 
equipment, such as VOIP or IPTV-equipment. 

 * Data format: JSON array of JSON objects

**Keys**
 * vendorId
   * Data format: text
   * Specifies the DHCP Option 60 Vendor class identifier 
   * See [RFC 2132](https://www.ietf.org/rfc/rfc2132.txt)

 * macAddress
   * Data format: [macAddress](dataformats.md#macaddress)
   * Specifies the equipments MAC-address

Examples

```JSON
[
    {
      "vendorId": "ACME-IPTV",
      "macAddress": "AA:BB:CC:11:22:33"
    },
    {
      "vendorId": "ACME-IPTV",
      "macAddress": "AA:BB:CC:44:55:66"
    }
]
```


### characteristics
Settings for a subscription.

 * Data format: JSON object

#### characteristics/fixedIp
Indicates if a fixedIp is to be used. 

Data format: [boolean](dataformats.md#boolean)

#### characteristics/ipAddresses
If the ipAddresses characteristic is provided in an [order](orders.md) the specified IP-addresses will be 
used. If ipAddresses is omitted from the [order](orders.md) the CO reserves an IP-address from a predefined pool, the 
IP-addresses is later displayed under characteristics in the [subscriptions API](subscriptions.md).

Data format: JSON-array of [IP-addresses](dataformats.md#ipaddress) to be used.

```JSON
{
    "characteristics": {
        "fixedIp": true,
        "ipAddresses": [
            "1.2.3.4",
            "AB::01/64",
            "1.3.0.1/24"
        ]
    }
}
```

#### characteristics/SLA
SLA type to be used for the service. 

Data format: [text](dataformats.md#text)

```JSON
{
    "characteristics": {
        "SLA": "SLA-3"
    }
}
