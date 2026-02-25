---
Document: Architecture_Decision_Record_Template
Version: 1.0
Status: Approved
Audience: Interns
Approval required: No
Taal: Nederlands (vertaling van v1.0)
---

# Architecture Decision Record (ADR) Template

## Wat is een ADR?

Een Architecture Decision Record documenteert een belangrijke architecturale of technische beslissing die tijdens het project is genomen, samen met de context en de gevolgen ervan.

ADRs helpen het team:
- te onthouden waarom beslissingen zijn genomen;
- te voorkomen dat afgeronde beslissingen opnieuw worden besproken;
- de afwegingen die zijn gemaakt te begrijpen;
- nieuwe teamleden in te werken;
- te leren van eerdere beslissingen.

**ADRs worden in Git opgeslagen** naast je code, omdat:
- beslissingen en code samen evolueren;
- Git-geschiedenis toont wanneer en waarom beslissingen zijn gewijzigd;
- Pull Request-discussies onderdeel worden van het besluitvormingsrecord;
- ADRs net als code worden versiebeheerd;
- iedereen met toegang tot de code de architecturale beslissingen kan inzien.

---

## Wanneer schrijf je een ADR

Schrijf een ADR wanneer:
- je kiest tussen meerdere haalbare technische alternatieven;
- je beslissingen neemt die later moeilijk of kostbaar zijn om te wijzigen;
- je afwijkt van gevestigde patronen of conventies;
- beslissingen significant van invloed zijn op niet-functionele vereisten (prestaties, beveiliging, schaalbaarheid);
- een beslissing meerdere onderdelen van het systeem beïnvloedt.

**Voorbeelden waarvoor een ADR vereist is:**
- Kiezen van een databaseschema-aanpak
- Selecteren van een API-authenticatiemethode
- Bepalen van een state management-strategie (frontend)
- Kiezen tussen REST en GraphQL
- Databasemigratiestrategie
- **AVG-nalevingsaanpak (dataretentie, anonimisering, gebruikersrechten)**
- **Privacy by design implementatie**

**Voorbeelden waarvoor geen ADR nodig is:**
- Naamgevingsconventies voor variabelen
- Individuele componentbestandsstructuur
- Kleine refactoringbeslissingen
- Aanpak voor bugfixes

Twijfel je? Vraag jezelf af: "Zouden toekomstige teamleden moeten begrijpen waarom we deze keuze hebben gemaakt?" Als het antwoord ja is, schrijf dan een ADR.

---

## ADR-proces

1. **Maak** het ADR-bestand aan in `/docs/architecture/decisions/` met het formaat: `ADR-XXX-korte-titel.md`
2. **Stel** het ADR op met de status "Proposed" en commit naar een feature branch
3. **Bespreek** met het team (Daily Scrum, Sprint Planning of een aparte sessie)
4. **Beoordeel** door minimaal 2 teamleden via Pull Request
5. **Werk bij** de status naar "Accepted" wanneer het team consensus bereikt
6. **Merge** het ADR naar de main/dev branch

**Git workflow:**
- ADRs worden opgeslagen in de Git-repository naast code
- Maak ADRs aan in feature branches, net als code
- Gebruik Pull Requests voor beoordeling en discussie
- Statuswijzigingen zijn nieuwe commits (behoudt geschiedenis in Git)
- Verwijder nooit ADRs — verander de status naar "Superseded"

**Belangrijk:** Elke statuswijziging moet worden gedocumenteerd in het gedeelte "Status History" onderaan het ADR, inclusief de datum en de reden voor de wijziging.

ADRs zijn **onveranderlijk** zodra ze geaccepteerd zijn. Als een beslissing verandert, maak dan een nieuw ADR dat het oude vervangt.

**Wat "onveranderlijk" betekent:**
- De **inhoud** (context, beslissing, redenering) kan na acceptatie niet worden bewerkt
- De **status** kan worden bijgewerkt (Accepted → Superseded of Deprecated)
- Kleine correcties (typefouten, opmaak) zijn toegestaan, maar geen wijzigingen in betekenis

