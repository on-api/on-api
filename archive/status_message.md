# Status Message API

## Listes changes on orders and Subscriptions


<h3>Description</h3>

CO = Communication Operator<br>
SP = Service Provider<br>
NO = Network Owner<br>

<h4>Request </h4>
0-N of the fields listed below is needed to get a list of StatusMessages<br>

<table>
    <tbody>
        <tr>
            <td><strong>Field</td>            
            <td><strong>Type</td>            
            <td><strong>Description</td>
        </tr>
        <tr>
            <td>orderId</td>            
            <td>string 1-36</td>            
            <td>Unique identifyer for a Order, owned by CO</td>
        </tr>
        <tr>
            <td>subscriptionId</td>            
            <td>string 1-36</td>            
            <td>Unique identifyer for a Subscription, owned by CO</td>
        </tr>
        <tr>
            <td>accessId</td>            
            <td>string 1-32</td>            
            <td>Unique identifyer for a Access, owned by CO</td>
        </tr>
        <tr>
            <td>fromDateTime</td>            
            <td>dateTime</td>            
            <td>Gets all StatusMessages from this point in time</td>
        </tr>
        <tr>
            <td>toDateTime</td>            
            <td>dateTime</td>            
            <td>Gets all StatusMessages to this point in time</td>
        </tr>
        <tr>
            <td>fromStatusMessageID</td>            
            <td>int64</td>            
            <td>Gets all StatusMessages after this StatusMessageId</td>
        </tr>
        <tr>
            <td>toStatusMessageID</td>            
            <td>int64</td>            
            <td>Gets all StatusMessages before this StatusMessageId</td>
        </tr>
        <tr>
            <td>macAddress</td>            
            <td>string 12-17</td>            
            <td>Gets all StatusMessages for the specifyed Mac-address</td>
        </tr>
    </tbody>
</table>
                       
              
<h4>Response</h4>
0-N StatusMessages and Response code is returned<br>
StatusMessage<br>

<table>
    <tbody>
        <tr>
            <td><strong>Field</td>            
            <td><strong>Type</td>            
            <td><strong>Description</td>
        </tr>
        <tr>
            <td>statusMessageID</td>     
            <td>int64</td>    
            <td>Then idintifyer of the StatusMessage (used when syncing StatusMessages incremental)</td>
        </tr>
            <tr>messageDate</td>         
            <tr>dateTime</td>        
            <tr>When the event took place</td>
        </tr>
        <tr>
            <td>messageCode</td>         
            <td>int</td>             
            <td>ON-API generic message code</td>
        </tr>
        <tr>
            <td>messageParameters</td>   
            <td>list 0-N</td>        
            <td>ON-API generic key value list of parameters, including "Delivery date"</td>
        </tr>
        <tr>
            <td>orderId</td>             
            <td>string 1-36</td>     
            <td>Unique identifyer for a Order, owned by CO</td>
        </tr>
        <tr>
            <td>subscriptionId</td>      
            <td>string 1-36</td>     
            <td>Unique identifyer for a Subscription, owned by CO</td>
        </tr>
        <tr>
            <td>accessId</td>         
            <td>string 1-32</td>     
            <td>Unique identifyer for a Access, owned by CO</td>
        </tr>
        <tr>
            <td>macAddress</td>           
            <td>List</td>             
            <td>list of string 12-17, mac-address used by the service</td>
        </tr>
        <tr>
            <td>dhcpOption</td>           
            <td>DhcpOption</td>       
            <td>Class with DHCP options for IPv4: optoin82.remoteId, option82.circuitId and IPv6: option18 (interfaceID),  option37 (remoteID)</td> 
        </tr>
    </tbody>
</table> 


<t4>MessageTypes (This needs further discussion)</t4>
101     Created
102     Pending
103     NeedApproval
104     Approved
105     ErrorActivation
106     Activated
107     IPDepleted
108     AwaitingTermination
109     Terminated
110     Delayed
...     ...
...     ...


<t4>Example</b4> 

Request:
```http
POST /api/2.3/orders/ HTTP/1.1
Content-Type: application/json

{
    "spReference": "0656c2f0-731a-11e8-adc0-fa7ae01bbebc"
}
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

"StatusMessages": [   
    {   
        "statusMessageID": "1000023424553123",
        "messageDate": "2018-06-17T14:50:10.033",
        "messageCode": "101",
        "messageParameters": [
            {
            "Delivery date": "2018-06-17"
            }
        ],
        "orderId": "O10000004234345"
        "subscriptionId": "S100943053344"
        "accessId": "A100003453455"
        "dhcpOption"  
        {
            "IPv4"
            {
                "option82"
                {
                    "circuitId": "A100003453455"
                }
            }
        }
    },

    {   
        "statusMessageID": "100002342455554",
        "messageDate": "2018-06-17T14:58:12.043",
        "messageCode": "110",
        "messageParameters": [
            {
            "Delivery date": "2018-06-18"
            }
        ],
        "orderId": "O10000004234345"
        "subscriptionId": "S100943053344"
        "accessId": "A100003453455"
        "dhcpOption"  
        {
            "IPv4"
            {
                "option82"
                {
                    "remoteId": "KS_A001:Gi0/014"
                    "circuitId": "A100003453455"
                }
            }
        }
    },

    {   
        "statusMessageID": "100002342455554",
        "messageDate": "2018-06-17T16:05:41.201",
        "messageCode": "106",
        "messageParameters": [
            {
            "Delivery date": "2018-06-18"
            }
        ],
        "orderId": "O10000004234345"
        "subscriptionId": "S100943053344"
        "accessId": "A100003453455"
        "macAddress": [ 
                "fe:00:ae:35:44:ac",
                "oc:be:65:40:20:de"
            ],
        "dhcpOption"  
        {
            "IPv4"
            {
                "option82"
                {
                    "remoteId": "KS_A001:Gi0/014"
                    "circuitId": "A100003453455"
                }
            }
        }
    },

    {   
        "statusMessageID": "100002342455554",
        "messageDate": "2018-06-19T23:01:20.105",
        "messageCode": "109",
        "subscriptionId": "S100943053344"
        "accessId": "A100003453455"
    }
]
```
