# Contact information for end customers

The API enables the CO to request contact information for an end customer from the SP.

## Usage

The CO requests contact information for a customer identified with the `spReference` that was provided by the SP 
during activation. The CO must also provide either a `reason` or a `spTicketReference` in the request.

## Request

Request information with a reason:

```http
POST /2.6/contacts/{ spReference }

{
  "reason": "Reason for request"
}
```

Request information with a ticket reference:

```http
POST /2.6/contacts/{ spReference }

{
  "spTicketReference": "123"
}
```

### spReference

The spReference value that was provided by the SP during activation.

* Data format: [text](../common/dataformats.md#text)
* Mandatory

### reason

The reason for requesting this information.

* Data format: [text](../common/dataformats.md#text)
* Mandatory if spTicketReference is not provided

### spTicketReference

The spTicketReference, used for tracking, that was provided by the SP for a related ticket created via ON-API.

* Data format: [text](../common/dataformats.md#text)
* Mandatory if reason is not provided

## Response

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@johndoe.com",
  "phone": "",
  "mobilePhone": ""
}
```

For data format, see [data formats](../../2.6.0/common/dataformats.md)
