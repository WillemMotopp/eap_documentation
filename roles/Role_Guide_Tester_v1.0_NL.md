# Tester / QA Role guide

**Versie:** 1.0  
**Datum:** 2026-03-03  
**Doelgroep:** Trainees (Tester/QA rol)  
**Doel:** Heldere verwachtingen, verantwoordelijkheden en praktische begeleiding

---

## Roloverzicht

### Wat is een Tester/QA?

De Tester (Quality Assurance) is **verantwoordelijk voor het waarborgen dat het product aan kwaliteitsnormen voldoet** voordat het gebruikers bereikt.

**Je bent NIET:**
- ❌ Alleen iemand die aan het eind op knoppen klikt
- ❌ De "kwaliteitspolitie" die alles afkeurt
- ❌ Alleen verantwoordelijk voor het vinden van bugs
- ❌ Alleen werkend nadat developers klaar zijn

**Je BENT:**
- ✅ Kwaliteitsadvocaat gedurende het hele ontwikkelproces
- ✅ Degene die nadenkt over edge cases en failure scenarios
- ✅ Bugs voorkomen, niet alleen vinden
- ✅ Samenwerken met developers vanaf story refinement tot deployment

### Kernverantwoordelijkheid

**In één zin:** Je zorgt ervoor dat het team hoogwaardige, werkende software levert door vroeg te testen, vaak te testen, en na te denken over wat fout kan gaan.

---

## Kernverantwoordelijkheden

### 1. Testplanning & Strategie

**Je helpt het team om vanaf het begin over testen na te denken:**

**Tijdens Refinement:**
- Begrijp acceptance criteria vanuit testperspectief
- Vraag "Hoe gaan we dit testen?" voor elke story
- Identificeer testscenario's en edge cases
- Signal early als requirements niet testbaar zijn

**Voor de Sprint:**
- Bekijk welke stories welke soorten tests nodig hebben
- Identificeer testafhankelijkheden (testdata, omgevingen)
- Plan de testaanpak voor de sprint

### 2. Testontwerp & Uitvoering

**Je creëert en voert tests uit:**

**Testontwerp:**
- Schrijf testcases gebaseerd op acceptance criteria
- Denk aan edge cases die developers kunnen missen
- Ontwerp tests voor happy path EN failure scenarios
- Overweeg verschillende gebruikerstypes en datascenario's

**Testuitvoering:**
- Voer handmatige tests uit op afgeronde features
- Voer geautomatiseerde tests uit (als het team die heeft)
- Test integraties tussen componenten
- Verifieer fixes voor bugs
- Voer regressietests uit (hebben we iets anders kapotgemaakt?)

### 3. Bug Detectie & Rapportage

**Je vindt problemen en communiceert ze helder:**

**Bugs Vinden:**
- Test features tegen acceptance criteria
- Probeer dingen intentioneel kapot te maken
- Test edge cases en boundary conditions
- Zoek naar usability issues en inconsistenties

**Bugs Rapporteren:**
- Documenteer bugs helder met stappen om te reproduceren
- Voeg screenshots/schermopnames toe
- Beoordeel ernst en prioriteit
- Verifieer bugfixes wanneer developers ze oplossen

### 4. Kwaliteitsadvocaat

**Je vertegenwoordigt kwaliteit in teambeslissingen:**

- Spreek je uit als Definition of Done niet wordt gehaald
- Pushback bij "ship it broken" druk
- Pleit voor testbaarheid in design
- Help team kwaliteitsrisico's te begrijpen

### 5. Testautomatisering Ondersteuning

**Je ondersteunt geautomatiseerd testen (met developers):**

- Identificeer welke tests geautomatiseerd moeten worden
- Help developers testscenario's te begrijpen
- Schrijf geautomatiseerde tests als je codeervaardigheden hebt
- Onderhoud en update bestaande geautomatiseerde tests

**Let op:** In EAP schrijven developers vaak geautomatiseerde tests. Jouw rol is zorgen dat de JUISTE dingen getest worden.

### 6. Documentatie & Kennisdeling

**Je documenteert kwaliteit en deelt learnings:**

- Documenteer testscenario's en resultaten
- Houd bekende issues en workarounds bij
- Deel bevindingen in Sprint Review
- Update testdocumentatie naarmate product evolueert

---

## Concrete Taken

### Tijdens Sprint 0 (Voorbereidingsweek)

**Jouw taak deze week: Testfundament voorbereiden**

**Dag 1-2:**
- [ ] Lees Product Vision en begrijp productdoelen
- [ ] Bekijk user stories in Product Backlog
- [ ] Begrijp GDPR-vereisten (testen van privacy features)
- [ ] Zet je testomgeving op (toegang tot VPS, testaccounts)

**Dag 2-3:**
- [ ] Neem deel aan het opstellen van Definition of Done
- [ ] Voeg testperspectief toe: "Wanneer is iets echt done?"
- [ ] Zorg dat DoD testvereisten bevat
- [ ] Bekijk Definition of Ready - voeg "testbaarheid" overwegingen toe

**Dag 3-5:**
- [ ] Neem deel aan backlog refinement sessies
- [ ] Vraag voor elke story: "Hoe gaan we dit testen?"
- [ ] Identificeer stories die specifieke testdata of setup nodig hebben
- [ ] Signal onduidelijke of niet-testbare acceptance criteria

**Dag 4-5:**
- [ ] Help team stories te schatten (testinspanning is onderdeel van schatting)
- [ ] Maak initieel testplan template voor Sprint 1
- [ ] Zet bug tracking aanpak op in Jira
- [ ] Bereid testdata voor Sprint 1 stories voor