**Waarom onveranderlijkheid belangrijk is:**
- Behoudt het historische record van waarom beslissingen zijn genomen
- Toont welke informatie beschikbaar was op het moment van de beslissing
- Maakt leren van eerdere beslissingen mogelijk
- Voorkomt het herschrijven van geschiedenis

---

## ADR Template

Kopieer het onderstaande template wanneer je een nieuw ADR aanmaakt:

```markdown
# ADR-XXX: [Decision Title]

**Repository:** [eap-architecture | eap-backend | eap-frontend | eap-qa]
**Date:** YYYY-MM-DD
**Status:** [Proposed | Accepted | Superseded | Deprecated]
**Deciders:** [Names of team members involved]
**Category:** [Platform Decision | Application Decision]

## Context

What is the issue or problem we're trying to solve?

- Describe the forces at play (technical, business, organizational)
- What requirements or constraints exist?
- What's the current situation?

Keep this section factual and neutral.

## Decision

What did we decide to do?

State the decision clearly and concisely. Use active voice:
- "We will use PostgreSQL for data persistence"
- "We will implement authentication using JWT tokens"

## Consequences

What are the results of this decision?

### Positive
- What benefits do we gain?
- What problems does this solve?
- What becomes easier?

### Negative
- What trade-offs are we accepting?
- What becomes harder?
- What risks are we taking on?

### Neutral
- What else changes as a result?
- What future decisions does this constrain?

## Alternatives Considered

What other options did we evaluate?

For each alternative:
1. **[Alternative name]**
   - Description
   - Why we chose not to pursue this
   - Key trade-offs vs. chosen decision

If no alternatives were seriously considered, explain why this decision was obvious.

## Constraints

List any constraints that limited our options:
- Platform constraints (e.g., "Must use PostgreSQL - platform requirement")
- Time constraints
- Budget constraints
- Technical constraints
- Team skill constraints

## Notes

Any additional context, references, or implementation notes:
- Links to relevant documentation
- Proof of concept results
- Performance benchmarks
- Examples from similar projects

## Related ADRs

### In this repository:
- List ADRs in this repository that are related to this decision

### In other repositories:
- Use full GitHub links when referencing ADRs from other repositories
- Example: [eap-architecture ADR-003: API Authentication](https://github.com/org/eap-architecture/blob/main/decisions/ADR-003-api-authentication.md)

---

**Last Updated:** YYYY-MM-DD
**Supersedes:** [ADR-XXX] (if applicable)
**Superseded By:** [ADR-XXX] (if applicable)

---

## Status History

Document all status changes here to maintain a complete audit trail:

| Date | Status | Reason |
|------|--------|--------|
| YYYY-MM-DD | Proposed | Initial draft |
| YYYY-MM-DD | Accepted | Team consensus reached in Sprint X Planning |
| YYYY-MM-DD | Superseded | Replaced by ADR-XXX due to [reason] |

---
```

---

## Voorbeeld-ADR

Hieronder een volledig voorbeeld:

