---
Document: EAP_Product_Vision
Version: 1.1
Status: Draft
Audience: Interns + Staff
Approval required: Yes (Product Owner)
Changes from v1.0: Added GDPR/Privacy compliance section
Taal: Nederlands (vertaling van v1.1)
---

# Enterprise Application Project (EAP) - Product Vision

**Versie:** 1.0
**Datum:** 2026-01-06
**Eigenaar:** Product Owner (stagiairsrol)
**Goedgekeurd door:** Staff

---

## Samenvatting

Het Enterprise Application Project (EAP) is een webgebaseerd aanvraagbeheersysteem dat is ontworpen om medewerkeraanvragen voor middelen, toegang en diensten binnen een organisatie te stroomlijnen.

Het systeem biedt een gestructureerde workflow voor het indienen, beoordelen, goedkeuren en volgen van aanvragen, met duidelijke audit trails en geautomatiseerde meldingen.

**Doelgroep:** Organisaties die medewerkeraanvragen voor hardware, software, toegangsrechten en andere bedrijfsmiddelen willen beheren.

---

## Visie

> **"Medewerkers in staat stellen efficiënt middelen aan te vragen, terwijl managers inzicht en controle over goedkeuringen hebben, alles binnen een transparant en auditeerbaar systeem."**

---

## Het probleem dat we oplossen

### Huidige situatie (zonder EAP)

Organisaties verwerken medewerkeraanvragen doorgaans via:
- **E-mailketens** - Moeilijk te volgen, makkelijk te verliezen, geen audit trail
- **Spreadsheets** - Handmatige updates, geen automatisering, foutgevoelig
- **Ad-hoc processen** - Inconsistent, afhankelijk van wie je kent
- **Papieren formulieren** - Traag, niet schaalbaar, moeilijk te archiveren

**Pijnpunten:**
- 😞 Medewerkers weten niet wat de status van hun aanvraag is
- 😞 Managers verliezen het overzicht over openstaande goedkeuringen
- 😞 Geen inzicht in aanvraaghistorie
- 😞 Moeilijk te controleren wie wat heeft goedgekeurd
- 😞 Geen gestandaardiseerd proces per afdeling
- 😞 Tijdverlies door follow-ups en statuscontroles

### Toekomstige situatie (met EAP)

Met het EAP-systeem:
- ✅ **Self-service portal** voor medewerkers om aanvragen in te dienen
- ✅ **Geautomatiseerde routing** naar de juiste Approvers
- ✅ **Realtime status** zichtbaar voor alle betrokkenen
- ✅ **E-mailmeldingen** bij elke stap in de workflow
- ✅ **Volledige audit trail** van alle acties
- ✅ **Gestandaardiseerd proces** door de hele organisatie
- ✅ **Dashboard** voor managers en admins

---

## Kernproces

Het EAP-systeem implementeert een driestappe workflow:

```
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│   STAP 1:       │      │   STAP 2:       │      │   STAP 3:       │
│   Indienen      │  →   │   Goedkeuren    │  →   │   Uitvoeren     │
│                 │      │                 │      │                 │
│ Medewerker vult │      │ Manager/Admin   │      │ Aanvraag wordt  │
│ aanvraagformul. │      │ beoordeelt en   │      │ uitgevoerd en   │
│ in              │      │ goed-/afkeurt   │      │ afgesloten      │
└─────────────────┘      └─────────────────┘      └─────────────────┘
        ↓                        ↓                        ↓
    Ingediend            In beoordeling / Goedgekeurd   Voltooid
```

### Workflowstatussen

| Status | Omschrijving | Wie kan handelen |
|--------|-------------|-----------------|
| **Concept** | Aanvraag wordt aangemaakt | Requester |
| **Ingediend** | Wacht op beoordeling | Systeem (automatische routing naar Approver) |
| **In beoordeling** | Wordt beoordeeld | Approver |
| **Goedgekeurd** | Goedgekeurd, wacht op uitvoering | Admin/Uitvoerder |
| **Afgewezen** | Geweigerd met reden | - (eindstatus) |
| **Voltooid** | Uitgevoerd en afgesloten | - (eindstatus) |
| **Geannuleerd** | Geannuleerd door Requester | - (eindstatus) |