**Einde Sprint 0:**
- [ ] Je begrijpt het product en zijn kwaliteitsvereisten
- [ ] Je weet welke stories in Sprint 1 zitten en hoe ze te testen
- [ ] Testomgeving is klaar
- [ ] Team begrijpt je rol en hoe jullie samenwerken

### Tijdens Elke Sprint (Doorlopend)

**Begin Sprint (Sprint Planning):**
- [ ] Luister naar user story discussies
- [ ] Identificeer testaanpak voor elke story
- [ ] Noteer eventuele testafhankelijkheden of blockers
- [ ] Zorg dat testinspanning wordt meegenomen in team's commitment
- [ ] Stel verduidelijkende vragen over acceptance criteria

**Tijdens Sprint (Dagelijks Werk):**

**Dagelijks:**
- [ ] Woon Daily Standup bij
- [ ] Rapporteer testvoortgang en eventuele blockers
- [ ] Test afgeronde features (wacht niet tot einde sprint!)
- [ ] Log bugs in Jira met heldere reproductiestappen
- [ ] Communiceer bevindingen onmiddellijk naar developers

**Continue Testen:**
- [ ] Test features zodra developers ze markeren als "ready for testing"
- [ ] Wacht niet - test incrementeel gedurende sprint
- [ ] Verifieer bugfixes binnen 24 uur nadat developer "fixed" markeert
- [ ] Voer snelle regressietests uit wanneer code wijzigt
- [ ] Test op verschillende browsers/devices indien relevant

**Half Sprint:**
- [ ] Bekijk sprint voortgang - liggen we op schema qua kwaliteit?
- [ ] Escaleer kwaliteitszorgen als sprint doel in gevaar is
- [ ] Update testdocumentatie voor afgeronde features
- [ ] Bereid complexe testscenario's voor resterende werk voor

**Samenwerking:**
- [ ] Pair met developers op complexe features (test terwijl ze coderen)
- [ ] Help developers testbare code te schrijven
- [ ] Review Pull Requests vanuit testperspectief (indien tijd)
- [ ] Deel testresultaten en bevindingen proactief

**Einde Sprint (Sprint Review):**
- [ ] Verifieer dat al het geaccepteerde werk aan DoD voldoet
- [ ] Test het geïntegreerde increment (volledige regressie)
- [ ] Bereid kwaliteitsrapport voor Sprint Review voor
- [ ] Demo eventuele gebruikte testtools of -aanpakken
- [ ] Documenteer bekende issues die nog niet gefixt zijn

**Einde Sprint (Sprint Retrospective):**
- [ ] Deel wat werkte/niet werkte in testproces
- [ ] Suggereer verbeteringen aan testaanpak
- [ ] Bespreek kwaliteitsissues en hoe ze te voorkomen
- [ ] Commit aan verbeteringen in testproces

### Soorten Tests Die Je Uitvoert

**Functionele Tests:**
- Doet de feature wat het moet doen?
- Slagen alle acceptance criteria?
- Werken happy path scenario's?

**Negatieve Tests:**
- Wat gebeurt er met ongeldige input?
- Wat als verplichte velden leeg zijn?
- Wat als gebruiker iets onverwachts probeert?

**Edge Cases:**
- Grenswaarden (min/max datums, zeer lange tekst, etc.)
- Speciale karakters in input
- Meerdere gebruikers die toegang hebben tot dezelfde data
- Netwerkonderbrekingen of timeouts

**Integratietests:**
- Werken frontend en backend samen?
- Werkt e-mailverzending end-to-end?
- Interacteren verschillende features correct?

**Regressietests:**
- Hebben nieuwe wijzigingen bestaande features kapotgemaakt?
- Snelle smoke test van kernfunctionaliteit

**GDPR/Privacy Tests:**
- Kunnen gebruikers hun data exporteren?
- Kunnen gebruikers dataverwijdering aanvragen?
- Is persoonlijke data goed beschermd?
- Werken toegangscontroles?

**Usability Tests:**
- Is de interface intuïtief?
- Zijn foutmeldingen duidelijk?
- Is de gebruikersflow logisch?

**Browser/Device Tests:**
- Werkt het in Chrome, Firefox, Safari?
- Werkt het op mobiel (responsive design)?

**Performance Tests (Basis):**
- Laadt de pagina in redelijke tijd?
- Kan het meerdere gelijktijdige requests aan?

---

## Hoe Schrijf Je Goede Bug Reports

### Bug Report Template

```
TITEL: Heldere, specifieke beschrijving (bijv. "Login faalt met geldige credentials")

ERNST: Kritiek / Hoog / Gemiddeld / Laag

PRIORITEIT: Urgent / Hoog / Gemiddeld / Laag

OMGEVING:
- Browser: Chrome 120.0
- OS: Windows 11
- Server: Testomgeving (motoppdemo.nl)

STAPPEN OM TE REPRODUCEREN:
1. Navigeer naar https://motoppdemo.nl/login
2. Voer gebruikersnaam in: "test@example.com"
3. Voer wachtwoord in: "ValidPass123!"
4. Klik op "Inloggen" knop

VERWACHT RESULTAAT:
Gebruiker moet inloggen en doorgestuurd worden naar dashboard

WERKELIJK RESULTAAT:
Foutmelding verschijnt: "Ongeldige credentials" hoewel credentials correct zijn
Gebruiker blijft op loginpagina

AANVULLENDE INFORMATIE:
- Gebeurt consistent (100% reproductiesnelheid)
- Screenshot bijgevoegd: [link]
- Network log toont 401 error van /api/auth/login
- Console error: "TypeError: Cannot read property 'token' of undefined"

IMPACT:
Gebruikers kunnen niet inloggen in de applicatie

WORKAROUND:
Geen gevonden
```

### Ernst vs Prioriteit Gids