```markdown
# ADR-001: Database Schema Versioning Strategy

**Repository:** eap-backend
**Date:** 2026-01-08
**Status:** Accepted
**Deciders:** Alice (DevOps lead), Bob (Backend dev), Carol (Product Owner)
**Category:** Application Decision

## Context

Our application needs a way to manage database schema changes across development,
testing, and production environments. Multiple developers will be creating database
changes simultaneously across different feature branches.

Requirements:
- Schema changes must be trackable and reversible
- Changes must be applied consistently across environments
- Changes must work with our Git Flow branching strategy
- Solution must integrate with our CI/CD pipeline

## Decision

We will use Alembic (SQLAlchemy migrations) for database schema versioning.

Migration files will be:
- Stored in `/backend/migrations/versions/`
- Generated using `alembic revision --autogenerate`
- Reviewed in pull requests before merging
- Applied automatically by CI/CD pipeline during deployment

## Consequences

### Positive
- Schema changes are version controlled alongside code
- Automatic migration generation reduces manual work
- Built-in rollback capability
- Wide adoption in Python/SQLAlchemy ecosystem
- Good integration with our testing pipeline

### Negative
- Autogenerate doesn't catch all schema changes (indexes, constraints sometimes missed)
- Requires discipline to review generated migrations
- Merge conflicts possible when multiple branches create migrations simultaneously
- Team needs to learn Alembic-specific commands

### Neutral
- Migration files become part of code review process
- Deployments take slightly longer (running migrations)
- Need to establish naming convention for migration files

## Alternatives Considered

1. **Raw SQL Migration Scripts**
   - Would give us more control over SQL
   - Rejected because: doesn't integrate well with SQLAlchemy ORM,
     no automatic generation, more manual work

2. **Django Migrations**
   - Excellent migration system
   - Rejected because: we're using FastAPI, not Django

3. **Flyway**
   - Industry standard for Java/enterprise
   - Rejected because: overkill for our project size, less Python-native

## Constraints

- Must work with PostgreSQL (platform requirement)
- Must work with SQLAlchemy (chosen ORM)
- Must integrate with GitHub Actions (CI/CD platform)

## Notes

- Alembic documentation: https://alembic.sqlalchemy.org/
- Team training session scheduled for Sprint 2
- Initial migration setup tracked in ticket EAP-15

## Related ADRs

### In this repository (eap-backend):
- None yet - this is the first backend-specific ADR

### In other repositories:
- [eap-architecture ADR-002: Technology Stack](https://github.com/org/eap-architecture/blob/main/decisions/ADR-002-tech-stack.md)

---

**Last Updated:** 2026-01-08

---

## Status History

| Date | Status | Reason |
|------|--------|--------|
| 2026-01-07 | Proposed | Initial draft by Alice |
| 2026-01-08 | Accepted | Team consensus in Sprint 1 Planning |

---
```

---

## ADR-nummering

ADRs worden sequentieel genummerd **binnen elke repository**: ADR-001, ADR-002, ADR-003, etc.

**Waarom sequentieel per repository in plaats van globale nummering of voorvoegsels?**

We hebben voor deze aanpak gekozen omdat:
1. **Industriestandaard** – Dit is hoe ADRs doorgaans worden genummerd in de bredere softwaregemeenschap
2. **Eenvoudig** – Geen coördinatie nodig tussen repositories om het volgende nummer te "claimen"
3. **Repository biedt natuurlijke scope** – De repositorynaam geeft al de scope aan (platform, backend, frontend, QA)
4. **Expliciete kruisverwijzingen** – Bij verwijzing naar ADRs uit andere repos moet je de repositorynaam vermelden, waardoor afhankelijkheden zichtbaar worden

**Dit betekent:**
- `ADR-001` bestaat in meerdere repositories (eap-architecture, eap-backend, eap-frontend, eap-qa)
- Elke repository behoudt zijn eigen sequentiële nummering
- Kruisverwijzingen moeten de repositorynaam bevatten

**Voorbeeld:**
- `eap-architecture/decisions/ADR-001-repository-strategy.md`
- `eap-backend/docs/decisions/ADR-001-database-schema.md`
- `eap-frontend/docs/decisions/ADR-001-state-management.md`

Dit zijn drie verschillende ADRs met hetzelfde nummer maar in verschillende scopes.

---

## ADR-organisatie per repository

### eap-architecture/decisions/
**Doel:** Beslissingen op platformniveau en cross-cutting

**Wanneer hier ADRs aanmaken:**
- Beslissingen die meerdere componenten beïnvloeden (backend + frontend + QA)
- Infrastructuur- en deploymentbeslissingen
- API-contracten en authenticatie
- Keuze van tech stack
- Beslissingen over ontwikkelworkflow

**Voorbeelden:**
- Repositorystrategie
- Selectie van tech stack
- API-authenticatieaanpak
- Deploymentstrategie
- Git workflow

### eap-backend/docs/decisions/
**Doel:** Backend-specifieke implementatiebeslissingen

**Wanneer hier ADRs aanmaken:**
- Beslissingen die alleen de backendcode beïnvloeden
- Implementatiedetails binnen backendbeperkingen
- Backend-specifieke patronen

