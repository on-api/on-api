# Web Portal API

Syftet med Web Portal API är att på ett säkert sätt kunna göra en överlämning av en kund från en kommunikationsoperatörs web-portal till en tjänsteleverantörs. I samband med en sådan överlämning så vill man skicka med data så som kundens access-id till tjänsteleverantören. Tanken är alltså att KO detekterar port (access) och sedan ger kunden en länk eller gör en HTTP redirect till TL-portal.

Detta API specificerar inte vad tjänsteleverantörens portalsida skall användas till. Tänkbara användingsområden är aktivering, kontroll, eller köp av tjänster.

Detta API specificerar inte i vilket skede en KO gör överlämningen till tjänsteleverantörens portal. Man kan tänka sig scenarion där KO gör en automatisk HTTP redirect till TL baserad på t.ex. vendor-id (option 60) i DHCP eller att kunden måste klicka på en länk i KO:s portal.

## URL-format

En web portal URL skall ha följande format:

	https://sp.example.com/some-path?ko=example_net&accessId=ABCD1234&mac=01:23:45:67:89:AB&tid=2017-08-15T06:58:26.628Z&hash=16eec7df7085f2de0a8d351ac4c75a0c02fb775c5eb823f96e6fb19bedaf65ed

`sp.example.com` är en server som driftas av TL. Hostnamn, och path bestäms gemensamt av KO och TL och specificeras inte av detta API.

<table>
	<tr>
		<th>Query parameter</th>
		<th>Beskrivning</th>
	</tr>
	<tr>
		<td>
			<code>ko</code>
		</td>
		<td>
			Identifierare av KO.
		</td>
	</tr>
	<tr>
		<td>
			<code>accessId</code>
		</td>
		<td>
			KO:s detekterade access-id.
		</td>
	</tr>
	<tr>
		<td>
			<code>mac</code>
		</td>
		<td>
			MAC-adress för kundens utrustning. Detta kan vara användbart för TL för felsökning och aktivering av tjänster (t.ex. ATA-box i hemma-router levererad av TL).<br>
			MAC-adressen representeras genom 6 par av hexadecimala siffror konkatenerade med kolon ':'. Den skall uteslutande vara i uppercase.<br>
			MAC-adressen är alltid exakt 17 tecken lång.<br>
			Exempel: "01:23:45:67:89:AB".
		</td>
	</tr>
	<tr>
		<td>
			<code>tid</code>
		</td>
		<td>
			Tidsstämpel då URL:en skapades. TL kan avgöra hur länge en URL skall vara godkänd att användas beroende på hur känslig data som exponeras av portalen. Detta för att förhindra replay-attacker.<br>
			Skall vara formaterad enligt ISO-8601 i tidszon Z (UTC).
		</td>
	</tr>
	<tr>
		<td>
			<code>hash</code>
		</td>
		<td>
			Kryptografisk hash (Message Authentication Code) av övriga query parametrar (se nedan) i hex-format.
		</td>
	</tr>
</table>

## Kryptografisk hash (Message Authentication Code)

För att förhindra att spoofing-attacker där en attackerare anger ett annat access-id eller MAC än det hen faktiskt sitter på så behöver datat signeras. Detta görs med fördel med en standardiserad algoritm som HMAC-SHA256.

KO och TL kommer behöva komma överens om algoritm och en (gemensam) hemlig nyckel som skall användas vid signeringen.

Hashen skapas genom att initiera algoritmen med det hemliga lösenordet och sedan i tur och ordning skriva värdet av `ko`, `accessId`, `mac`, `tid` encodade i UTF-8.

Exempelimplementation i Java:
```java
	public static byte[] authenticationHash(String ko, String accessId, String mac, String tid) throws NoSuchAlgorithmException, InvalidKeyException  {
		Mac macAlgo = Mac.getInstance("HmacSHA256");
		SecretKeySpec keySpec = new SecretKeySpec("secret-password".getBytes(UTF_8), "HmacSHA256");
		macAlgo.init(keySpec);
		macAlgo.update(ko.getBytes(UTF_8));
		macAlgo.update(accessId.getBytes(UTF_8));
		macAlgo.update(mac.getBytes(UTF_8));
		macAlgo.update(tid.getBytes(UTF_8));
		return macAlgo.doFinal();
	}
```

Ev. URL-encoding av query-paramterar skall *inte* påverka `hash`; värdet skall alltid genereras från de avkodade värderna. D.v.s. samma värde på hashen skall genereas oavsett om `mac` skickas som `mac=01:23:45:67:89:AB` eller som `mac=01%3A23%3A45%3A67%3A89%3AAB` i URL:en.

Notera att hostnamn och path inte är del av hashen, detta för att underlätta att TL-portalen kan finnas på flera nät och bakom diverse HTTP proxies etc.




