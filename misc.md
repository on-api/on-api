# Övergripande Information

## Endpoints

_En_ URL pekar ut adressen till roten API:et, ex. `http://host/api/2.3/`.

Under URL:en förväntas tjänsterna finnas: `orders/` (`http://host/api/2.3/orders/`),  `accesses/` (`http://host/api/2.3/accesses/`) etc.

## Autentisering

Autentisering sker med HTTP BASIC. Se [RFC-2617][rfc2617].

[rfc2617]: http://www.ietf.org/rfc/rfc2617.txt "HTTP Authentication: Basic and Digest Access Authentication"

## Character Encoding

Samtliga API:er använder UTF-8.

