# TL API: Kundinformation för Access

Syftet med API är att låta KO hämta kundinformation om en access från Tjänsteleverantör.

Använd `access_sp` - endpointen för att hämta kundinformation med tjänsteleverantörens kundnummer.

Möjlighet att skicka med ett ticket-id eller anledning till varför kunduppgifterna efterfrågas.

*OBS! Till skillnad mot andra APIer är KO klient och TL server i detta API.*

## Exempel

Request:
```http
GET /api/2.3.1/access/STTA0001 HTTP/1.1
```

```http
GET /api/2.3.1/access_sp/1337 HTTP/1.1
```

```http
POST /api/2.3.1/access/STTA0001 HTTP/1.1
Content-Type: application/json

{
    "koTicketReference": "123123",
    "spTicketReference": "123123",
    "reason": "Techinician need to know..."

}
```
```http
POST /api/2.3.1/access_sp/1337 HTTP/1.1
Content-Type: application/json

{
    "koTicketReference": "123123",
    "spTicketReference": "123123",
    "reason": "Techinician need to know..."
}
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "BB-1000-100": {
        "customer": {
            "name": "Kalle Anka",
            "email": "karl@ankeborg.se",
            "phone": "",
            "mobilePhone": ""
        },
        "spReference: "1337",
        "accessId": "STTA0001" 
    }
}
```




## Fältbeskrivningar

<table>
    <tbody>
        <tr>
            <td><strong>Fält</strong></td>
            <td><strong>Förklaring</strong></td>
        </tr>
        <tr>
            <td>
                <code>service</code>
            </td>
            <td>
                Service är key i root-objektet.<br>
                Anger teknisk tjänst som skall vara aktiv på accessen. <br>
                Värden för tekniska tjänster är KO-specifika och erhålls genom Feasibility-APIt. <em>text, obligatoriskt</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>customer</code>
            </td>
            <td>
                Syftet med customer är att ge KO information om Tjänsteleverantörens slutkund.<br>
                JSON-strukturen är obligatorisk och kommer alltid skickas med, men samtliga attribut kan vara tomma.<br>
            </td>
        </tr>
        <tr>
            <td>
                <code>customer.phone</code>
            </td>
            <td>
                Exempelformat: +4631650000
            </td>
        </tr>
        <tr>
            <td>
                <code>customer.mobilePhone</code>
            </td>
            <td>
                Exempelformat: +4631650000
            </td>
        </tr>
        <tr>
            <td>
                <code>spReference</code>
            </td>
            <td>
                `spReference` anger TLs referens på tjänsten. Används av TL för korrelering.<br>
                <em>Sträng, max 255 tecken</em>
            </td>
        </tr>
        <tr>
            <td>
                <code>accessId</code>
            </td>
            <td>
                `accessId` blir redundant men skickas med för att göra endpoints enhetliga beroende på vilket kundnummer man efterfrågar med</em>
            </td>
        </tr>
    </tbody>
</table>

Gemensamt för alla fält är att de måste finnas i JSON-strukturen och inte vara null.


POST-parametrarna `koTicketReference` `spTicketReference` `reason` är frivilliga att användas om man vill eller om enskild SP + KO kommer överens om implementation.