**Voorbeelden:**
- Databaseschema-ontwerp
- ORM-gebruikspatronen
- Cachingstrategie
- Modulestructuur
- Verwerking van achtergrondtaken

### eap-frontend/docs/decisions/
**Doel:** Frontend-specifieke implementatiebeslissingen

**Wanneer hier ADRs aanmaken:**
- Beslissingen die alleen de frontendcode beïnvloeden
- Frontend-implementatiepatronen
- Technische UI/UX-beslissingen

**Voorbeelden:**
- State management-aanpak
- Keuze van componentenbibliotheek
- Routingstrategie
- Formulierafhandeling
- Client-side caching

### eap-qa/docs/decisions/
**Doel:** QA- en testspecifieke beslissingen

**Wanneer hier ADRs aanmaken:**
- Beslissingen over teststrategie
- Keuze van testtooling
- QA-specifieke processen

**Voorbeelden:**
- E2E-testframework
- Beheer van testdata
- Aanpak voor performance testing
- Opzet van testomgeving

---

## Kruisverwijzingen

Bij verwijzing naar een ADR uit een andere repository, **vermeld altijd de repositorynaam** en geef bij voorkeur een volledige GitHub-link.

**Goede voorbeelden:**
- "This implements the authentication approach defined in [eap-architecture ADR-003](https://github.com/org/eap-architecture/blob/main/decisions/ADR-003-api-authentication.md)"
- "See backend ADR-002 for database migration strategy"
- "Related to eap-frontend ADR-001 (State Management)"

**Slechte voorbeelden:**
- "See ADR-003" (Welke repository?)
- "As per the authentication ADR" (Welk nummer? Welke repo?)

---

## ADRs terugvinden

**Om het volgende beschikbare nummer in je repository te vinden:**
1. Bekijk de map `/decisions/` of `/docs/decisions/`
2. Kijk naar het hoogst genummerde ADR
3. Gebruik het volgende sequentiële nummer

**Om alle ADRs in het project te vinden:**
- Elke repository's `/decisions/` map heeft een README.md met een index
- eap-architecture/decisions/README.md linkt naar de beslissingsmappen van andere repositories

---

## Bestandsnaamconventie

**Formaat:** `ADR-XXX-korte-beschrijvende-titel.md`

**Regels:**
- Gebruik driecijferige, links met nullen gevulde nummers: `001`, `002`, `010`, `100`
- Gebruik kleine letters met koppeltekens voor de titel
- Houd titels beknopt maar beschrijvend (3–6 woorden)
- Vermijd afkortingen tenzij algemeen bekend

**Goede voorbeelden:**
- `ADR-001-repository-strategy.md`
- `ADR-002-database-schema-versioning.md`
- `ADR-015-frontend-state-management.md`
- `ADR-023-api-authentication-approach.md`

**Slechte voorbeelden:**
- `ADR-1-repo-strat.md` (niet links gevuld, te afgekort)
- `ADR-042-we-decided-to-use-postgresql-for-persistence.md` (te lang)
- `ADR-008-Database_Schema.md` (gemengde hoofdletters, underscore)

---

## ADR-categorieën

### Platform Decision
Beslissingen die review door staff vereisen (na teaminput):
- **Tech stack versies** (React 18 vs 19, Python 3.11 vs 3.12)
- **Ecosysteemkeuzes** (componentenbibliotheek met niche vs mainstream community)
- Infrastructuurkeuzes
- Beveiligingsimplementaties
- Deploymentstrategieën
- Toolselecties die het gehele systeem beïnvloeden
- **AVG-nalevingsaanpak (staff/FG geconsulteerd)**
- **Dataretentie- en privacybeleid**
- **Beslissingen die leer- of marktdoelen beïnvloeden**

**Criteria voor Platform Decisions:**
- Beïnvloedt het gehele systeem of meerdere componenten
- Later moeilijk te wijzigen (hoge overstapkosten)
- Vereist ervaring/oordeel dat het teamniveau overstijgt
- Beïnvloedt leerdoelen of marktvoorbereiding
- Team mist context om langetermijngevolgen te evalueren

