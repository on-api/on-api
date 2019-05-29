# Webportal API
HTTPS-redirect to SP-page for further order managment and handling at SP side of things when unable or unwilling to use the OrderNotification style api.


### General redirect to SP homepage
## Example
```https
GET https://telia.se/ko?mac=00:11:22:33:44:55&reference=asdf-1234-qwer-zxcv
```

## Parameters:
| field       | mandatory   | description                                                             |
|-------------|-------------|-------------------------------------------------------------------------|
| `mac`       | *optional*  | mac-address of connected customer-device (for pre-seating if relevant)  |
| `accessId`  | *mandatory* | KO accessID                                                             |
| `reference` | *optional*  | SP reference for current order. Gotten from the order-notification API. |

## Additional information
Adress-data should be synched via availability/feasibility-api. Additional billing-address to be managed by SP.