**Ernst = Hoe erg is de bug?**
- **Kritiek:** Systeem crash, dataverlies, beveiligingsbreuk
- **Hoog:** Kernfunctie volledig kapot
- **Gemiddeld:** Feature werkt maar met significante issues
- **Laag:** Klein cosmetisch probleem of zeldzame edge case

**Prioriteit = Hoe urgent moet het gefixt worden?**
- **Urgent:** Fix onmiddellijk (blokkeert alles)
- **Hoog:** Fix deze sprint
- **Gemiddeld:** Fix snel (komende 1-2 sprints)
- **Laag:** Fix wanneer tijd het toelaat

**Voorbeelden:**

**Kritiek + Urgent:**
"Gebruikers kunnen geen verzoeken indienen (500 error)" → Fix NU

**Hoog + Gemiddeld:**
"Datumvalidatie staat ongeldige datums toe" → Fix deze sprint, maar heeft workaround

**Laag + Laag:**
"Knop uitlijning is 2px off" → Fix bij UI polish

---

## Goede Praktijkscenario's

### Scenario 1: Vroege Test Samenwerking

**Context:** Sprint Planning, team bespreekt nieuwe story "Medewerker kan verlofaanvraag indienen"

**Wat Tester Doet:**

**Tijdens story discussie:**

> **Tester:** "Ik zie dat de acceptance criteria 'startdatum en einddatum' noemen. Moeten we testen:
> - Wat gebeurt er als einddatum voor startdatum ligt?
> - Wat is de maximale datumrange die is toegestaan?
> - Kunnen gebruikers datums in het verleden selecteren of alleen toekomstige?
> - Hoe zit het met feestdagen - moeten die behandeld worden?"

**Developer:** "Goede vragen. Laat me dit verduidelijken met de Product Owner..."

**Product Owner:** "Einddatum moet na startdatum liggen. Geen maximale range. Alleen toekomstige datums. Feestdagen zijn out of scope voor deze sprint."

**Tester:** "Perfect, ik zal die scenario's testen. Ook, moeten we concurrente indieningen testen - wat als gebruiker hetzelfde verzoek twee keer indient?"

**PO:** "Goed punt - voeg validatie toe om dubbele indieningen binnen 1 minuut te voorkomen."

**Resultaat:**
- ✅ Requirements verduidelijkt VOOR coderen
- ✅ Edge cases vroeg geïdentificeerd
- ✅ Acceptance criteria uitgebreid
- ✅ Minder rework later

**Waarom dit goed is:**
- Tester nam actief deel aan Planning
- Vroeg "Hoe gaan we dit testen?" vroeg
- Hielp requirements te verbeteren
- Voorkwam bugs door vooruit te denken

### Scenario 2: Incrementeel Testen Tijdens Sprint

**Context:** Sprint Dag 3, developer rondt "basis formulier" story af

**Wat Tester Doet:**

**Developer in standup:** "Ik heb het verlofaanvraag formulier af. Klaar voor testen."

**Tester:** "Geweldig! Ik test het deze ochtend en geef je voor de lunch feedback."

**Ochtend - Testen:**
- [ ] Test happy path (geldige aanvraag indienen) ✅ Werkt
- [ ] Test lege verplichte velden ❌ Geen validatie, formulier wordt toch verstuurd
- [ ] Test ongeldige datum (eind voor start) ❌ Staat ongeldige datums toe
- [ ] Test zeer lange tekst in reden veld ✅ Werkt, kapt af op 500 tekens

**Voor lunch - Bug report:**
```
BUG-001: Formulier wordt verstuurd met lege verplichte velden
Ernst: Hoog | Prioriteit: Hoog
Stappen: Laat alle velden leeg, klik Versturen
Verwacht: Validatiefouten getoond
Werkelijk: Formulier wordt verstuurd met lege waarden
```

**Developer:** "Bedankt! Ik fix dit vandaag."

**Middag - Developer fixt, Tester hertest:**
- ✅ Validatie werkt nu
- ✅ Alle originele tests slagen nog (regressiecheck)

**Volgende ochtend standup:**

**Tester:** "Formulier story is nu volledig getest en werkend. Developer kan naar volgende story."

**Resultaat:**
- ✅ Bugs vroeg gevonden (Dag 3, niet Dag 10)
- ✅ Developer kreeg snelle feedback
- ✅ Issues zelfde dag gefixt
- ✅ Story correct afgerond

**Waarom dit goed is:**
- Tester wachtte niet tot einde sprint
- Snelle feedback loop met developer
- Regressietesten na fixes
- Heldere communicatie over kwaliteit

### Scenario 3: GDPR Testen

**Context:** Sprint bevat "Gebruiker kan eigen data exporteren" story

**Wat Tester Doet:**

**Testplan voor GDPR Export:**

**Testscenario's:**
1. Gebruiker met data vraagt export aan → ontvangt bestand met al hun data
2. Gebruiker zonder data vraagt export aan → ontvangt leeg/minimaal bestand
3. Export bevat alle vereiste velden (naam, email, verzoeken, datums)
4. Export bevat NIET data van andere gebruikers
5. Export bestandsformaat is leesbaar (JSON/CSV)
6. Export werkt voor gebruikers met speciale karakters in data

**Testen:**

**Test 1: Gebruiker met data**
- Maak gebruikersaccount
- Dien 3 verlofaanvragen in
- Vraag data export aan
- Download bestand
- ✅ Verifieer: Alle 3 verzoeken aanwezig met correcte datums
- ✅ Verifieer: Email en naam van gebruiker aanwezig
- ✅ Verifieer: Bestandsformaat is geldig JSON

