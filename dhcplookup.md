# DHCP lookup
path /2.4/dhcplookup/

## Operations

### GET

Look up an access with values from DHCP logs, returns a single accessId if a unique access can be found. 

### Parameters 

   * ipv4CircuitId
     * DHCP option 82 sub-option 1
   * ipv4RemoteId
     * DHCP option 82 sub-option 2
   * ipv6InterfaceId
     * DHCPv6 option 18
   * ipv6RemoteId
     * DHCPv6 option 37
   * ipv4option82
     * Data format: option82

Request:
```HTTP
GET /api/2.4/dhcplookup/?ipv4circuitid=ABC123&ipv4remoteid=XYZ HTTP/1.1
```

Response:

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json

{
    "accessId": "96bd5353f0854cb4a18457d9b5f66d4b"
}
```

### Fields

 #### accessId
 * Data format: [accessId](dataformats.md#accessid)