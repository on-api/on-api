# Provider API 2.3

API 2.3 innehåller ändringar motiverade av [GDPR][wikipedia-gdpr].

# Skillnader mot API 2.2

## Ändringar som bryter API

* Borttagning av reglerad kundinformation i Service Activation API.
 * Fälten `customer` och `deliveryAddress` är borttagna.
 * Trouble-Ticket API är borttaget.

## Nytt i API 2.3

* SP-referenser i Service Activation API & Availability API.
* Nytt API för låta KO hämta kundinformation associerad med en access från TL.
* Backport av Web Portal API från API 3.0

[wikipedia-gdpr]: https://sv.wikipedia.org/wiki/Allm%C3%A4nna_dataskyddsf%C3%B6rordningen "Allmänna_dataskyddsförordningen"