**Test 2: Data isolatie**
- Maak twee gebruikers (Gebruiker A, Gebruiker B)
- Gebruiker A dient verzoeken in
- Gebruiker B vraagt export aan
- ✅ Verifieer: Export van Gebruiker B bevat ALLEEN hun data, niet die van A

**Bevinding:**
❌ Export van Gebruiker B bevatte verzoek-IDs van Gebruiker A (niet volledige data, maar IDs lekten)

**Bug Report:**
```
BUG-015: Data export lekt verzoek-IDs van andere gebruikers
Ernst: Kritiek (GDPR schending)
Prioriteit: Urgent

Stappen:
1. Maak Gebruiker A, dien verzoek in (ID: 123)
2. Maak Gebruiker B, dien verzoek in (ID: 124)
3. Gebruiker B vraagt data export aan
4. Open export bestand van Gebruiker B

Verwacht: Alleen verzoek ID 124
Werkelijk: Export toont "related_requests": [123, 124]

GDPR Impact: Gebruiker B kan zien dat andere verzoeken bestaan (privacy lek)
```

**Developer:** "Oh! Ik had 'alle verzoeken in zelfde periode' per ongeluk toegevoegd. Fix het nu."

**Na fix:**
- Hertest alle 6 scenario's ✅ Alle slagen
- Markeer story als Done vanuit testperspectief

**Resultaat:**
- ✅ Kritieke GDPR bug gevonden voor productie
- ✅ Privacy by design gevalideerd
- ✅ Uitgebreide GDPR test coverage

**Waarom dit goed is:**
- Tester begreep GDPR vereisten
- Maakte specifiek testplan voor privacy
- Testte data isolatie expliciet
- Ving kritiek privacy lek

---

## Anti-Patronen (Wat Gaat Fout)

### Anti-Patroon 1: Alleen Testen aan Einde Sprint

**Hoe het eruitziet:**

**Sprint Dagen 1-8:** Tester wacht tot "alle features klaar zijn"

**Sprint Dag 9 (laatste dag):**

**Tester:** "Oké, ik begin nu met testen..."

*[Test 3 uur lang]*

**Tester:** "Ik heb 12 bugs gevonden. Geen van de stories voldoet aan Definition of Done."

**Developer:** "Maar sprint eindigt morgen! We hebben geen tijd om dit allemaal te fixen!"

**Scrum Master:** "Waarom ontdekken we dit op Dag 9?"

**Sprint Review:**
Slechts 1 van 5 stories is echt Done. Sprint Goal mislukt.

**Waarom het slecht is:**
- Geen tijd om bugs te fixen voor sprint eindigt
- Developers zitten stil vroeg in sprint, gestrest aan het eind
- Kwaliteit lijdt (druk om kapotte features te shippen)
- Team kan niet leveren op commitments
- Retrospective is pijnlijk

**Symptomen:**
- Meeste bugs gevonden in laatste 2 dagen van sprint
- Developers zeggen "Ik heb dit een week geleden afgerond"
- Stories voldoen zelden aan Definition of Done
- Sprint Reviews tonen kapotte features
- Team velocity is onvoorspelbaar

**Hoe te fixen:**

**Onmiddellijk:**
- **Test incrementeel:** Zodra developer zegt "ready for testing," test het
- **Wacht niet:** Zelfs als slechts één feature klaar is op Dag 2, test het op Dag 2
- **Snelle feedback:** Rapporteer bugs binnen uren, niet dagen

**Mindset shift:**
- Testen is NIET de finale fase
- Testen gebeurt GEDURENDE de sprint
- Je doel: Help team continue kwaliteit te leveren, niet beoordeel kwaliteit aan het eind

**Praktijken:**
- **Dagelijkse testcyclus:** Test wat elke dag klaar is
- **Zet verwachting:** "Ik test binnen 4 uur nadat je het ready markeert"
- **Communiceer status:** In standup, zeg "Story X is getest en done" of "Story Y heeft 3 bugs"

**Workflow voorbeeld:**
```
Dag 2: Developer rondt Story A af → Tester test → 2 bugs gevonden → Developer fixt → Done
Dag 4: Developer rondt Story B af → Tester test → Slaagt → Done
Dag 6: Developer rondt Story C af → Tester test → 1 bug → Developer fixt → Done
Dag 8: Volledige regressietest → Alles goed
Dag 9-10: Buffer voor eventuele issues, refinement voor volgende sprint
```

### Anti-Patroon 2: "Niet Mijn Taak" Tester

**Hoe het eruitziet:**

**Refinement sessie:**

**Developer:** "Hoe moeten we deze complexe workflow testen?"

**Tester:** "Dat is niet mijn taak. Jij schrijft de code, ik test het."

**Half Sprint:**

**Developer:** "Kun je me helpen deze edge case te begrijpen?"

**Tester:** "Ik test het wanneer je klaar bent. Stoor me niet tot dan."

**Bug gevonden:**

**Tester:** "Dit is compleet kapot. Hoe heb je dit zelfs geschreven?"

**Developer:** "Als je de aanpak eerder had beoordeeld, hadden we dit kunnen vermijden..."

**Team dynamiek:**
- Developers gefrustreerd met houding van tester
- Tester geïsoleerd van team
- Kwaliteit lijdt omdat tester alleen issues vindt, niet voorkomt
- Geen samenwerking, vijandige relatie

**Waarom het slecht is:**
- Testen wordt kwaliteitspoort, niet kwaliteitsadvocaat
- Tester gezien als blocker, niet helper
- Team werkt niet samen aan kwaliteit
- Bugs laat gevonden (duurder om te fixen)
- Team moraal daalt

**Symptomen:**
- Tester zit apart, engageert niet met team
- "Gooi het over de muur" mentaliteit
- Tester zegt vaak "niet mijn probleem"
- Developers vermijden vragen aan tester
- Retrospectives: klachten over tester-developer relatie

