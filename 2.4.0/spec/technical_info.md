# Technical Info API

### Description

The information communicated is intended for troubleshooting purposes and is sourced from network elements.

Technical decisions and data structure design are taken with regards to network element resource utilization, and to promote programmatic decision making. 

Information should be sanitized or formatted in regard to keep data as raw as possible, but enabling a standardized way to communicate this data. For example converting timestamps in an unified manner, or translating vlan tags to service names.

Data communicated should only be related to its troubleshooting purpose or context.

Example service types:

| Name   | Description      |
|--------|------------------|
| bb     | Internet         |
| iptv   | Tv               |
| voip   | Voip             |
| unknown| Unknown service  |


# Specification
## Reference index
### access
* GET [access/{accessId}/hardware](#get-access-hardware)
* GET [access/{accessId}/link/macaddresstable](#get-access-link-macaddresstable)
* GET [access/{accessId}/link/leaseinfo](#get-access-link-leaseinfo)
* GET [access/{accessId}/link/igmpsnooping](#get-access-link-igmpsnooping)
* GET [access/{accessId}/link/status](#get-access-link-status)

### cpe
* GET [cpe/{accessId}/status](#get-cpe-status)

## Requirements


**API Prefix:** `/tech` 
eg: `domain.local/api/2.4/tech/access/equipment/423323449`

Endpoints like leaseinfo should when empty return an empty array:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[]
```




## Parameters

| Parameter  | Data format |
|------------|-------------|
| accessId   | accessId    |

## Endpoints

<h3 id="get-access-hardware">GET access/{accessId}/hardware</h3>
Returns information about the customer-facing network element, eg. access switch.

Request:
```http
GET /api/2.4/tech/{accessId}/access/hardware
```

Response when the network element is working as intended:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "up": true,
  "upSince": "2004-08-14T14:09:23Z",
  "vendor": "Huawei",
  "model": "S5320+"
}
```
Response when network element or eg. management interface is unavailable:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "up": false
}
```
| Parameter | Type              | Description                                                       |
|-----------|-------------------|-------------------------------------------------------------------|
|up         | bool              | Status of network element, eg. pingable/management is reachable   |
|upSince    | string (iso8601)  | Timestamp when hardware was started                               |
|vendor     | string            | Hardware vendor                                                   |
|model      | string            | Hardware model                                                    |

<h3 id="get-access-link-macaddresstable">GET access/{accessId}/link/macaddresstable</h3>

Fetch mac address table data from only the access interface.

Request:
```http
GET /api/2.4/tech/access/{accessId}/link/macaddresstable
```


Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "mac": "00:11:22:aa:bb:cc",
    "serviceType": "bb"
  },
  {
    "mac": "00:11:22:aa:bb:cc",
    "serviceType": "iptv"
  }
]
```

| Parameter | Type        | Description                                     |
|-----------|-------------|-------------------------------------------------|
| mac       | string (17) | Mac address of device                           |
| serviceType   | string      | Which network service the mac originates from   |

<h3 id="get-access-link-leaseinfo">GET access/{accessId}/link/leaseinfo</h3>

Fetch lease data from the access interface.

Request:
```http
GET /api/2.4/tech/access/{accessId}/link/leaseinfo
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "lease": "10.0.0.1",
    "mac": "00:00:00:00:00:00",
    "serviceType": "iptv",
    "start": "2004-08-14T14:09:23Z",
    "end": "2004-08-14T14:09:23Z"
  },
  {
    "lease": "10.0.0.1",
    "mac": "00:00:00:00:00:00",
    "serviceType": "iptv",
    "start": "2004-08-14T14:09:23Z",
    "end": "2004-08-14T14:09:23Z"
  }
]
```

|Parameter|Type|Description|
|--|--|--|
|lease|ip|ip address|
|mac|mac|mac address|
|serviceType|serviceType|Service type for lease|
|start|timestamp|Starting timestamp of lease|
|end|timestamp|End timestamp of lease|


<h3 id="get-access-link-igmpsnooping">GET access/{accessId}/link/igmpsnooping</h3>

Fetch igmp snooping data from only the access interface.

Request:
```http
GET /api/2.4/tech/access/{accessId}/link/igmpsnooping/
```
Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "multicast": "233.10.10.100",
    "timestamp": "2004-08-14T14:09:23Z",
    "counter": 231231
  },
  {
    "multicast": "233.10.10.100",
    "timestamp": "2004-08-14T14:09:23Z",
    "counter": 231231
  }
]
```
| Parameter  | Type             | Description                            |
|------------|------------------|----------------------------------------|
| multicast  | string (7-19)    | Multicast address                      |
| timestamp| string (iso8601) | Timestamp when latest join was sent|
| counter    | integer          | Traffic counter                        |



<h3 id="get-access-link-status">GET access/{accessId}/link/status</h3>

Fetch access equipment access interface status.

Request:
```http
GET /api/2.4/tech/access/{accessId}/link/status
```
Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "link": true,
  "fullDuplex": true,
  "linkSince": "2014-08-14T14:09:23Z",
  "speed": "auto",
  "linkSpeed": 1000,
  "configuredSpeed": [
    {
      "serviceType": "bb",
      "queue": 1,
      "cir": 3000,
      "pir": 3000
    },
    {
      "serviceType": "iptv",
      "queue": 0,
      "cir": 12000,
      "pir": 12000
    }
  ],
  "statistics": {
    "counterResetAt": "2014-08-14T14:09:23Z",
    "peakInputRate": {
      "counter": 30000,
      "timestamp": "2014-08-14T14:09:23Z"
    },
    "peakOutputRate": {
      "counter": 30000,
      "timestamp": "2014-08-14T14:09:23Z"
    },
    "lastFiveInput": { 
      "packets": 100,
      "bytes": 10000,
    },
    "lastFiveOutput": {
      "packets": 100,
      "bytes": 10000,
    },
    "input": {
      "packets": 100,
      "bytes": 1000,
      "unicast": 100,
      "broadcast": 100,
      "multicast": 100,
      "pauses": 0,
      "errors": 1337,
      "crcErrors": 0
    },
    "output": {
      "packets": 100,
      "bytes": 1000,
      "unicast": 100,
      "broadcast": 100,
      "multicast": 100,
      "pauses": 0,
      "errors": 1337,
      "crcErrors": 0
    }
  },
  "fiber": {
    "dbmRx": "-12",
    "dbmTx": "-8",
    "temp": "35"
  },
}
```
| Parameter                                     | Type              | Description                                      |
|-----------------------------------------------|-------------------|--------------------------------------------------|
| link                                          | bool              | Physical link status                             |
| fullDuplex                                    | bool              | If interface is set to full duplex               |
| linkSince                                     | string (iso8601)  | Timestamp when port changed status               |
| speed                                         | string            | Configured speed                                 |
| linkSpeed                                     | integer           | Link speed                                       |
| configuredSpeed                               | list              | List of configured traffic shaping/policies      |
| configuredSpeed.#.serviceType                     | string            | Service type                                     |
| configuredSpeed.#.queue                       | string            | Queue index                                      |
| configuredSpeed.#.cir                         | string            | Committed rate                                    |
| configuredSpeed.#.pir                         | string            | Peak rate                                        |
| statistics.counterResetAt                     | string (iso8601)  | Timestamp when statistics counter was started    |
| statistics.peakInputRate.counter                 | integer           | Bytes per second                                 |
| statistics.peakInputRate.timestamp                   | string (iso8601)  | Timestamp of peak                                |
| statistics.peakOutputRate.counter                | string            | Bytes per second                                 |
| statistics.peakOutputRate.timestamp|string (iso8601) | Timestamp of peak |                                                  |
| statistics.lastFiveInput.packets              | integer           | Ingress count of packets last five minutes       |
| statistics.lastFiveInput.bytes                | integer           | Ingress count of bytes last five minutes         |
| statistics.lastFiveOutput.packets             | integer           | Egress count of packets last five minutes        |
| statistics.lastFiveOutput.bytes               | integer           | Egress count of byes last five minutes           |
| statistics.input.packets                      | integer           | Ingress count of packets                         |
| statistics.input.bytes                        | integer           | Ingress count of bytes                           |
| statistics.input.unicast                      | integer           | Ingress count of unicast                         |
| statistics.input.broadcast                    | integer           | Ingress count of broadcast                       |
| statistics.input.multicast                    | integer           | Ingress count of multicast                       |
| statistics.input.pauses                       | integer           | Ingress count of pauses                          |
| statistics.input.errors                       | integer           | Ingress count of errors                          |
| statistics.input.crcErrors                    | integer           | Ingress count of crc errors                      |
| statistics.output.packets                     | integer           | Egress count of packets                          |
| statistics.output.bytes                       | integer           | Egress count of bytes                            |
| statistics.output.unicast                     | integer           | Egress count of unicast                          |
| statistics.output.broadcast                   | integer           | Egress count of broadcast                        |
| statistics.output.multicast                   | integer           | Egress count of multicast                        |
| statistics.output.pauses                      | integer           | Egress count of pauses                           |
| statistics.output.errors                      | integer           | Egress count of errors                           |
| statistics.output.crcErrors                   | integer           | Egress count of crc errors                       |
| fiber.dbmRx                                   | string            | Fiber receiver dampening                          |
| fiber.dbmTx                                   | string            | Fiber transceiver dampening                       | 
| fiber.temp                                    | string            | SFP temperature                                  |


<h3 id="get-cpe-status">GET cpe/{accessId}/status</h3>

Fetch full cpe state.

Request:
```http
GET /api/2.4/tech/cpe/{accessId}/status
```
Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "firmware": "abc123.123",
  "vendor": "inteno",
  "model": "xge365",
  "mac": "xx:xx:xx:xx:xx:xx",
  "up": true,
  "upSince": "2004-08-14T14:09:23Z",
  "ports": [
    {
      "index": 0,
      "ifDescription": "WAN",
      "name": "WAN sfp",
      "link": true,
      "fullDuplex": true,
      "changedAt": "2004-08-14T14:09:23Z",
      "loopDetectionStatus": "unlocked",
      "freeSeating": false,
      "configuredSpeed": "auto",
      "linkSpeed": 1000,
      "fiber": {
        "dbmRx": "-12",
        "dbmTx": "-8",
        "temp": "35"
      },
      "statistics": {
        "input": {
          "errors": 123,
          "crcErrors": 123,
          "bytes": 123,
          "multicast": 123,
          "unicast": 123,
        },
        "output": {
          "errors": 123,
          "crcErrors": 123,
          "bytes": 123,
          "multicast": 123,
          "unicast": 123,
        }
      }
    },
    {
      "index": 1,
      "ifDescription": "LAN1",
      "name": "LAN 1 (red)",
      "link": true,
      "fullDuplex": true,
      "changedAt": "2004-08-14T14:09:23Z",
      "loopDetectionStatus": "unlocked",
      "freeSeating": false,
      "configuredSpeed": "auto",
      "linkSpeed": 1000,
      "fiber": null,
      "statistics": {
        "input": {
          "errors": 123,
          "crcErrors": 123,
          "bytes": 123,
          "multicast": 123,
          "unicast": 123,
        },
        "output": {
          "errors": 123,
          "crcErrors": 123,
          "bytes": 123,
          "multicast": 123,
          "unicast": 123,
        }
      }
    }
  ],
  "macAddressTable": [
    {
      "mac": "xx:xx:xx:xx:xx:xx",
      "serviceType": "bb",
      "port": 1
    },
    {
      "mac": "xx:xx:xx:xx:xx:xx",
      "serviceType": "iptv",
      "port": 2
    }
  ],
  "dhcpSnooping": [
    {
      "ip:": "10.0.0.1",
      "mac": "00:11:22:aa:bb:cc",
      "serviceType": "iptv",
      "timeout": "2004-08-14T14:09:23Z",
    },
    {
      "ip:": "10.0.0.1",
      "mac": "00:11:22:aa:bb:cc",
      "serviceType": "iptv",
      "timeout": "2004-08-14T14:09:23Z",
    },
  ]
}
```

| Parameter                                     | Type              | Description                                      |
|-----------------------------------------------|-------------------|--------------------------------------------------|
|firmware                                       | string            | CPE firmware name                                |
| vendor                                        | string            | CPE vendor name                                  |
| model                                         | string            | CPE model name                                   |
| mac                                           | string            | CPE mgmt interface mac address                   |
| up                                            | bool              | Power status                                     |
| upSince                                       | string            | Uptime of CPE                                    |
| ports                                         | list              | List of port objects                             |
| ports.#.index                                 | integer           | Interface number                                 |
| ports.#.ifDescription                         | string            | Interface description                            |
| ports.#.name                                  | string            | Friendly interface name                          |
| ports.#.link                                  | bool              | duplex status                                    |
| ports.#.fullDuplex                            | bool              | duplex status                                    |
| ports.#.changedAt                             | string (iso8601)  | Timestamp when port changed state                |
| ports.#.loopDetectionStatus                   | string            | Loop detection status                            | 
| ports.#.freeSeating                           | bool              | Free seating status                              | 
| ports.#.configuredSpeed                       | string            | Configured speed                                 |
| ports.#.linkSpeed                             | integer           | Link speed                                       |
| ports.#.fiber.dbmRx                           | string            | Fiber receive dampening                          |
| ports.#.fiber.dbmTx                           | string            | Fiber transceiver dampening                       |
| ports.#.fiber.temp                            | string            | SFP temperature                                  |
| ports.#.fiber.biasTx                          | string            | SFP TX bias current                              |
| ports.#.fiber.supplyVoltage                   | string            | SFP Supply voltage                               |
| ports.#.fiber.vendor                          | string            | SFP Vendor                                       |
| ports.#.fiber.partNumber                      | string            | SFP Part Number                                  |
| ports.#.fiber.serialNumber                    | string            | SFP Serial Number                                |
| ports.#.statistics.input.errors               | integer           | Ingress count of total errors                    |
| ports.#.statistics.input.crcErrors            | integer           | Ingress count of crc errors                      |
| ports.#.statistics.input.pause                | integer           | Ingress count of pause frames                    |
| ports.#.statistics.input.bytes                | integer           | Ingress count of total bytes                     |
| ports.#.statistics.input.multicast            | integer           | Ingress count of multicast bytes                 |
| ports.#.statistics.input.unicast              | integer           | Ingress count of unicast bytes                   |
| ports.#.statistics.input.packets              | integer           | Ingress count of total packets                   |
| ports.#.statistics.input.multicastPackets     | integer           | Ingress count of multicast packets               |
| ports.#.statistics.input.unicastPackets       | integer           | Ingress count of unicast packets                 |
| ports.#.statistics.output.errors              | integer           | Egress count of total errors                     |
| ports.#.statistics.output.crcErrors           | integer           | Egress count of crc errors                       |
| ports.#.statistics.output.pause               | integer           | Egress count of pause frames                     |
| ports.#.statistics.output.bytes               | integer           | Egress count of total bytes                      |
| ports.#.statistics.output.multicast           | integer           | Egress count of multicast bytes                  |
| ports.#.statistics.output.unicast             | integer           | Egress count of unicast bytes                    |
| ports.#.statistics.output.packets             | integer           | Egress count of total packets                    |
| ports.#.statistics.output.multicastPackets    | integer           | Egress count of multicast packets                |
| ports.#.statistics.output.unicastPackets      | integer           | Egress count of unicast packets                  |
| macAddressTable                               |list               | List of mac address objects                      |
| macAddressTable.#.mac                         |string             | Mac address of device                            |
| macAddressTable.#.serviceType                     |string             | Which network service the mac originates from    |
| macAddressTable.#.port                        |string             | Which CPE port index the mac originates from     |
| dhcpSnooping                                  |list               | List of dhcp snooping objects                    |
| dhcpSnooping.#.ip                             |string             | IP lease                                         |
| dhcpSnooping.#.mac                            |string             | Mac address of device                            |
| dhcpSnooping.#.serviceType                        |string             | Which network service the lease originates from  |
| dhcpSnooping.#.timeout                        |string (iso8601)   | DHCP Lease timeout                               |
