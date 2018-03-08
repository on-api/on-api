# Feasibility API

Feasibility API används av Tjänsteleverantör för att kunna hitta avlämningspunkter och svara på om en fastighet/lägenhet är inkopplad i ett nät. Tjänsteleverantör ser även vilken teknisk kapacitet varje access har genom de tekniska tjänster som är definierade på accessen.

## Exempel

Request:
```http
GET /api/2.3/accesses/ HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Last-Modified: Fri, 31 Aug 2012 12:03:28 GMT
Content-Type: application/json
[
    {
        "accessId": "STTA0001",
        "streetName": "Testvägen",
        "streetNumber": "100",
        "streetLittera": "",
        "postalCode": "10000",
        "city": "Ankeborg",
        "countryCode": "SE",
        "premisesType": "MDU_APARTMENT",
        "mduApartmentNumber": "1001",
        "mduDistinguisher": "12121212",
        "outlet": "A-11-14",
        "population": "Hemsöhem",
        "services": [
            {
                "service": "BB-100-100",
                "connection": "2014-03-01"
            }, {
                "service": "BB-100-10",
                "connection": "2013-10-12"
            }, {
                "service": "BB-10-10",
                "connection": "2013-10-12"
            }, {
                "service": "IPTV",
                "connection": "2013-10-12"
            }, {
                "service": "VOIP",
                "connection": "2013-08-13"
            }
        ],
        "coFiberConverter": "LASER_3001X_MK2",
        "coCpeSwitch": "",
        "coCpeRouter": "NETGEAR WNDR4000"
    }
]
```

## Fältbeskrivningar

* `null` är inte ett giltigt värde för något fält.
* Fält markerade med _obligatoriskt_ får inte vara tomma strängen (`""`)

<table>
    <tbody>
        <tr>
            <td><strong>Fält</strong></td>
            <td><strong>Förklaring</strong></td>
        </tr>
        <tr>
            <td>
                <code>accessId</code>
            </td>
            <td>
                Ett, per kommunikationsoperatör, unikt ID på en access.<br>Får enbart bestå av tecknen a-z, A-Z, 0-9, '-' och '.'. <em>text, obligatoriskt, max 32 tecken, [a-zA-Z0-9-.]+</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>streetName</code>
            </td>
            <td>
                Gatunamn.<br> I fallet "Kungsgatan 10G" är StreetName "Kungsgatan". <em>text, obligatoriskt</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>streetNumber</code>
            </td>
            <td>
                Gatunummer.<br> I fallet "Kungsgatan 10G" är StreetNumber "10". I fallet "Lantvägen 550-70" är StreetNumber "550". Enbart siffror. <em>text</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>streetLittera</code>
            </td>
            <td>
                Gatubokstav/Uppgång.<br> I fallet "Kungsgatan 10G" är StreetLittera "G". I fallet "Lantvägen 550-70" är StreetLittera "70". <em>text</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>postalCode</code>
            </td>
            <td>
                Postnummer. Exempelvis "41369". Min 10000, max 99999. Alltid fem siffror. <em>text, obligatoriskt</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>city</code>
            </td>
            <td>
                Postort. Exempelvis "Göteborg". <em>text, obligatoriskt</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>countryCode</code>
            </td>
            <td>
                Landskod. Följer ISO 3166-1 för landskoder. Exempel: "SE" för Sverige. <em>text, ISO 3166-1, obligatoriskt</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>premisesType</code>
            </td>
            <td>
                PremisesType beskriver avlämningspunktens lokal. Vid MDU_APARTMENT och MDU_COMMON måste MduDistinguisher eller MduApartmentNumber vara populerade.<em>obligatoriskt</em>
