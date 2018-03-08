# Fault Management: Link Status API

Link Status API används för felsökning av tjänster. Det erbjuder aktuell information of kunds länk i access-switch/router.

### Exempel

Anrop:

```http
GET /api/2.3/accesses/STTA0001/link HTTP/1.1
```

Svar när länken är uppe:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"link": "UP",
	"up": {
		"since": "2014-08-14T14:09:23Z",
		"mbps": 1000,
		"clients": [
			{
				"mac": "DE:AD:BE:EF:00:01",
				"ip": "10.10.1.181"
			}
		]
	}
}
```

Svar när länken är nere:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"link": "DOWN"
}
```

## Fältbeskrivningar

* `null` eller `""` är inte ett giltiga värden för något fält.

<table>
    <tbody>
        <tr>
            <td><strong>Fält</strong></td>
            <td><strong>Förklaring</strong></td>
        </tr>
	<tr>
            <td>
                <code>link</code>
            </td>
            <td>
	    	Anger status på länken.<br>
		Giltiga värden är "UP" och "DOWN".
            </td>
        </tr>
	<tr>
            <td>
                <code>up</code>
            </td>
            <td>
	    	Innehåller information om länken, förutsatt att den är uppe.<br>
		Noden skall enbart finnas när link = "UP".
            </td>
        </tr>
 	<tr>
            <td>
                <code>up / since</code>
            </td>
            <td>
                Anger tidpunkt då porten gick up och sedan när den haft länk<br>
		Formatet är "YYYY-MM-DDThh:mm:ssZ" enligt ISO-8601.<br>
		Avslutande "Z" innebär att tiden alltid är i UTC.
            </td>
        </tr>
        <tr>
            <td>
                <code>up / mbps</code>
            </td>
            <td>
	    	Anger länkens faktiskta länkhastighet.<br>
		Enheten är mbps, giltiga värden är: 10, 100, 1000.
            </td>
        </tr>
	<tr>
            <td>
                <code>up / clients</code>
            </td>
            <td>
	    	Lista som innehåller de enheter som finns på porten.
            </td>
        </tr>
        <tr>
            <td>
                <code>up / clients / mac</code>
            </td>
            <td>
            	MAC-adress på enheten.<br>
		MAC-adressen representeras genom 6 par av hexadecimala siffror konkatenerade med kolon ':'. Den skall utelstutande vara i uppercase.<br>
		MAC-adressen är alltid exakt 17 tecken lång.<br>
		Exempel: "DE:AD:BE:EF:00:01".  
	    </td>
        </tr>
        <tr>
            <td>
                <code>up / clients / ip</code>
            </td>
            <td>
	    	Tilldelad IPv4-adress på enheten.<br>
		IP-adress representeras som fyra decimala tal mellan 0 och 255 konkatenerade med punkter'.'.<br>
		Noden skall enbart finnas när enheten har en ipv4-adress.<br>
		Exempel: "10.101.1.181".
            </td>
        </tr>
     </tbody>
</table>