**Hoe te fixen:**

**Onmiddellijk:**
- **Excuseer je:** "Ik ben te afstandelijk geweest. Laten we beter samenwerken."
- **Bied hulp aan:** "Hoe kan ik je helpen dit de eerste keer goed te bouwen?"
- **Doe mee aan discussies:** Neem actief deel aan refinement, planning, design gesprekken

**Mindset shift:**
- **Je bent deel van het team, niet apart**
- **Kwaliteit is ieders taak** - jij bent de advocaat, niet enige eigenaar
- **Bugs voorkomen > Bugs vinden**
- **Samenwerking > Scheiding**

**Praktijken:**
- **Pair met developers:** "Kan ik met je meezitten terwijl je dit bouwt? Ik denk aan testcases."
- **Review designs:** "Laat me je aanpak bekijken voor je gaat coderen - ik spot edge cases"
- **Vriendelijke bug reports:** "Issue gevonden - laten we erover praten" niet "Dit is kapot"
- **Vier kwaliteit:** "Goed gedaan! Deze feature had nul bugs" niet alleen kritiek

### Anti-Patroon 3: Vage Bug Reports

**Hoe het eruitziet:**

**Bug Report Voorbeeld:**

```
Titel: Login werkt niet

Beschrijving: De login is kapot. Fix het.
```

**Developer reactie:** "Wat? Het werkt bij mij. Ik kan dit niet reproduceren."

**Tester:** "Nou het werkt niet! Fix het gewoon!"

**Developer:** "Kun je meer details geven?"

**Tester:** "Ik heb het je al verteld - het is kapot."

*[3 dagen heen-en-weer om bug te begrijpen]*

**Uiteindelijk ontdekt:** Gebeurt alleen wanneer wachtwoord speciale karakters heeft EN gebruikersaccount meer dan 7 dagen geleden is aangemaakt.

**Waarom het slecht is:**
- Developer kan bug niet reproduceren
- Verspilt tijd met heen-en-weer
- Bug wordt mogelijk niet goed gefixt
- Frustratie aan beide kanten
- Kritieke details ontbreken

**Symptomen:**
- Bugs worden gemarkeerd als "Kan Niet Reproduceren"
- Developers blijven om meer info vragen
- Bugs duren dagen om te fixen (zouden uren moeten zijn)
- Tester gefrustreerd dat bugs niet gefixt worden
- Developer gefrustreerd door onduidelijke reports

**Hoe te fixen:**

**Gebruik juiste bug template (zie sectie hierboven):**

**❌ SLECHT Bug Report:**
```
Login werkt niet
```

**✅ GOED Bug Report:**
```
TITEL: Login faalt met "Ongeldige credentials" voor gebruikers met speciale karakters in wachtwoord

ERNST: Hoog
PRIORITEIT: Hoog

OMGEVING:
- Browser: Chrome 120.0
- OS: Windows 11
- Testomgeving

STAPPEN OM TE REPRODUCEREN:
1. Maak gebruiker met email: test@example.com
2. Zet wachtwoord: "Pass@123!"
3. Wacht 8 dagen (of zet account aanmaakdatum handmatig op 8 dagen geleden in DB)
4. Navigeer naar loginpagina
5. Voer email in: test@example.com
6. Voer wachtwoord in: Pass@123!
7. Klik Inloggen

VERWACHT: Gebruiker logt succesvol in
WERKELIJK: Foutmelding "Ongeldige credentials" getoond

AANVULLENDE INFO:
- Gebeurt alleen met wachtwoorden met @ of !
- Gebeurt alleen voor accounts > 7 dagen oud
- Screenshot bijgevoegd
- Console toont: "Token validation failed"
- 100% reproduceerbaar met deze condities

WORKAROUND: Maak nieuw account (< 7 dagen) OF wijzig wachtwoord om speciale tekens te verwijderen
```

**Praktijken:**
- **Voeg altijd stappen toe om te reproduceren** - als je ze niet kunt schrijven, heb je de bug niet begrepen
- **Geef bewijs:** Screenshots, console logs, network logs
- **Test reproductie:** Voor je bug indient, probeer het zelf te reproduceren vanuit je stappen
- **Vraag jezelf af:** "Als ik dit report aan iemand anders geef, kunnen ze het reproduceren?"

### Anti-Patroon 4: "Automaat" Tester (Alleen Hokjes Afvinken)

**Hoe het eruitziet:**

**Testaanpak:**

**Tester vinkt methodisch elk acceptance criterium af:**
- [ ] Formulier heeft naamveld ✅
- [ ] Formulier heeft emailveld ✅
- [ ] Formulier heeft verstuur knop ✅
- [ ] Verstuur knop is klikbaar ✅

**Alle hokjes afgevinkt!**

**Tester markeert story als Done.**

**Maar Tester probeerde nooit:**
- Wat als email ongeldig formaat heeft?
- Wat als naam 500 karakters heeft?
- Wat als gebruiker formulier twee keer verstuurt?
- Wat als netwerk faalt tijdens versturen?
- Hoe zit het met toegankelijkheid (toetsenbordnavigatie)?

**Sprint Review - Stakeholder probeert feature te gebruiken:**

**Stakeholder:** "Ik diende in met email 'geenemail' en het accepteerde het!"

**Team:** "Dat stond niet in acceptance criteria..."

**Waarom het slecht is:**
- Acceptance criteria zijn minimumvereisten, niet complete testdekking
- Mist edge cases en real-world scenario's
- Product heeft slechte kwaliteit ondanks "geslaagde tests"
- Gebruikerservaring lijdt
- Bugs gevonden in productie of door stakeholders