---

## Gebruikersrollen

### 1. Requester (Medewerker)

**Wie:** Elke medewerker in de organisatie

**Mogelijkheden:**
- Nieuwe aanvragen indienen
- Eigen aanvraaghistorie bekijken
- Status van openstaande aanvragen volgen
- E-mailmeldingen ontvangen bij statuswijzigingen
- Eigen openstaande aanvragen annuleren (vóór goedkeuring)
- Opmerkingen/aanvullende informatie toevoegen aan aanvragen

**Gebruiksvoorbeelden:**
- "Ik heb een nieuwe laptop nodig voor ontwikkelwerk"
- "Ik heb toegang nodig tot de productieomgeving"
- "Ik heb een softwarelicentie nodig voor Adobe Creative Suite"

---

### 2. Approver (Manager/Teamlead)

**Wie:** Managers, teamleads, budgetverantwoordelijken

**Mogelijkheden:**
- Alle aanvragen bekijken die hun goedkeuring vereisen
- Aanvragen goed- of afkeuren
- Goedkeuringscommentaar toevoegen (reden voor afkeuring, voorwaarden, etc.)
- Aanvraagdetails en informatie over de Requester bekijken
- E-mailmeldingen ontvangen bij nieuwe aanvragen
- Goedkeuringshistorie bekijken (wat ze hebben goedgekeurd/afgewezen)

**Beslissingscriteria:**
- Beschikbaarheid van budget
- Zakelijke rechtvaardiging
- Naleving van beleid
- Beschikbaarheid van middelen

---

### 3. Admin (Systeembeheerder)

**Wie:** IT-admins, HR-admins, facilitair managers

**Mogelijkheden:**
- Alle aanvragen in het systeem bekijken
- Gebruikersaccounts en rollen beheren
- Aanvraagtypen en workflows configureren
- Rapporten en analyses genereren
- Aanvragen markeren als uitgevoerd/voltooid
- Workflows overschrijven (indien nodig voor uitzonderingen)
- Systeeminstellingen beheren

**Verantwoordelijkheden:**
- Systeemconfiguratie
- Gebruikersbeheer
- Coördinatie van uitvoering
- Audit en compliance

---

## Aanvraagtypen (voorbeelden)

Het systeem ondersteunt verschillende soorten aanvragen. Voorbeelden:

### Hardwareaanvragen
- **Laptop/Desktop** - Nieuwe computer voor medewerker
- **Monitor** - Extra beeldscherm
- **Randapparatuur** - Toetsenbord, muis, headset, webcam
- **Mobiel apparaat** - Zakelijke telefoon of tablet

### Software & Toegang
- **Softwarelicentie** - Adobe, Microsoft Office, ontwikkeltools
- **Systeemtoegang** - Productieomgeving, beheerdersrechten
- **Applicatietoegang** - CRM, ERP, interne tools
- **VPN-toegang** - Connectiviteit voor thuiswerken

### Diensten & Faciliteiten
- **Parkeerplaats** - Gereserveerd parkeren
- **Kantoorinrichting** - Bureau, stoel, zit-sta bureau
- **Training** - Cursusinschrijving, conferentiedeelname
- **Reisgoedkeuring** - Autorisatie voor zakenreis

**Opmerking:** De Product Owner bepaalt de initiële set aanvraagtypen tijdens Sprint 1. Het systeem moet zo worden ontworpen dat nieuwe typen eenvoudig kunnen worden toegevoegd.

---

## Kernfuncties (MVP)

### Voor Requesters

**1. Aanvraagformulier**
- Aanvraagtype selecteren uit dropdown
- Verplichte velden invullen (omschrijving, zakelijke onderbouwing, etc.)
- Bijlagen toevoegen (optioneel)
- Indienen voor goedkeuring

