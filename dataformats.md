# Conventions and formatting

All use of the on-api is expecting formatting to be according to these rules.

## Data fields
<table>
  <tbody>
  <tr>
    <td><strong>Field</stong></td>
    <td><strong>Sample(s)</stong></td>
    <td><strong>Explanation</stong></td>
  </tr>
  <tr>
    <td>accessId</td>
    <td>123456<br>ADA1343-12</td>
    <td>One, per communications operator, unique ID for an access.<br> May only concist of the a-z, A-Z , 0-9, '-' and '.'. [a-zA-Z0-9-.]+. Max length 32 characters</td>
  </tr>
  <tr>
    <td>phoneNo</td>
    <td>+46701234567<br>+12035551345</td>
    <td>Phone numbers should always follow the E.164 convensions and consist of a +-sign followed by digits only. Incl country code such as 46 for Sweden and 1 for US/Canada.</td>
  </tr>
  </tbody>
</table>
