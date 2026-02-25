---
Document: Definition_of_Done_Template
Version: 1.2
Status: Draft
Audience: Interns
Approval required: Yes
Changes from v1.1: Added privacy & data protection checkpoint
Taal: Nederlands (vertaling van v1.2)
---

# Definition of Done (Template)

Elk team stelt zijn eigen Definition of Done op.
Gebruik dit template als startpunt.

## Code
- Code is leesbaar en beoordeeld door minimaal één teamlid
- Geen kritieke waarschuwingen of fouten
- Code voldoet aan de overeengekomen codestandaarden

## Testen
- Unit tests zijn toegevoegd of bijgewerkt waar relevant
- Tests slagen in CI
- Testdekking is adequaat voor de gemaakte wijzigingen

## DevOps
- Build is geslaagd
- Relevante geautomatiseerde tests worden uitgevoerd als onderdeel van de pipeline
- Deployment werkt in de doelomgeving (indien van toepassing)

## Kwaliteit & Weerbaarheid
- De applicatie gedraagt zich voorspelbaar onder faalcondities
- Fouten worden duidelijk gelogd
- Herstel of rollback is mogelijk

## Documentatie
- Wijzigingen zijn gedocumenteerd
- Setup-instructies zijn bijgewerkt (indien van toepassing)
- API-documentatie is bijgewerkt (indien van toepassing)

## Architectuur
- Architecturele impact is gedocumenteerd (indien van toepassing)
- Als er significante architecturele beslissingen zijn genomen:
  - Een Architecture Decision Record (ADR) is opgesteld
  - Het ADR is beoordeeld en geaccepteerd door het team
  - Architectuurdiagrammen zijn bijgewerkt (indien nodig)

## Privacy & Gegevensbescherming
- Verwerking van persoonsgegevens is beoordeeld (indien van toepassing)
- Geen gevoelige gegevens zichtbaar in logs of foutmeldingen
- Gevolgen voor dataretentie zijn overwogen
- Toegangscontroles voorkomen ongeautoriseerde toegang tot gegevens
- Privacy by design principes zijn gevolgd

## Akkoord
- Het team is het erover eens dat dit werk "Done" is
- Done betekent: klaar om te tonen in een Sprint Demo en klaar om door anderen gebruikt te worden

---

## Toelichting op "indien van toepassing"

Niet elk item vereist alle checkpoints:
- **Kleine bugfixes** hoeven mogelijk niet architectureel gedocumenteerd te worden
- **Alleen UI-wijzigingen** zijn mogelijk niet van invloed op API-documentatie
- **Interne refactoring** vereist mogelijk geen bijgewerkte setup-instructies

Gebruik professioneel oordeel als team.
Twijfel je? Documenteer dan.

---

**Einde Definition of Done Template v1.2**
