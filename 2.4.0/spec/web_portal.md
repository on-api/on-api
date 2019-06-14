# Web Portal API

The purpose of this APi is to enable the hand over of an end-user from the portal of a communication operator to the portal of a service provider.
The communication provider identifies the port that the request originated at, and adds accessId and mac-address to a link that is either given to the customer or used by a HTTP redirect. 

The API doesnt specify what the portals are used for. It could for example be to activate an subscription, to buy a subscription or to do some kind of control.

The Web-portal URL has the following format
<pre>
https://&lt;service-provider&gt;/&lt;path&gt;?ko=<b>&lt;co-id&gt;</b>&amp;accessId=<b>&lt;accessID&gt;</b>&amp;mac=<b>&lt;mac-address&gt;</b>&amp;tid=<b>&lt;timestamp&gt;</b>&amp;hash=<b>&lt;hash&gt;</b>
</pre>

## Example

	https://sp.example.com/some-path?ko=example_net&accessId=ABCD1234&mac=01:23:45:67:89:AB&tid=2017-08-15T06:58:26.628Z&hash=16eec7df7085f2de0a8d351ac4c75a0c02fb775c5eb823f96e6fb19bedaf65ed

`sp.example.com` is a server at the Service provider.
Host name and path are set by the service provider and are used by the communication operator when creating the URL.


## Parameters

<table>
	<tr>
		<th>Query parameter</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>
			<code>ko</code>
		</td>
		<td>
			<p>Identification of the communication operator.</p>
			<p>See coID in <a href="dataformats.md">dataformats</a></p>
		</td>
	</tr>
	<tr>
		<td>
			<code>accessId</code>
		</td>
		<td>
			<p>The accessID identified by the communication operator.</p>
			<p>See accessID in <a href="dataformats.md">dataformats</a></p>
		</td>
	</tr>
	<tr>
		<td>
			<code>mac</code>
		</td>
		<td>
			<p>The MAC-address of the end users equippment.</p>
			<p>To be used in fault localization and activation.</p>
			<p>See mac-address in <a href="dataformats.md">dataformats</a> for data format</p>
		</td>
	</tr>
	<tr>
		<td>
			<code>tid</code>
		</td>
		<td>
  			<p>Time stamp when the URL was created.</p> 
            <p>Depending on the use case and the sensitivty of the data, the service provider can choose to only trust the information in a certain time intervall.</p>
			<p>See dateTime in <a href="dataformats.md">dataformats</a> for data format</p>
		</td>
	</tr>
	<tr>
		<td>
			<code>hash</code>
		</td>
		<td>
			<p>Cryptographic hash (Message Authentication Code) of the other query parameters in hex format.</p>
			<p>See below for details.</p>
		</td>
	</tr>
</table>

## Cryptographic hash (Message Authentication Code)

To authenticate the query parameters in the URL, a HMAC-SHA256 should be calculated on the other query parameters.
A pre shared key is used between the communication operator and the service provider. 

The hash must be calculated on the following parameters and in the following order:
1. `ko`
2. `accessId`
3. `mac`
4. `tid`

The values should be UTF-8 encoded.

***Note 1:***  Any URL-encoding of the of the query parameters should *not* affect the `hash`-value.
The hash should be calculated before any URL-encoding occurs.