**2. Aanvraagdashboard**
- Alle eigen aanvragen bekijken (heden en verleden)
- Huidige status in één oogopslag zien
- Filteren op status (In behandeling, Goedgekeurd, Afgewezen, Voltooid)
- Sorteren op datum, type, status

**3. Statusopvolging**
- Realtime statusupdates
- Tijdlijnweergave van de voortgang van een aanvraag
- Zien wie heeft goedgekeurd/afgewezen en wanneer
- Goedkeuringscommentaar lezen

**4. Meldingen**
- E-mailmelding bij statuswijziging
- Herinnering als actie vereist is
- Bevestiging bij indiening

---

### Voor Approvers

**1. Goedkeuringswachtrij**
- Lijst van aanvragen die wachten op goedkeuring
- Indicatoren voor prioriteit/urgentie
- Voorvertoning van aanvraagdetails
- Snelle goed-/afkeuracties

**2. Aanvraagdetailweergave**
- Volledige aanvraaginformatie
- Gegevens van de Requester en diens historie
- Zakelijke onderbouwing
- Kostenimplicaties (indien van toepassing)

**3. Goedkeuringsacties**
- Goedkeuren met commentaar
- Afwijzen met verplichte reden
- Aanvullende informatie opvragen
- Doorsturen naar andere Approver

**4. Goedkeuringshistorie**
- Bijhouden wat ik heb goedgekeurd/afgewezen
- Patronen en trends inzien
- Exporteren voor rapportage

---

### Voor Admins

**1. Admin Dashboard**
- Systeembrede statistieken
- Aantal openstaande aanvragen
- Knelpunten in goedkeuringen
- Trends in aanvraagvolume

**2. Gebruikersbeheer**
- Gebruikers toevoegen/verwijderen
- Rollen toewijzen (Requester, Approver, Admin)
- Goedkeuringshiërarchieën beheren
- Gebruikers deactiveren

**3. Systeemconfiguratie**
- Aanvraagtypen definiëren
- Goedkeuringsworkflows configureren
- Meldingssjablonen instellen
- Systeeminstellingen beheren

**4. Rapportage & Analyse**
- Aanvragen per type, status, tijdsperiode
- Goedkeuringstijden (gemiddeld, mediaan)
- Identificatie van knelpunten
- Gebruikersactiviteitsrapporten
- Exporteren naar Excel/PDF

**5. Audit Trail**
- Volledige historie van alle acties
- Wie wat heeft gedaan en wanneer
- Zoek- en filtermogelijkheden
- Compliance-rapportage

---

## Niet-functionele vereisten

### Prestaties
- Laadtijd pagina < 2 seconden
- Reactietijd bij formulierindiening < 1 seconde
- Ondersteuning voor 100 gelijktijdige gebruikers (initieel doel)
- Databasequery-optimalisatie voor grote datasets

### Beveiliging
- Role-based access control (RBAC)
- Veilige authenticatie (OAuth2/JWT)
- HTTPS voor alle communicatie
- Invoervalidatie en -sanitisatie
- Bescherming tegen SQL-injectie
- XSS-bescherming

### Bruikbaarheid
- Mobiel-responsief ontwerp
- Intuïtieve navigatie
- Consistente UI-patronen
- Duidelijke foutmeldingen
- Behulpzame tooltips en begeleiding
- Toegankelijkheid (WCAG 2.1 niveau AA)

### Betrouwbaarheid
- 99% uptime tijdens kantooruren
- Geautomatiseerde back-ups (dagelijks)
- Foutregistratie en monitoring
- Elegante foutafhandeling
- Rollback-mogelijkheid bij deployments

### Onderhoudbaarheid
- Schone, gedocumenteerde code
- Geautomatiseerde tests (unit, integratie, e2e)
- CI/CD pipeline
- Versiebeheer (Git)
- ADR-documentatie voor beslissingen

### Privacy & AVG-naleving

