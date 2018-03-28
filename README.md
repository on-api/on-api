# Open Networks API 2.3.1

##### Länk till dokumentation: [ON-API 2.3.1](https://on-api.github.io "ON-API docs")
##### Länk till github repository: [on-api/on-api-prerelease](https://github.com/on-api/on-api-prerelease "ON-API repo")

___

Open Networks API (ON-API) är ett leverantörsoberoende öppet API för effektivt systemsamarbete mellan tjänsteleverantörer (TL eller SP), öppna nät (ÖN) och kommunikationsoperatörer (KO eller CO). Vidare är ON-API ett initiativ som tagits av tjänsteleverantörer, kommunikationsoperatörer och systemleverantörer, med syfte att komma överens om en enhetlig standard för kommunikation mellan parterna. Första versionen, ON-API 2.3.1, är en förhandsrelease som innehåller mindre utbyggnad av PI-API 2.3, med utökat stöd för GDPR.

API exponerar de accesser som ställs till förfogande för tjänsteleverantörer att leverera sina tjänster på. På de accesser som exponeras kan sedan tekniska tjänster beställas, avbeställas och konsolideras.
Innehåller operationer med följande syften:

Innehåller operationer med följande syften:
* Hämta säljdata/univers från KO.
* Beställa tjänster hos KO.
* Hämta tekniska detaljer och status på aktiva tjänster hos KO.
* Stöd för autoaktivering.
* Uppfyller GDPR.

___

## Terminologi

### Access

En _Access_ definieras som en avlämningspunkt som måste aktiveras för att en slutkund skall få tjänst. Utgörs typiskt av en port i en access-switch, förbindelsen till och uttaget i bostaden.

### Feasibility

_Feasibility_ definieras som lista med _accesser_ med tillhörande data för att unikt kunna identifiera accesser (adress, lägenhetsbeteckningar etc.) och vilka tekniska tjänster som är potentiellt beställningsbara (per _access_). _Feasibility_ omfattar inte om tjänsterna är aktiva eller tillgängliga. _Feasibility_ används till säljkampanjer, täckningskartor och liknande. _Feasiblitity_ används även vid kontakt med slutkund för att identifiera vilken specifik _access_ som tjänster skall aktiveras på.

### Availability

_Availability_ definieras som aktuell status på vilka tjänster som är aktiva och vilka som går att leverera på en specifik access. _Availability_-frågor används ofta interaktivt, exempelvis under konversation med potentiell slutkund. KO kan med hjälp av _Availability_ indikera om en teknisk tjänst är "upptagen" av en annan TL.

### Teknisk Tjänst

En _Teknisk Tjänst_ definieras som en tjänst, vars realisation är unik. Det skall alltså endast finnas en teknisk tjänst med samma nätkonfiguration. Det betyder att det inte får finnas olika tekniska tjänster beroende på pris, bindningstid eller andra erbjudanden. 
_Tekniska Tjänster_ skall även vara ortogonala mot andra tekniska tjänster av annan tjänstetyp. Tjänstetyp är Bredband, Telefoni och TV. En _Teknisk Tjänst_ får inte avse mer än en tjänstetyp. Det betyder att det inte får finnas tekniska tjänster som avser flera tjänster, exempelvis "Bredband 10/10 + TV".