### Application Decision
Beslissingen die eigendom zijn van het team (binnen platformbeperkingen):
- **Implementatie binnen gekozen tech stack**
- **Specifieke componenten binnen goedgekeurd ecosysteem**
- Databaseschema-ontwerp (met privacyoverwegingen)
- API-eindpuntstructuur
- Frontend-componentorganisatie
- Implementatiepatronen
- Codeorganisatie en naamgevingsconventies
- **Technische implementatie van AVG-vereisten (anonimisering, export, etc.)**

**Criteria voor Application Decisions:**
- Binnen gevestigde platformbeperkingen
- Team kan afwegingen evalueren
- Relatief eenvoudig te wijzigen (lagere kosten)
- Goede leerervaring voor het team
- Team kan experimenteren en leren van fouten

### Beslisboom voor grijze gevallen

**Als je twijfelt over de categorie, vraag jezelf af:**

1. **Heeft dit invloed op leerdoelen of marktvoorbereiding?**
   → Als JA: Platform Decision

2. **Is dit later moeilijk/kostbaar te wijzigen?**
   → Als JA: Platform Decision

3. **Heeft het team voldoende context om de langetermijngevolgen te evalueren?**
   → Als NEE: Platform Decision

4. **Kan het team veilig experimenteren en leren van fouten?**
   → Als NEE: Platform Decision

5. **Gaat het hoofdzakelijk over implementatiedetails binnen beperkingen?**
   → Als JA: Application Decision

**Bij twijfel:** Markeer als "Application Decision" en bespreek het met de staff coach tijdens ADR-review. Staff begeleidt de categorisering.

---

## Tips voor het schrijven van goede ADRs

**Wees specifiek**
- Slecht: "We will use a modern frontend framework"
- Goed: "We will use React 19 with TypeScript and Zustand for state management"

**Leg de 'waarom' uit, niet alleen de 'wat'**
- Documenteer de redenering en context
- Toekomstige teamleden moeten de krachten die meespeelden begrijpen

**Voorbeeld: Platform Decision met teaminput**

```markdown
# ADR-003: React Version Selection

## Status
Accepted

## Category
Platform Decision (Staff decided after team input)

## Context
Team discussed using React v18 vs React v19 for the frontend.

**React v18 Arguments:**
- Team member has prior experience with v18
- Specific component library preference (ecosystem familiarity)
- Proven stability in production environments

**React v19 Arguments:**
- Latest version with performance improvements (concurrent rendering, automatic batching)
- Better preparation for Dutch IT market (industry moving to v19)
- Mainstream ecosystem with stronger European/global community support
- Modern best practices and patterns

## Decision
We will use **React v19** with mainstream component libraries.

## Consequences

**Positive:**
- Team learns latest React features and patterns
- Better alignment with Dutch IT industry trends
- Strong community support and extensive documentation
- Modern performance optimizations built-in

**Negative:**
- Team member's v18 experience less directly applicable
- Slightly newer, less battle-tested in production
- Learning curve for v19-specific features

**Mitigation:**
- Team member with React experience helps team understand core concepts
- React fundamentals (components, hooks, state) remain consistent across versions
- Focus on learning modern patterns over leveraging existing v18 knowledge

## Alternatives Considered
1. **React v18 with team member's preferred library**: Rejected due to niche community
   and learning goals prioritization
2. **Vue.js or other framework**: Out of scope - React already chosen as platform

## Constraints
- **Learning Goal:** Prepare trainees for Dutch corporate IT market
- **Community:** Prefer mainstream libraries with large European/global communities
- **Maintenance:** Avoid libraries with small or region-specific communities
- **Market Relevance:** Industry is moving toward v19, not staying on v18

## Deciders
Staff (after team discussion and input)

## Notes
This decision prioritizes learning goals and market preparation over
leveraging existing team member experience. Team member's React knowledge
remains valuable for teaching fundamental concepts to other team members.
```

**Houd het beknopt**
- Streef naar maximaal 1–2 pagina's
- Link naar externe bronnen in plaats van documentatie te kopiëren