**Persoonsgegevens die we verwerken:**
- Namen en e-mailadressen van medewerkers
- Aanvraagdetails en onderbouwingen (kunnen gevoelige informatie bevatten)
- Goedkeuringsbeslissingen en commentaar
- Audit trail (wie heeft wat gedaan en wanneer)
- Gebruikersrollen en rechten

**AVG-vereisten:**

**Rechtmatige grondslag:**
- Gerechtvaardigd belang (interne bedrijfsvoering)
- Staff raadpleegt de Functionaris Gegevensbescherming (FG) of juridische afdeling van de organisatie ter bevestiging van de rechtmatige grondslag

**Kernprincipes:**
- **Dataminimalisatie:** Alleen gegevens verzamelen die noodzakelijk zijn voor aanvraagverwerking
- **Doelbinding:** Gegevens uitsluitend gebruikt voor aanvraagbeheer, niet voor andere doeleinden
- **Opslagbeperking:** Retentiebeleid definiëren en implementeren
- **Integriteit en vertrouwelijkheid:** Veilige opslag en toegangscontroles

**Rechten van betrokkenen:**
- **Recht op inzage:** Gebruikers kunnen hun eigen aanvraaghistorie bekijken
- **Recht op verwijdering:** Anonimiseringsaanpak voor gesloten aanvragen (audit trail behouden, persoonsgegevens verwijderen)
- **Recht op gegevensoverdraagbaarheid:** Exportfunctionaliteit voor eigen gegevens
- **Recht op rectificatie:** Gebruikers kunnen hun eigen gegevens bijwerken

**Technische implementatie:**
- Persoonsgegevens scheiden van audit trail (anonimisering mogelijk zonder auditcapaciteit te verliezen)
- Configureerbaar retentiebeleid (bijv. anonimiseren na 2 jaar)
- Gebruikersgegevens-exportfunctionaliteit (JSON/CSV-formaat)
- Anonimiseringsmogelijkheid voor gesloten aanvragen (namen vervangen door "Gebruiker [ID]")
- Privacy-bewuste logging (geen gevoelige aanvraagdetails in applicatielogs)
- Toegangscontroles voorkomen ongeautoriseerde inzage in persoonsgegevens

**Buiten scope voor MVP:**
- Formele Gegevensbeschermingseffectbeoordeling (DPIA) – verantwoordelijkheid van staff
- Privacy-dashboard voor eindgebruikers
- Geautomatiseerde workflows voor gegevensverwijdering
- Toestemmingsbeheersysteem
- Overeenkomsten met externe gegevensverwerkers
- Mechanismen voor grensoverschrijdende gegevensoverdracht

**Verantwoordelijkheden van staff:**
- FG/juridische consultatie vóór Sprint 1 (bevestiging rechtmatige grondslag, retentietermijn)
- AVG-vereisten verstrekken aan Product Owner
- Architecture beoordelen op AVG-naleving
- Retentie- en anonimiseringsbeleid goedkeuren

**Verantwoordelijkheden van het team:**
- AVG-aanpak documenteren in ADR (bijv. ADR-004: AVG-nalevingsaanpak)
- Privacy by design implementeren vanaf Sprint 1
- Privacy-review opnemen in Definition of Done
- Databaseschema ontwerpen met anonimisering in gedachten

**Opmerking:** De Product Owner ontvangt AVG-vereisten van staff/FG vóór Sprint Planning. Het team is verantwoordelijk voor de technische implementatie, staff is verantwoordelijk voor juridische naleving.

---

## User Stories (voorbeelden)

### Epic: Aanvraag indienen

**US-001: Hardware aanvragen**
```
Als medewerker
wil ik een aanvraag indienen voor een nieuwe laptop,
zodat ik de apparatuur krijg die ik nodig heb voor mijn werk.

Acceptatiecriteria:
- Ik kan "Laptop" selecteren uit het dropdown-menu voor aanvraagtype
- Ik kan laptopspecificaties opgeven (processor, RAM, opslag)
- Ik kan een zakelijke onderbouwing opgeven
- Ik ontvang een bevestigingsmail na indiening
- De aanvraag verschijnt in mijn dashboard met de status "Ingediend"
```