**Symptomen:**
- Alle stories slagen testen, maar kwaliteit is slecht
- Bugs gevonden door stakeholders in Sprint Review
- Echte gebruikers vinden voor de hand liggende issues
- Tester zegt defensief "Het voldeed aan de criteria!"
- Team beseft dat acceptance criteria onvolledig waren

**Hoe te fixen:**

**Denk verder dan de checklist:**

**Acceptance Criteria (minimum):**
```
- [ ] Gebruiker kan emailadres invoeren
- [ ] Gebruiker kan formulier versturen
- [ ] Gebruiker ontvangt bevestiging
```

**Tester's uitgebreide testscenario's:**

**Happy Path:**
- Geldig email → versturen werkt → bevestiging ontvangen ✅

**Validatie:**
- Ongeldig emailformaat (geen @) → fout getoond ❌ BUG GEVONDEN
- Leeg email → fout getoond ✅
- Zeer lang email (500 tekens) → fout getoond ✅

**Edge Cases:**
- Email met speciale tekens (gebruiker+tag@example.com) → werkt ✅
- Email met unicode karakters → werkt of toont duidelijke fout ✅

**Gebruikerservaring:**
- Verstuur knop uitgeschakeld tijdens verzenden → voorkomt dubbel versturen ✅
- Duidelijke foutmeldingen → gebruiker begrijpt wat fout is ✅
- Toetsenbordnavigatie → formulier bruikbaar zonder muis ✅

**Integratie:**
- Netwerk faalt tijdens versturen → gebruiker krijgt duidelijke foutmelding ✅
- Server retourneert 500 error → gebruiker ziet vriendelijke boodschap ✅

**Mindset shift:**
- **Acceptance criteria = startpunt, niet finish**
- **Denk als gebruiker:** "Hoe zou dit kunnen breken?"
- **Denk kwaadwillig:** "Hoe kan ik dit kapotmaken?"
- **Denk creatief:** "Welke scenario's overwogen we niet?"

**Praktijken:**
- **Vraag "Wat als...?"** voor elke feature
- **Test happy path EN sad path**
- **Probeer dingen opzettelijk kapot te maken**
- **Denk aan real-world gebruiksscenario's**
- **Gebruik exploratory testing** - niet alleen gescripte tests

---

## Veelvoorkomende Uitdagingen & Oplossingen

### Uitdaging 1: "Developers markeren dingen 'Done' die niet Done zijn"

**Voorbeeld:** Developer markeert story Done, maar het voldoet niet aan Definition of Done (geen tests geschreven, bugs nog aanwezig, etc.)

**Oplossing:**

**1. Verwijs expliciet naar Definition of Done:**

**In Standup:**
> "Story X is gemarkeerd als Done, maar ik zie dat er nog geen unit tests zijn. Volgens onze DoD hebben we tests nodig. Kunnen we die toevoegen voor we het Done noemen?"

**2. Gebruik Jira workflow:**
- Developer markeert: "Ready for Testing"
- Tester test en: "Accept" (Done) of "Reject" (terug naar In Progress)
- Alleen Tester kan stories naar "Done" verplaatsen

**3. Team afspraak:**
- In Retrospective: "Laten we afspreken: Done betekent het voldoet aan DoD, niet alleen gecodeerd"
- Maak DoD zichtbaar (hang op muur, link in Jira)

### Uitdaging 2: "Ik heb niet genoeg tijd om alles te testen"

**Realiteit:** Je kunt niet alles exhaustief testen. Prioriteer.

**Oplossing - Risicogebaseerd Testen:**

**Hoge Prioriteit (Test grondig):**
- Kern gebruikersflows (login, hoofdfeatures)
- GDPR/privacy features (data export, verwijdering)
- Features die persoonlijke data raken
- Integratiepunten tussen systemen
- Features met complexe bedrijfslogica

