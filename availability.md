# Availability API

Availability ger samma information som Feasibility-API, men enbart för en access.
Dessutom svarar det med information som kan vara kostsammare att producera och av naturen behöver vara aktuell.
Typiskt används frågan för att kunna svara kund om vilka tekniska tjänster som är lediga, med hänsyn taget till andra tjänsteleverantörer.

### Exempel

Request:
```http
GET /api/2.3/accesses/STTA0001 HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

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
            "connection": "2014-03-01",
            "available": "2014-01-01",
            "forcedTakeoverPossible": false
        }, {
            "service": "BB-100-10",
            "connection": "2013-10-12",
            "available": "YES",
            "forcedTakeoverPossible": false
        }, {
            "service": "BB-10-10",
            "connection": "2013-10-12",
            "available": "YES",
            "forcedTakeoverPossible": false
        }, {
            "service": "IPTV",
            "connection": "2013-10-12",
            "available": "YES",
            "forcedTakeoverPossible": false
        }, {
            "service": "VOIP",
            "connection": "2013-08-13",
            "available": "NO",
            "forcedTakeoverPossible": true
        }
    ],
    "active": [
        {
            "service": "BB-100-10",
            "option82": "5216010765746820302F31020B31302E31302E31302E3130",
            "equipment": [
                { "vendorId" : "CH_BROADBAND" }
            ],
            "spReference": ""
        }, {
            "service": "IPTV",
            "option82": "5216010765746820302F32020B31302E31302E31302E3130",
            "equipment": [],
            "spReference": ""
        }
    ],
    "coFiberConverter": "LASER_3001X_MK2",
    "coCpeSwitch": "",
    "coCpeRouter": "NETGEAR WNDR4000"
}
```

## Fältbeskrivningar

Listan omfattar de fält som Availability definererar _utöver_ <a href="feasibility.md">Feasibility</a>.

* `null` är inte ett giltigt värde för något fält.
* Fält markerade med _obligatoriskt_ får inte vara tomma stängen (`""`)

<table>
    <tbody>
        <tr>
            <td><strong>Fält</strong></td>
            <td><strong>Förklaring</strong></td>
        </tr>
        <tr>
            <td>
                <code>services</code>
            </td>
            <td>
                Anger accessens tjänster och feasibility per tjänst. Se fält per tjänst nedan. <br/>
                Oavsett vilken Service Provider som hämtar feasibility-data skall services innehålla samma information.<br/>
                <em>obligatorisk</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>services / service</code>
            </td>
            <td>
                Id/namn på teknisk tjänst som avses. Den tekniska tjänsten kan beställas via Service Activation API. <em>obligatorisk</em>
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
                <code>services / available</code>
            </td>
            <td>
                Anger om/när teknisk tjänst är/blir tillgänglig för beställning och leverans.<br/>
                Om tjänsten inte är tillgänglig för beställning av anropande TL skall det indikeras med "NO" eller datum då tjänsten blir tillgänglig.
                <br/> Datumet får tidigast vara 1970-01-01.<br/>
                <br/>
                Innan tjänsten är tillgänglig första gången sammanfaller Available och Connection.<br/>
                <br/>
                <em>"YES", "NO" eller ISO-8601 datum (YYYY-MM-DD), obligatoriskt</em><br/>
                Exempel: YES, NO, 2012-07-01<br>
                Exempel: Anropande TL har BB 10/10 aktivt. BB 10/10, BB 100/100 kan beställas om BB 10/10 först avaktiveras. KO skall svara med available YES.<br>
                Exempel: Annan TL har BB 10/10 aktivt. BB 10/10, 100/100 skall svara med NO eller datum.
            </td>
        </tr>
        <tr>
            <td>
                <code>services / forcedTakeoverPossible</code>
            </td>
            <td>
                Anger om flaggan "force" i en beställning kommer att ha effekt.<br>
                Alltså, är det möjligt att använda "force" (Forced Takeover) för att KO skall börja leverera anropande TLs tjänst istället för annan TLs tjänst. <br>
                Om Forced Takeover inte stöds skall <b>false</b> returneras.<br>
                <em>true eller false, obligatoriskt</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>active</code>
            </td>
            <td>
                Lista över de tjänster som är aktiva på accessen för inloggad TL. <em>obligatorisk</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>active / service</code>
            </td>
            <td>
                Service-namn på den aktiva tjänsten. Skall finnas i "services"-listan. <em>text, obligatoriskt</em><br>
                <br>
                Exempel: "BB-100-10"
            </td>
        </tr>
        <tr>
            <td>
                <code>active / option82</code>
            </td>
            <td>
                Fältet används av tjänsteleverantör för att korrelera en DHCP förfrågan till en Access. Värdet utgör alltså en nyckel som DHCP, Radius och TR69-servrar använder för att slå upp access-specifik information. Option82 måste vara unikt inom en kommunikationsoperatörs bestånd. Se <em>text, obligatoriskt</em><br>
                <a href="option82.md">Option82 format</a>
                <br>
                Exempel: "5216010765746820302F31020B31302E31302E31302E3130"<br/>
            </td>
        </tr>
        <tr>
            <td>
                <code>active / equipment</code>
            </td>
            <td>
                Lista av utrustning som tjänsteleverantör angett för tjänsten.<br>
                Se <a href="service_activation.md">Service Activation</a> för mer information.
            </td>
        </tr>
        <tr>
            <td>
                <code>spReference</code>
            </td>
            <td>
                Se <a href="service_activation.md">Service Activation</a> för fullständig förklaring och specifikation.
            </td>
        </tr>
    </tbody>
</table>