**US-002: Aanvraagstatus volgen**
```
Als medewerker
wil ik de huidige status van mijn aanvragen zien,
zodat ik weet of mijn aanvraag in behandeling is.

Acceptatiecriteria:
- Ik kan al mijn aanvragen bekijken in een dashboard
- Elke aanvraag toont de huidige status (Ingediend, In beoordeling, Goedgekeurd, etc.)
- Ik kan zien wie mijn aanvraag momenteel beoordeelt
- Ik kan de tijdstempel van de laatste statuswijziging zien
```

---

### Epic: Aanvraag goedkeuren

**US-010: Aanvraag goed-/afkeuren**
```
Als manager
wil ik aanvragen van mijn team beoordelen en goed- of afkeuren,
zodat ik de toewijzing van middelen kan bewaken.

Acceptatiecriteria:
- Ik zie een lijst van aanvragen die wachten op mijn goedkeuring
- Ik kan volledige aanvraagdetails bekijken inclusief onderbouwing
- Ik kan met één klik goedkeuren
- Ik kan afwijzen met een verplichte reden
- De Requester ontvangt een e-mailmelding van mijn beslissing
```

**US-011: Goedkeuringswachtrij beheren**
```
Als manager
wil ik alle openstaande goedkeuringen op één plek zien,
zodat ik meerdere aanvragen efficiënt kan verwerken.

Acceptatiecriteria:
- Dashboard toont het aantal openstaande goedkeuringen
- Ik kan sorteren op datum, prioriteit, Requester
- Ik kan filteren op aanvraagtype
- Ik kan vergelijkbare aanvragen bulksgewijs goedkeuren (stretch goal)
```

---

### Epic: Systeembeheer

**US-020: Gebruikersbeheer**
```
Als admin
wil ik nieuwe gebruikers toevoegen en rollen toewijzen,
zodat het systeem onze organisatiestructuur weerspiegelt.

Acceptatiecriteria:
- Ik kan nieuwe gebruikersaccounts aanmaken
- Ik kan rollen toewijzen (Requester, Approver, Admin)
- Ik kan gebruikers deactiveren die de organisatie verlaten
- Ik kan gebruikersinformatie bijwerken
```

**US-021: Rapporten genereren**
```
Als admin
wil ik rapporten genereren over aanvraagactiviteit,
zodat ik trends kan analyseren en knelpunten kan identificeren.

Acceptatiecriteria:
- Ik kan een rapport genereren voor een datumbereik
- Het rapport toont aanvragen per type, status, Approver
- Ik kan het rapport exporteren naar Excel
- Het rapport bevat de gemiddelde goedkeuringstijd
```

---

## Buiten scope (niet in MVP)

De volgende functies zijn **NIET** opgenomen in de initiële release:

❌ **Meervoudige goedkeuringen** - Slechts één Approver per aanvraag (geen goedkeuringsketens)
❌ **Budgetbeheer** - Geen integratie met financiële systemen
❌ **Activabeheer** - Geen opvolging van fysieke activa na uitvoering
❌ **SLA-beheer** - Geen automatische escalatie op basis van tijd
❌ **Geavanceerde workflows** - Geen conditionele routing op basis van aanvraagdetails
❌ **Mobiele apps** - Alleen web (responsief ontwerp, geen native apps)
❌ **Integraties** - Geen integratie met externe systemen (Slack, JIRA, etc.)
❌ **Realtime chat** - Geen in-app berichten tussen gebruikers
❌ **Goedkeuringsdelegatie** - Approvers kunnen niet delegeren aan anderen
❌ **Terugkerende aanvragen** - Geen sjablonen voor herhaalde aanvragen

**Opmerking:** Deze functies kunnen worden overwogen voor toekomstige releases op basis van gebruikersfeedback en zakelijke prioriteiten.

---

## Succesindicatoren

Hoe weten we dat het EAP succesvol is?

