# Conventions and formatting

All use of the on-api is expecting formatting to be according to these rules.

## Data fields
<table>
  <thead>
  <tr>
    <th>Field</th>
    <th>Sample(s)</stong></th>
    <th>Explanation</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td>accessId</td>
    <td>123456<br>ADA1343-12</td>
    <td>One, per communications operator, unique ID for an access.<br> May only concist of the a-z, A-Z , 0-9, '-' and '.'. [a-zA-Z0-9-.]+. Max length 32 characters</td>
  </tr>
  <tr>
    <td>spReference</td>
    <td>123<br>ABC123<br>abc-123</td>
    <td><p>`spReference` is set by the service provider and is used as a reference of the service</p>
        <p>Text, max 255 characters</p>
  </tr>

  <tr>
    <td>phoneNo</td>
    <td>+46701234567<br>+12035551345</td>
    <td>Phone numbers should always follow the E.164 convensions and consist of a +-sign followed by digits only. Incl country code such as 46 for Sweden and 1 for US/Canada.</td>
  </tr>
  <tr>
    <td>option82</td>
    <td>520A01036162630203313233</td>
    <td>
    <p>DHCPv4 Option82 should be hex encoded.</p>
    <p>The complete option82 TLV (typ, length, value) should be encoded.</p> 
    <p>The data should allways start with 52 which is hex for 82</p>
    </td>
  </tr>
    <tr>
    <td>ticketReference</td>
    <td>abc1234<br>987654321<br>abc-123.DEF</td>
    <td>
    <p>Reference to a ticket in ticket system</p>
    <p>May only concist of the a-z, A-Z , 0-9, '-' and '.'. [a-zA-Z0-9-.]+. </p>
    <p>Max length 32 characters</p></td>
    </td>
  </tr>
  <tr>
    <td>coID</td>
    <td>testNet<br>exampleNet</td>
    <td>
    <p>Identification of the communication operator.</p>
    <p>May only concist of the a-z, A-Z , 0-9, '-' and '.'. [a-zA-Z0-9-.]+.</p>
    <p>Max length 32 characters</p></td>
    </td>
  </tr>
  <tr>
    <td>dateTime</td>
    <td>2017-08-15T06:58:26.628Z<br>2019-01-28T14:21:43.236Z</td>
    <td>
    <p>Time and date.</p>
    <p>Formated accordingly to ISO-8601. UTC Time zone should be used (time zone: Z).</p>
    <p>Max length 32 characters</p></td>
    </td>
  </tr>
  <tr>
    <td>mac-address</td>
    <td>01:02:03:04:05:06<br>AA:BB:CC:DD:EE</td>
    <td>
    <p>MAC address.</p>
    <p>Formatted as 12 hexadecimal digits with a colon (":") as a separator every third character.</p>
    <p>Digits A to F should use capital letters</p></td>
    </td>
  </tr>

  </tbody>
</table>