**Gemiddelde Prioriteit (Test hoofdscenario's):**
- Secundaire features
- Edge cases voor kernflows
- UI polish en usability

**Lage Prioriteit (Snelle smoke test):**
- Cosmetische wijzigingen
- Interne tools
- Zelden gebruikte features

**Praktijken:**
- **Focus op risico:** "Wat is het ergste dat kan gebeuren als dit breekt?"
- **Test critical path eerst:** Kernfunctionaliteit voor nice-to-haves
- **Gebruik geautomatiseerde tests** voor repetitief testen (regressie)
- **Communiceer prioriteiten:** "Ik test X grondig, snel test Y, skip Z"

### Uitdaging 3: "Ik vond een bug, maar developer zegt het is een feature"

**Voorbeeld:** 

**Tester:** "Wanneer gebruiker ongeldige datum invoert, reset het formulier alle velden. Dat is een bug."

**Developer:** "Nee, dat is intentioneel - we maken formulier leeg bij elke fout."

**Tester:** "Maar gebruikers moeten alles opnieuw invoeren! Dat is verschrikkelijke UX."

**Developer:** "Zo heb ik het gebouwd. Geen bug."

**Oplossing:**

**1. Check acceptance criteria:**
- Als AC zegt "maak formulier leeg bij fout" → Geen bug, maar je kunt UX verbetering voorstellen
- Als AC is stil → Verduidelijk met Product Owner

**2. Escaleer naar Product Owner:**

> "PO, wanneer gebruiker ongeldige datum invoert, maakt het formulier alle velden leeg. Gebruikers moeten alles opnieuw invoeren. Is dit bedoeld gedrag? Ik denk dat het UX schaadt."

**PO beslist:**
- "Ja, bedoeld" → Geen bug, accepteer (of stel verbetering voor later voor)
- "Nee, niet bedoeld" → Het is een bug, developer fixt

**3. Onderscheid bug vs verbetering:**
- **Bug:** Voldoet niet aan acceptance criteria of DoD
- **Verbetering:** Werkt zoals gespecificeerd, maar zou beter kunnen

Log verbeteringen als "Enhancement" niet "Bug" - bespreek prioritering met PO.

### Uitdaging 4: "Ik weet niet hoe ik deze technische feature moet testen"

**Voorbeeld:** Story over "Implementeer caching voor API responses" - erg technisch, onduidelijk hoe van buitenaf te testen.

**Oplossing:**

**1. Vraag developer om uit te leggen:**

> "Ik weet niet zeker hoe ik de caching feature moet testen. Kun je me laten zien hoe het werkt en wat ik moet verifiëren?"

**Developer toont:** "Wanneer je /api/requests aanroept, duurt eerste call 500ms. Tweede call duurt 10ms. Dat is caching die werkt."

**Tester:** "Begrepen! Ik test: 
- Eerste call is traag (cache miss)
- Tweede call is snel (cache hit)
- Na cache verloopt (5 min), is call weer traag
- Gecachte data komt overeen met verse data"

**2. Pair test met developer:**
- Developer loopt door technische implementatie
- Tester stelt vragen, leert, test samen
- Samen verifiëren dat het werkt

**3. Focus op waarneembaar gedrag:**
- Je hoeft code niet te begrijpen
- Je moet verifiëren: Doet het wat het moet doen?
- Gebruik developer tools (browser console, network tab) om te observeren

---

## Testtools & Technieken

### Browser Developer Tools

**Essentieel voor testen:**

**Chrome DevTools (F12):**
- **Console:** Zie JavaScript fouten
- **Network:** Zie API calls, response times, statuscodes
- **Application:** Check cookies, localStorage, session data
- **Elements:** Inspecteer HTML/CSS

**Voorbeeld gebruik:**
- API call testen: Network tab → zie of POST /api/requests 200 OK retourneert
- Error handling testen: Console → zie of fout duidelijk gelogd is
- Caching testen: Network tab → zie of tweede call uit cache komt

### Schermopname voor Bug Reports

**Tools:**
- Windows: Xbox Game Bar (Win+G)
- Mac: QuickTime Screen Recording
- Browser extensie: Loom

**Wanneer gebruiken:**
- Bug is moeilijk in woorden te beschrijven
- Bug betreft animatie of timing
- Reeks van acties tonen
- UX issue demonstreren

### Testdata Beheer

**Maak herbruikbare testaccounts:**

**Voorbeelden:**
- `test.employee@example.com` - Standaard medewerker
- `test.manager@example.com` - Manager rol
- `test.admin@example.com` - Admin rol
- `test.edge.case@example.com` - Account met 100+ verzoeken voor limiet testen

**Documenteer testdata:**
- Houd lijst bij van testaccounts en hun doelen
- Deel met team (iedereen kan gebruiken voor testen)
- Reset/clean data regelmatig

### Exploratory Testing

**Niet al het testen moet gescript zijn. Soms gewoon exploreren:**

**Techniek:**
- Kies een feature
- Gebruik het zoals een echte gebruiker zou doen
- Probeer willekeurige dingen
- Zie wat breekt

**Voorbeeld sessie (15 minuten):**
- "Laat me proberen 10 verzoeken tegelijk in te dienen"
- "Wat als ik deze pagina bookmark en morgen terugkom?"
- "Wat als ik venster echt klein maak?"
- "Wat als ik browser terug knop gebruik mid-flow?"

**Documenteer bevindingen:** Zelfs als je geen bugs vindt, noteer "Verkende X feature, geen issues"

---

## Snelle Referentie Checklists

### Sprint 0 Checklist

- [ ] Lees Product Vision en begrijp product
- [ ] Bekijk Product Backlog user stories
- [ ] Begrijp GDPR vereisten
- [ ] Zet testomgeving op (VPS toegang, testaccounts)
- [ ] Neem deel aan opstellen Definition of Done (voeg testperspectief toe)
- [ ] Neem deel aan beoordeling Definition of Ready
- [ ] Woon backlog refinement bij - vraag "Hoe testen we dit?"
- [ ] Maak testdata voor Sprint 1
- [ ] Zet bug tracking aanpak op in Jira

### Sprint Planning Checklist

- [ ] Luister naar story discussies
- [ ] Vraag "Hoe testen we dit?" voor complexe stories
- [ ] Identificeer testafhankelijkheden (testdata, omgevingen, toegang)
- [ ] Noteer edge cases en failure scenarios
- [ ] Zorg dat testinspanning deel is van team's schatting
- [ ] Bevestig dat je stories in sprint kunt toegang/testen

### Dagelijkse Test Checklist

- [ ] Woon Daily Standup bij - rapporteer teststatus
- [ ] Check Jira voor stories gemarkeerd "Ready for Testing"
- [ ] Test stories zodra ze klaar zijn (wacht niet)
- [ ] Log bugs onmiddellijk met heldere reproductiestappen
- [ ] Hertest gefixte bugs binnen 24 uur
- [ ] Update Jira status (verplaats naar Done of terug naar In Progress)
- [ ] Communiceer bevindingen naar team (Standup of direct)

### Story Test Checklist

Bij het testen van een story:

- [ ] Lees acceptance criteria grondig
- [ ] Test happy path (geldige inputs, verwachte flow)
- [ ] Test validatie (lege velden, ongeldige formaten)
- [ ] Test edge cases (grenswaarden, speciale karakters)
- [ ] Test error handling (netwerkfouten, serverfouten)
- [ ] Test integratie (werkt het met andere features?)
- [ ] Check GDPR compliance (als persoonlijke data betrokken)
- [ ] Verifieer dat Definition of Done gehaald is
- [ ] Documenteer testresultaten
- [ ] Markeer story Done of log bugs

### Sprint Review Checklist

- [ ] Verifieer dat alle "Done" stories echt aan DoD voldoen
- [ ] Voer volledige regressietest uit op geïntegreerd increment
- [ ] Bereid kwaliteitssamenvatting voor (stories getest, bugs gevonden/gefixt)
- [ ] Documenteer bekende issues die nog niet gefixt zijn
- [ ] Wees klaar om kwaliteitsrisico's te bespreken
- [ ] Demo eventuele testtools of technieken gebruikt (indien relevant)

### Sprint Retrospective Checklist

- [ ] Reflecteer op wat goed werkte in testproces
- [ ] Identificeer test bottlenecks of problemen
- [ ] Suggereer verbeteringen aan testaanpak
- [ ] Bespreek kwaliteitsproblemen en grondoorzaken
- [ ] Commit aan specifieke testverbeteringen volgende sprint

---

## Tips voor Succes

### 1. Test Vroeg, Test Vaak

**Wacht niet.** Test incrementeel zodra features klaar zijn.

**Workflow:**
- Developer rondt feature af → Jij test binnen uren → Geef feedback
- Snelle feedback = Minder rework = Betere kwaliteit

### 2. Denk Als Gebruiker EN Als Hacker

**Als gebruiker:** "Hoe gebruiken echte mensen dit? Wat zal hen verwarren?"

**Als hacker:** "Hoe kan ik dit kapotmaken? Welke edge cases misten we?"

**Beide perspectieven vinden verschillende bugs.**

### 3. Communiceer Helder

**Goede communicatie:**
- Bug reports: Helder, specifiek, reproduceerbaar
- Status updates: "Story X is getest en Done" of "Story Y heeft 2 bugs"
- Risico's: "Feature Z is complex, ik heb extra tijd nodig om te testen"

**Slechte communicatie:**
- "Er is iets kapot"
- "Ik ben nog aan het testen"
- Stilte

### 4. Wees Samenwerkend, Niet Vijandig

**Jij en developers zijn in hetzelfde team.**

**Goede tester:**
- "Issue gevonden, laten we het samen fixen"
- "Goed gedaan! Deze feature had nul bugs"
- "Hoe kan ik je helpen dit te testen?"

**Slechte tester:**
- "Dit is compleet kapot, waar dacht je aan?"
- "Afgekeurd, fix het"
- "Niet mijn probleem"

### 5. Focus op Preventie, Niet Alleen Detectie

**Preventie (Best):**
- Vraag "Hoe testen we dit?" in refinement
- Help developers edge cases vroeg te begrijpen
- Review designs voor coderen

**Detectie (Goed):**
- Vind bugs tijdens sprint
- Snelle feedback naar developers

**Late detectie (Slechtst):**
- Vind bugs in Sprint Review
- Vind bugs in productie

### 6. Documenteer Je Bevindingen

**Houd bij:**
- Uitgevoerde testscenario's
- Bugs gevonden en gefixt
- Bekende issues nog open
- Gebruikte testdata

**Waarom:** Team kan leren van je testaanpak, tests later repliceren.

### 7. Laat Perfect Niet de Vijand van Goed Zijn

**Je kunt niet alles perfect testen.**

**Prioriteer:**
- Kritieke features grondig
- Secundaire features adequaat
- Kleine features licht

**Het is oké om te zeggen:** "Ik testte kernflows diep, deed smoke test op secundaire features."

---

## Hulp Krijgen

### Wanneer Developers Vragen

- **Hoe technische features te testen:** "Hoe werkt caching? Wat moet ik verifiëren?"
- **Hoe bugs te reproduceren:** "Ik zag dit één keer, maar kan niet reproduceren. Ideeën?"
- **Testomgeving problemen:** "API retourneert 500 fouten. Is testserver down?"

### Wanneer Product Owner Vragen

- **Onduidelijke vereisten:** "AC specificeert niet - moeten ongeldige datums formulier legen?"
- **Is dit bug of feature:** "Formulier reset bij fout. Is dit bedoeld?"
- **Prioriteitsvragen:** "Ik vond 5 bugs. Welke moeten developers eerst fixen?"

### Wanneer Scrum Master Vragen

- **Procesvragen:** "Moet ik testen tijdens Sprint Planning?"
- **Team samenwerkingsproblemen:** "Developers fixen bugs niet. Kun je helpen?"
- **Workflow vragen:** "Hoe moeten we Jira gebruiken voor bug tracking?"

### Wanneer Staff Vragen

- **GDPR onzekerheid:** "Is dit persoonlijke data? Hebben we speciale behandeling nodig?"
- **Beveiligingszorgen:** "Ik vond dat gebruikers data van anderen kunnen zien. Hoe ernstig is dit?"
- **Kwaliteitsnormen:** "Wat is onze acceptabele bug drempel?"

---

## Onthoud

**Je bent aan het leren.** Niemand verwacht perfect testen in Sprint 1.

**Goede Testers:**
- Testen vroeg en vaak (niet alleen aan het eind)
- Communiceren helder (bugs, status, risico's)
- Werken samen met team (help bugs voorkomen)
- Denken verder dan checklist (edge cases, echt gebruik)
- Focussen op hoogwaardige testen (risicogebaseerde prioriteiten)

**Je hoeft niet:**
- Elk mogelijk scenario te testen (onmogelijk)
- Alle technische details te begrijpen (focus op gedrag)
- Alleen te werken (samenwerken met developers)
- Perfect te zijn (continue verbetering)

**Jouw succes = Team levert hoogwaardige software die betrouwbaar werkt en aan gebruikersbehoeften voldoet.**

---

**Vragen?** Vraag je Scrum Master, developers, of mede-testers.

**EINDE VAN TESTER/QA ROLGIDS**