**Gebruik Git effectief**
- Betekenisvolle commit-berichten voor ADR-updates
- PR-discussies leggen de redenering van het team vast
- Git blame toont wie welk gedeelte heeft geschreven
- Git history toont de evolutie van de beslissing

**Wees eerlijk over afwegingen**
- Elke beslissing heeft nadelen
- Die erkennen toont volwassen denken

**Werk status bij wanneer beslissingen veranderen**
- Bewerk de inhoud van geaccepteerde ADRs niet
- Verander de status naar "Superseded" en link naar het nieuwe ADR
- Maak een nieuw ADR dat het oude vervangt
- Beide ADRs blijven als historisch record in de repository

---

## Veelgestelde vragen

**V: Kunnen we een geaccepteerd ADR wijzigen?**
A: Je kunt de **status** bijwerken (bijv. Accepted → Superseded), maar je kunt de **inhoud** (de beslissing, redenering of context) niet wijzigen. Als de beslissing verandert, maak dan een nieuw ADR dat het oude vervangt. Beide ADRs blijven in de repository als historisch record.

**V: Hoe documenteren we statuswijzigingen?**
A: Voeg een regel toe aan de tabel "Status History" onderaan het ADR. Vermeld de datum, de nieuwe status en de reden voor de wijziging. Bijvoorbeeld: "2026-02-15 | Superseded | Replaced by ADR-023 due to new security requirements"

**V: Wat doen we met typefouten of opmaakcorrecties?**
A: Kleine correcties die de betekenis niet wijzigen zijn toegestaan. Gebruik je oordeel – als het de begrip van de beslissing verandert, maak dan liever een nieuw ADR.

**V: Worden ADRs beoordeeld via code review?**
A: Ja! ADRs worden net als code beoordeeld via Pull Requests. De PR-discussie wordt onderdeel van het besluitvormingsrecord. Vereist minimaal 2 reviewers.

**V: Moeten ADRs in dezelfde repository staan als de code?**
A: Ja. ADRs staan in `/docs/architecture/decisions/` in je hoofdcode-repository. Zo blijven beslissingen en code gesynchroniseerd.

**V: Wat als we een beslissing hebben genomen maar geen ADR hebben geschreven?**
A: Schrijf er alsnog een achteraf als de beslissing nog relevant en belangrijk is.

**V: Waarom kan hetzelfde nummer (bijv. ADR-001) in meerdere repositories bestaan?**
A: Elke repository behoudt zijn eigen sequentiële nummering. De repositorynaam geeft de scope. Dit is eenvoudiger dan het coördineren van een globaal nummersysteem over alle repositories en is de standaard in de industrie.

**V: Hoe verwijs ik naar een ADR uit een andere repository?**
A: Vermeld altijd de repositorynaam en geef bij voorkeur een volledige GitHub-link. Voorbeeld: "See [eap-architecture ADR-003](https://github.com/org/eap-architecture/blob/main/decisions/ADR-003-api-auth.md)". Hierdoor worden cross-repository afhankelijkheden expliciet en zichtbaar.

**V: In welke repository hoort mijn ADR?**
A: Vraag jezelf af: "Beïnvloedt deze beslissing slechts één component of meerdere?" Als het meerdere componenten beïnvloedt (bijv. API-ontwerp raakt zowel backend als frontend), zet het dan in eap-architecture. Als het specifiek is voor de interne implementatie van één component, zet het dan in de repository van dat component. Zie het gedeelte "ADR-organisatie per repository" voor gedetailleerde begeleiding.

**V: Moeten alle teamleden het eens zijn?**
A: Streef naar consensus. Als er sterke onenigheid is, documenteer beide standpunten in het ADR en laat de Product Owner de uiteindelijke beslissing nemen.

**V: Hoeveel ADRs moeten we hebben?**
A: Kwaliteit boven kwantiteit. Voor een project van 12 weken zijn 5–15 ADRs in totaal te verwachten.

**V: Wat als de beslissing voor de hand liggend is?**
A: Als het echt voor de hand liggend is, wordt het ADR kort. Maar "voor de hand liggende" beslissingen zijn later of voor nieuwelingen vaak helemaal niet zo vanzelfsprekend.

---

**Einde ADR Template**