### Gebruiksstatistieken
- **Adoptiegraad:** 80% van de medewerkers dient minimaal één aanvraag in de eerste 3 maanden
- **Actieve gebruikers:** 50+ actieve gebruikers per week
- **Aanvraagvolume:** 100+ verwerkte aanvragen per maand

### Prestatiestatistieken
- **Gemiddelde goedkeuringstijd:** < 48 uur van indiening tot goedkeuring
- **Tijd tot uitvoering:** < 5 werkdagen van goedkeuring tot voltooiing
- **Systeembeschikbaarheid:** 99% tijdens kantooruren

### Kwaliteitsstatistieken
- **Gebruikerstevredenheid:** Gemiddelde beoordeling 4/5 of hoger
- **Afwijzingspercentage:** < 10% van de aanvragen afgewezen
- **Bugmeldingen:** < 5 kritieke bugs per Sprint

### Processtatistieken
- **E-mailreductie:** 70% minder e-mails over aanvraagstatus
- **Tijdsbesparing admin:** 20% minder beheerderstijd besteed aan het bijhouden van aanvragen
- **Auditcompliance:** 100% van de aanvragen heeft een volledige audit trail

---

## Technologische beperkingen

Op basis van **eap-architecture ADR-002: Technology Stack** (nog te documenteren) maakt het systeem gebruik van:

**Backend:**
- Python 3.11+
- FastAPI framework
- PostgreSQL database
- SQLAlchemy ORM
- Alembic voor migraties

**Frontend:**
- React 18
- TypeScript
- Moderne componentbibliotheek (te bepalen door het team)

**Infrastructuur:**
- Docker containers
- GitHub Actions voor CI/CD
- TransIP VPS voor deployment

**API:**
- RESTful API-ontwerp
- OpenAPI/Swagger-specificatie
- JWT voor authenticatie

---

## Product Roadmap (voorlopig)

### Sprint 1-2: Fundament (weken 1-4)
- Gebruikersauthenticatie en autorisatie
- Basis aanvraagindiening (één aanvraagtype)
- Eenvoudige goedkeuringsworkflow
- E-mailmeldingen
- Basisdashboard

### Sprint 3-4: Kernfuncties (weken 5-8)
- Meerdere aanvraagtypen
- Aanvraaghistorie en opvolging
- Admin gebruikersbeheer
- Statusupdates en commentaar
- Uitgebreide dashboards

### Sprint 5-6: Afwerking & Schaling (weken 9-12)
- Rapportage en analyse
- Prestatieoptimalisatie
- Verbeterde UI/UX
- Volledige audit trail
- Documentatie en trainingsmateriaal

**Opmerking:** Deze roadmap is flexibel en wordt door de Product Owner bijgesteld op basis van teamsnelheid en feedback van stakeholders.

---

## Stakeholders

### Primaire stakeholders
- **Product Owner (stagiair)** - Definieert en prioriteert functies
- **Ontwikkelteam (stagiairs)** - Bouwt en levert het systeem
- **Eindgebruikers** - Medewerkers die het systeem zullen gebruiken (vertegenwoordigd door Product Owner)

### Secundaire stakeholders
- **Staff/Coaches** - Bieden begeleiding en beoordelen leeruitkomsten
- **Organisatie** - Profiteert van gestroomlijnd aanvraagproces
- **IT-afdeling** - Potentiële toekomstige beheerders van het systeem

---

## Verantwoordelijkheden Product Owner

De Product Owner (stagiairsrol) is verantwoordelijk voor:

✅ **Deze visie uitwerken** in gedetailleerde user stories
✅ **De Product Backlog prioriteren** op basis van bedrijfswaarde
✅ **Acceptatiecriteria definiëren** voor elke user story
✅ **Scopebeslissingen nemen** wanneer afwegingen nodig zijn
✅ **Gebruikersbehoeften vertegenwoordigen** in alle besprekingen
✅ **Voltooid werk accepteren of afwijzen** in Sprint Reviews
✅ **Dit document bijwerken** naarmate de visie evolueert (met teaminput)

**Rol van staff:** Staff coacht en daagt de Product Owner uit, maar neemt geen productbeslissingen.