<dl>
<dt>MDU_APARTMENT</dt><dd>Lägenhet i flerbostadshus. Delad fastighetsbeteckning.</dd>
<dt>MDU_COMMON</dt><dd>Gemensamt utrymme i flerbostadshus. Delad fastighetsbeteckning.</dd>
<dt>RESIDENTIAL_HOUSE</dt><dd>Bostad som har egen fastighetsbeteckning.</dd>
<dt>COMMERCIAL</dt><dd>Lokal, men utan tillträde från allmänheten. Till exempel ett kontor.</dd>
<dt>PUBLIC</dt><dd>Inrättning dit allmänheten har tillträde. Till exempel en restaurang eller ett gym.</dd>
<dt>UNKNOWN</dt><dd>Okänd.</dd>
</dl>
            </td>
        </tr>
        <tr>
            <td>
                <code>mduApartmentNumber</code>
            </td>
            <td>
								Lägenhetsnummer enligt Lantmäteriet. Används för att tillsammans med en adress identifiera en unik access. I fallet när kund vill beställa tjänster kan de inte aktiveras hos KO utan att TL har fastställt vilket AccessID kunden har. Genom att unikt identifiera lägenheten med mduApartmentNumber eller mduDistinguisher kan TL fastställa exakt vilken access som skall aktiveras. <em>text, 4 digits, obligatoriskt<sup>1</sup></em><br>
								<br>
								Exempel: 1101, 0901, 1201, 1213.<br>
								<br>
                [1] En av <code>mduApartmentNumber</code>, <code>mduDistinguisher</code> måste finnas om <code>premisesType</code> är <code>"MDU_APARTMENT"</code>.
            </td>
        </tr>
        <tr>
            <td>
                <code>mduDistinguisher</code>
            </td>
            <td>
                Alternativ lokalbeteckning som identifierar lägenheten unikt per adress. Behöver inte följa Lantmäteriets format. <em>text, obligatoriskt<sup>2</sup></em><br>
								<br>
								Exempel: 28, 65113, 1234-1919.<br>
								<br>
	              [2] En av <code>mduApartmentNumber</code>, <code>mduDistinguisher</code> måste finnas om <code>premisesType</code> är <code>"MDU_APARTMENT"</code>.
            </td>
        </tr>
        <tr>
            <td>
                <code>outlet</code>
            </td>
            <td>
                Uttagsnummer som identifierar porten i lägenhet/villa. Typiskt är porten hos slutkund märkt med uttagsnummer. Outlet behöver vara unikt per adress. <em>text</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>population</code>
            </td>
            <td>
                Anger delbestånd i hela beståndet. Hela beståndet hämtas alltid in, men det kan filtreras och göras säljbart i olika etapper. <em>text</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>services</code>
            </td>
            <td>
                Anger accessens tekniska tjänster och feasibility per teknisk tjänst. För beskrivning, se följande två rader i listan över fältbeskrivningar. <br/>
                Oavsett vilken Service Provider som hämtar feasibility-data skall services innehålla samma information.<br/>
                <em>obligatorisk</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>services / service</code>
            </td>
            <td>
                Id/namn på tekniskt tjänst som avses. Den tekniska tjänsten kan beställas via Service Activation API. <em>obligatorisk</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>services / connection</code>
            </td>
            <td>
                Anger när accessen kopplas in och den tekniska tjänsten blir aktiverbar första gången. På det angivna datumet, eller om connection är "YES", skall det gå att aktivera tjänster på accessen. <br/>
                Om tjänsten är aktiverbar men datumet är okänt kan "YES" användas för att indikera det. Datumet får tidigast vara 1970-01-01.<br/>
                <br/>
                <em>"YES", "NO" eller ISO-8601 datum (YYYY-MM-DD), obligatoriskt</em><br/>
                Exempel: YES, NO, 2012-07-01
            </td>
        </tr>
        <tr>
            <td>
                <code>coFiberConverter</code>
            </td>
            <td>
                Typ (tillverkare, modell) av Fiber Konverter Switch som "accessen" är kopplad till. Skall enbart användas för utrustning som KO tillhandahåller. <em>text</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>coCpeSwitch</code>
            </td>
            <td>
                Om CPEn är en Switch, är detta typen (tillverkare, modell) som är inkopplad. Enbart en av CpeSwitch och CpeRouter får finnas. Skall enbart användas för utrustning som KO tillhandahåller. <em>text</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>coCpeRouter</code>
            </td>
            <td>
                Om CPEn är en Router, är detta typen (tillverkare, modell) som är inkopplad. Enbart en av CpeSwitch och CpeRouter får finnas. Skall enbart användas för utrustning som KO tillhandahåller. <em>text</em>
            </td>
        </tr>
    </tbody>
</table>

## Begränsningsmekanism

If-Modified-Since används för att be om inkrementella uppdateringar av accesser. På det viset kan anropet ske ofta men fortfarande vara billigt.

Vid första anropet sker ingen begränsning. Då ber TL om fullständiga beståndet. Vid påföljande anrop används If-Modified-Since. Värdet för headern är föregående svars värde på Last-Modified.

Av den anledningen är "Last-Modified" obligatoriskt vid HTTP Status 200.

Se [RFC-2616][rfc2616-sec14]. Exemplen använder ingen autentisering.

```
If-Modified-Since = "If-Modified-Since" ":" HTTP-date
```

När en access förekommer i ett svar skall den alltid skickas i sin helhet: med accessens samtliga fält och tjänster.

## Begränsningsmekanism - Exempel

Exempel på anropssekvens:

Request:
```http
GET /api/2.3/accesses/ HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Last-Modified: Fri, 31 Aug 2012 12:03:28 GMT
Content-Type: application/json
...
```

Vid påföljande anrop skickas "If-Modified-Since"-header för att bara be om uppdaterade poster.

Request:
```http
GET /api/2.3/accesses/ HTTP/1.1
If-Modified-Since: Fri, 31 Aug 2012 12:03:28 GMT
...
```

Om det finns uppdaterade poster kan svaret se ut såhär:

Response:
```http
HTTP/1.1 200 OK
Last-Modified: Mon, 03 Sep 2012 09:54:55 GMT
Content-Type: application/json
...
```

Om det inte finns uppdaterade poster ser svaret istället ut såhär:

Response:
```http
HTTP/1.1 304 Not Modified
```

[rfc2616-sec14]: http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html "HTTP/1.1 RFC-2616 Section 14, Header Field Definitions"
