# Conventions and formatting

All use of the on-api is expecting formatting to be according to these rules.

Valid JSON values is expected.
 
[ECMA-404 JSON Data Interchange format](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

A JSON value can be an object, array, number, string, true, false, or null.

All string values is encoded in UTF-8.

## Data types

### ID
Used to identify a single object.

 * JSON string
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
 
### number
Decimal number 
 * Matching regular expression ^[0-9]+$

Examples
 * Internet access is blocked due to non payment.
 * A agreement with the network operator is required.
 * Data in the field service is invalid!

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

 * Data format hexBinary
 
Examples
 
 * 520A01036162630203313233

### dhcpIdentifier
 * JSON object
 * Fields with unknown or missing value is omitted
 * Fields
   * ipv4CircuitId
     * DHCP option 82 suboption 1
   * ipv4RemoteId
     * DHCP option 82 suboption 2
   * ipv6InterfaceId
     * DHCPv6 option 18
   * ipv6RemoteId
     * DHCPv6 option 37

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
 * 1985-04-12T23:20:50,52Z
 * 1985-04-12T23:20:50,0053Z
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
    
### boolean
Value that describes if a statement is true or false, this is not to be enclosed in double quotes in JSON representation.

 * JSON values true or false
 
Examples
 * true
 * false
  
### enumeration
 * JSON type string
 
 A predefined list of values that is possible for this field is provided where it is defined. No other values can be 
 used.
 
### object
 A field with a value containing zero or more fields and values. Documentation should specify the structure of that 
 object.

 * JSON type object

Examples 
 * { "Field": "Some value", "Other field": "Another value" }

 
### array
A list of values or objects. Documentation should specify the type of values in the list.

  * JSON type array

Examples
 * [ "First", "Second", "Third" ]
  
### mac-address
 * JSON string
 * Formatted as 12 hexadecimal digits with a colon (":") as a separator every third character
 * Digits A to F should use capital letters
 * Matching regular expression ^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$

Examples
 * 01:02:03:04:05:06
 * AA:BB:CC:DD:EE:FF