---

## Ontwerpprincipes

Het EAP-systeem moet deze principes belichamen:

1. **Gebruikersgericht** - Ontwerpen voor eindgebruikers, niet voor admins
2. **Transparant** - Iedereen kan status en historie zien
3. **Efficiënt** - Minimaal aantal klikken en wachttijd
4. **Betrouwbaar** - Geen verloren aanvragen, volledige audit trail
5. **Eenvoudig** - Eenvoudige oplossingen verkiezen boven complexe functies
6. **Veilig** - Gebruikersgegevens beschermen en ongeautoriseerde toegang voorkomen
7. **Onderhoudbaar** - Schone code, goede documentatie, geautomatiseerde tests

---

## Vragen & Verduidelijkingen

Dit gedeelte wordt bijgewerkt naarmate er vragen rijzen tijdens de ontwikkeling:

**V: Kan een Requester een aanvraag bewerken na indiening?**
A: Te bepalen door de Product Owner in Sprint 1. Initieel standpunt: Nee (Requester moet annuleren en opnieuw indienen).

**V: Wat gebeurt er als een Approver niet reageert?**
A: Buiten scope voor MVP. Geen automatische escalatie. Handmatige follow-up via e-mail.

**V: Kan een admin een goedkeuringsbeslissing overschrijven?**
A: Te bepalen door de Product Owner. Houd rekening met de gevolgen voor de audit trail.

**V: Hoe lang wordt aanvraaghistorie bewaard?**
A: Staff stelt een AVG-conform retentiebeleid op (bijv. 2 jaar, daarna anonimiseren). Product Owner implementeert deze vereiste.

**V: Hoe gaan we om met "recht op vergetelheid"-verzoeken?**
A: Anonimiseringsaanpak: vervang persoonsgegevens door "Gebruiker [ID]" met behoud van de audit trail-structuur. Staff/FG stelt specifieke vereisten op.

**V: Wat is de rechtmatige grondslag voor de verwerking van medewerkergegevens?**
A: Staff/FG bevestigt dit (waarschijnlijk: gerechtvaardigd belang voor interne bedrijfsvoering). Product Owner ontvangt deze informatie vóór Sprint 1.

---

## Referenties

- **Kickoff presentatie:** EAP_Kickoff_Presentation_v1.1.pptx (dia 4: Product Vision)
- **Project Initiation Document:** EAP_Project_Initiation_Document_Product_Focused_v1.0.md
- **Architecture repository:** eap-architecture (aan te maken in Sprint 1)
- **User Stories:** Uit te werken in Jira tijdens Sprint Planning

---

## Documenthistorie

| Versie | Datum | Wijzigingen | Auteur |
|--------|-------|-------------|--------|
| 1.0 | 2026-01-06 | Initieel product vision document | Staff (voor eigenaarschap door Product Owner) |
| 1.1 | 2026-01-06 | AVG/Privacy-nalevingssectie toegevoegd | Staff (voor eigenaarschap door Product Owner) |

---

## Volgende stappen

**Voor de Product Owner:**
1. Dit visiondocument in Sprint 1 met het team doornemen
2. Bijstellen en aanpassen op basis van teaminput
3. Uitwerken in gedetailleerde user stories in Jira
4. Initiële backlog prioriteren voor Sprint 1
5. Acceptatiecriteria definiëren voor elke story
6. Dit document bijwerken naarmate de visie evolueert

**Voor het ontwikkelteam:**
1. De product vision lezen en begrijpen
2. Verduidelijkende vragen stellen aan de Product Owner
3. Technische input geven over haalbaarheid
4. Helpen functies op te splitsen in implementeerbare stories
5. Aannames ter discussie stellen en verbeteringen voorstellen

---

**Documentbeheer**
- Aangemaakt: 2026-01-06
- Eigenaar: Product Owner (stagiairsrol)
- Goedgekeurd door: Staff
- Herzieningsfrequentie: Na elke Sprint (bijwerken indien nodig)
- Status: Levend document (evolueert gedurende het project)
