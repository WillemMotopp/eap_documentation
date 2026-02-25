---
Document: EAP_Repository_Structure_Guide
Version: 1.0
Status: Approved
Audience: Staff + Interns
Taal: Nederlands (vertaling van v1.0)
---

# EAP Project - Handleiding Repositorystructuur

**Versie:** 1.0
**Datum:** 2026-01-06
**Status:** Goedgekeurd
**Doelgroep:** Staff + Stagiairs

---

## Overzicht

Het EAP-project maakt gebruik van een **multi-repository structuur** met vier aparte repositories:

1. **eap-architecture** – Platformbeslissingen, API-specificaties, systeemdiagrammen
2. **eap-backend** – Python/FastAPI backend-applicatie
3. **eap-frontend** – React frontend-applicatie
4. **eap-qa** – Testautomatisering en QA-documentatie

Dit document legt de structuur, de redenering en de conventies uit voor het werken met meerdere repositories.

---

## Repositorydetails

### 1. eap-architecture

**Doel:** Cross-cutting documentatie en beslissingen op platformniveau

**GitHub URL:** `https://github.com/[org]/eap-architecture`

**Structuur:**
```
eap-architecture/
├── decisions/
│   ├── ADR-001-repository-strategy.md
│   ├── ADR-002-tech-stack.md
│   ├── ADR-003-api-authentication.md
│   ├── template.md
│   └── README.md (index of all ADRs)
├── diagrams/
│   ├── context.drawio
│   ├── container.drawio
│   ├── component-backend.drawio
│   └── README.md
├── api-specs/
│   ├── openapi.yaml
│   └── README.md
├── deployment/
│   ├── docker-compose.yml
│   ├── deployment-guide.md
│   └── README.md
├── .github/
│   └── workflows/
│       └── validate-openapi.yml
└── README.md
```

**Wat hier thuishoort:**
- Platformbeslissingen (tech stack, infrastructuur, tooling)
- API-specificaties (OpenAPI/Swagger)
- Architectuurdiagrammen (C4-model)
- Deploymentdocumentatie
- Cross-repository coördinatiedocumentatie

**Eigenaarschap:**
- Product Owner (primair)
- DevOps lead (deploymentdocumentatie)
- Heel team (bijdragen aan ADRs en diagrammen)

---

### 2. eap-backend

**Doel:** Backend API-applicatie

**GitHub URL:** `https://github.com/[org]/eap-backend`

**Structuur:**
```
eap-backend/
├── app/
│   ├── api/
│   │   ├── routes/
│   │   └── dependencies.py
│   ├── models/
│   ├── services/
│   ├── core/
│   │   ├── config.py
│   │   └── security.py
│   └── main.py
├── tests/
│   ├── unit/
│   ├── integration/
│   └── conftest.py
├── alembic/
│   ├── versions/
│   └── env.py
├── docs/
│   ├── decisions/
│   │   ├── ADR-001-database-schema.md
│   │   ├── ADR-002-orm-patterns.md
│   │   ├── template.md
│   │   └── README.md
│   └── api/
│       └── README.md
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
├── Dockerfile
├── requirements.txt
├── pyproject.toml
├── alembic.ini
└── README.md
```

**Wat hier thuishoort:**
- Backend-applicatiecode
- Backend-specifieke tests
- Databasemigraties
- Backend-specifieke ADRs (schemaontwerp, ORM-patronen, etc.)
- Backend API-documentatie

**Eigenaarschap:**
- Backend-developers
- DevOps lead (deploymentconfiguratie)

---

### 3. eap-frontend

**Doel:** React frontend-applicatie

**GitHub URL:** `https://github.com/[org]/eap-frontend`

**Structuur:**
```
eap-frontend/
├── src/
│   ├── components/
│   │   ├── common/
│   │   └── features/
│   ├── pages/
│   ├── services/
│   │   ├── api/
│   │   └── auth/
│   ├── store/
│   ├── hooks/
│   ├── utils/
│   ├── App.tsx
│   └── main.tsx
├── tests/
│   ├── unit/
│   └── integration/
├── public/
├── docs/
│   ├── decisions/
│   │   ├── ADR-001-state-management.md
│   │   ├── ADR-002-component-patterns.md
│   │   ├── template.md
│   │   └── README.md
│   └── components/
│       └── README.md
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
├── Dockerfile
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

**Wat hier thuishoort:**
- Frontend-applicatiecode
- Frontend-specifieke tests
- Frontend-specifieke ADRs (state management, componentpatronen, etc.)
- Componentdocumentatie

**Eigenaarschap:**
- Frontend-developers
- DevOps lead (deploymentconfiguratie)

---

### 4. eap-qa

**Doel:** Testautomatisering en QA-documentatie

**GitHub URL:** `https://github.com/[org]/eap-qa`

**Structuur:**
```
eap-qa/
├── e2e-tests/
│   ├── auth/
│   ├── requests/
│   ├── workflows/
│   └── conftest.py
├── performance/
│   ├── load-tests/
│   └── stress-tests/
├── test-plans/
│   ├── sprint-01-test-plan.md
│   └── regression-test-plan.md
├── test-data/
│   ├── fixtures/
│   └── mocks/
├── docs/
│   ├── decisions/
│   │   ├── ADR-001-e2e-framework.md
│   │   ├── ADR-002-test-data-strategy.md
│   │   ├── template.md
│   │   └── README.md
│   └── test-strategy.md
├── .github/
│   └── workflows/
│       ├── e2e.yml
│       └── performance.yml
├── requirements.txt
└── README.md
```

**Wat hier thuishoort:**
- End-to-end tests
- Performance tests
- Testplannen en documentatie
- QA-specifieke ADRs (testaanpak, tooling, etc.)
- Testdata en fixtures

**Eigenaarschap:**
- QA/testautomatiseringlead
- Heel team draagt bij aan testdekking

---

## Waarom multi-repository?

Deze beslissing is gedocumenteerd in **eap-architecture ADR-001: Repository Strategy**.

**Belangrijkste redenen:**
1. **Teamervaring** – Het team is vertrouwd met single-repo workflows
2. **DevOps-eenvoud** – Aparte CI/CD pipelines per component
3. **Duidelijk eigenaarschap** – Elke repo heeft een duidelijke primaire eigenaar
4. **Onafhankelijke deployment** – Backend kan deployen zonder frontend-build te activeren

**Geaccepteerde afwegingen:**
- Feature-coördinatie vereist discipline (Jira-tickets koppelen meerdere PRs)
- API-contractsynchronisatie vereist een expliciet proces (OpenAPI in eap-architecture)
- ADRs hebben duidelijke categoriseringsregels nodig

---

## Werken met meerdere repositories

### Git workflow

**Alle repositories gebruiken Git Flow:**
- `main` – Productieklare code
- `dev` – Integratietak
- `feature/EAP-XXX-omschrijving` – Feature branches

**Branch protection:**
- `main`: Vereist 2 PR-reviews, alle CI-checks moeten slagen
- `dev`: Vereist 1 PR-review, alle CI-checks moeten slagen

### Feature-ontwikkelworkflow

**User Story: EAP-123 "Gebruiker kan toegangsverzoek indienen"**

1. **Sprint Planning:**
   - Identificeer welke repos worden geraakt: backend + frontend + qa
   - Maak feature branches aan in elke repo:
     - `eap-backend: feature/EAP-123-access-request-endpoint`
     - `eap-frontend: feature/EAP-123-access-request-form`
     - `eap-qa: feature/EAP-123-access-request-tests`

2. **Ontwikkeling:**
   - Backend-team implementeert API-eindpunt
   - Frontend-team implementeert UI (moet mogelijk wachten op backend of mocks gebruiken)
   - QA bereidt testcases voor

3. **Pull Requests:**
   - Elke repo krijgt zijn eigen PR
   - Alle PRs verwijzen naar het Jira-ticket: `EAP-123`
   - PRs kunnen naar elkaar verwijzen voor context

4. **Review & Merge:**
   - PRs worden onafhankelijk beoordeeld
   - Backend mergt als eerste (API beschikbaar)
   - Frontend mergt daarna (verbruikt API)
   - QA mergt als laatste (tests tegen geïntegreerd systeem)

5. **Jira-integratie:**
   - Jira-ticket toont alle gerelateerde PRs
   - Status: In Progress → In Review → Done (wanneer alle PRs gemerged zijn)

### Commit-berichtconventie

**Formaat:** `type(scope): omschrijving (EAP-XXX)`

**Voorbeelden:**
```bash
# In eap-backend
git commit -m "feat(api): add access request endpoint (EAP-123)"

# In eap-frontend
git commit -m "feat(requests): add request submission form (EAP-123)"

# In eap-qa
git commit -m "test(e2e): add access request flow tests (EAP-123)"

# In eap-architecture
git commit -m "docs(adr): add ADR-005 access request workflow (EAP-123)"
```

**Types:** feat, fix, docs, test, refactor, chore, ci

### API-contractbeheer

**Probleem:** Backend en frontend moeten overeenstemmen over de API-structuur.

**Oplossing:** OpenAPI-specificatie in `eap-architecture`

**Workflow:**
1. **API-ontwerpdiscussie** → Werk `eap-architecture/api-specs/openapi.yaml` bij
2. **Backend** implementeert conform de specificatie
3. **Frontend** genereert TypeScript-types uit de specificatie
4. **QA** valideert contracten aan de hand van de specificatie

**Validatie:**
- Backend: OpenAPI-validatie in tests
- Frontend: TypeScript-types gegenereerd uit specificatie
- CI: Geautomatiseerde validatie van OpenAPI-specificatie

### Cross-repository ADR-verwijzingen

**Vermeld altijd de repositorynaam** bij verwijzing naar ADRs uit andere repos.

**Voorbeelden:**

In `eap-backend/docs/decisions/ADR-003-endpoint-structure.md`:
```markdown
## Related ADRs

### In this repository (eap-backend):
- ADR-001: Database Schema Approach
- ADR-002: ORM Patterns

### In other repositories:
- [eap-architecture ADR-003: API Authentication](https://github.com/org/eap-architecture/blob/main/decisions/ADR-003-api-authentication.md)
- [eap-architecture ADR-004: API Versioning](https://github.com/org/eap-architecture/blob/main/decisions/ADR-004-api-versioning.md)
```

---

## ADR-beslissingsmatrix

**In welke repository hoort jouw ADR?**

| Soort beslissing | Voorbeeld | Repository | Wie beslist | Redenering |
|------------------|-----------|------------|-------------|------------|
| **Platform** | React-versie (v18 vs v19) | eap-architecture | **Staff** (na teaminput) | Beïnvloedt gehele frontend, leerdoelen, moeilijk te wijzigen |
| **Platform** | Componentenbibliotheek-ecosysteem | eap-architecture | **Staff** (na teaminput) | Omvang community beïnvloedt onderhoud en leren |
| **Platform** | Keuze van tech stack | eap-architecture | **Staff** (na teaminput) | Beïnvloedt alle componenten |
| **Platform** | Authenticatieaanpak | eap-architecture | **Staff** (na teaminput) | Beveiligingskritisch, beïnvloedt alle componenten |
| **Platform** | Deploymentstrategie | eap-architecture | **Staff** (na teaminput) | Beïnvloedt alle deployments |
| **Application** | Specifiek component uit bibliotheek | eap-frontend | **Team** | Binnen goedgekeurd ecosysteem |
| **Application** | State management implementatie | eap-frontend | **Team** | Binnen gekozen stack (bijv. Zustand vs Context) |
| **Application** | Databaseschema-ontwerp | eap-backend | **Team** | Backend-specifiek detail |
| **Application** | ORM-gebruikspatronen | eap-backend | **Team** | Backend-specifiek detail |
| **Application** | Componentstructuurpatronen | eap-frontend | **Team** | Frontend-specifiek detail |
| **Application** | E2E-framework keuze | eap-qa | **Team** | QA-specifieke beslissing (binnen beperkingen) |
| **Application** | Testdatabeheer | eap-qa | **Team** | QA-procesdetail |

### Platform vs. Application – beslissingscriteria

**Criteria voor Platform Decisions:**
- Beïnvloedt het gehele systeem of meerdere componenten
- Later moeilijk te wijzigen (hoge overstapkosten)
- Vereist ervaring/oordeel dat het teamniveau overstijgt
- **Beïnvloedt leerdoelen of marktvoorbereiding**
- Team mist context voor langetermijngevolgen

**Voorbeelden:**
- React v18 vs v19 (versiekeuze = platform)
- Componentenbibliotheek met niche vs mainstream community (ecosysteem = platform)
- Databasetype (PostgreSQL vs MySQL)
- Authenticatiemethode (JWT vs sessie)

**Criteria voor Application Decisions:**
- Binnen gevestigde platformbeperkingen
- Team kan afwegingen evalueren
- Relatief eenvoudig te wijzigen (lagere kosten)
- Goede leerervaring
- Team kan veilig experimenteren

**Voorbeelden:**
- Welke Button-component uit de goedgekeurde bibliotheek te gebruiken
- Hoe Redux-state te structureren (als Redux gekozen is)
- Specifiek databasetabelontwerp
- Organisatie van componentbestanden

### Vuistregel voor repository-toewijzing

- **Beïnvloedt meerdere repos?** → `eap-architecture` (Platform Decision, staff beoordeelt)
- **Specifiek voor één component?** → Repository van dat component (Application Decision, team is eigenaar)
- **Grijze zone?** → Begin in `eap-architecture`, staff begeleidt tijdens review

---

## Versiebeheer en releases

### Semantisch versiebeheer

Alle repositories gebruiken semantisch versiebeheer: `MAJOR.MINOR.PATCH`

**Sprint-releases:**
- Sprint 1: v0.1.0
- Sprint 2: v0.2.0
- Sprint 3: v0.3.0
- Eindrelease: v1.0.0

### Gesynchroniseerde releases

Aan het einde van elke Sprint worden **alle repositories voorzien van hetzelfde versielabel**:

```bash
# Einde Sprint 2
eap-architecture: git tag -a v0.2.0 -m "Sprint 2 release"
eap-backend:      git tag -a v0.2.0 -m "Sprint 2 release"
eap-frontend:     git tag -a v0.2.0 -m "Sprint 2 release"
eap-qa:           git tag -a v0.2.0 -m "Sprint 2 release"
```

**Deployment:** Overeenkomende versies worden samen gedeployed.

### Versiecompatibiliteit

Documenteer versiecompatibiliteit in de README van elke repository:

```markdown
## Version Compatibility

This version (v0.2.0) is compatible with:
- eap-backend: v0.2.0
- eap-frontend: v0.2.0
- API spec: v0.2.0 (eap-architecture)
```

---

## README-structuur per repository

Elke repository moet een README.md hebben met:

1. **Projectomschrijving**
2. **Setup-instructies**
3. **Ontwikkelworkflow**
4. **Testinstructies**
5. **Deploymentproces**
6. **Links naar andere repositories**
7. **Link naar architectuurdocumentatie**
8. **Versiecompatibiliteitsmatrix**

**Template:** Zie `eap-architecture/templates/repository-readme-template.md`

---

## CI/CD per repository

Elke repository heeft zijn eigen GitHub Actions workflows:

### Backend CI (eap-backend/.github/workflows/ci.yml)
- Actief bij: Pull requests naar `dev` of `main`
- Stappen: Lint → Test → Build → Deploy (indien main)

### Frontend CI (eap-frontend/.github/workflows/ci.yml)
- Actief bij: Pull requests naar `dev` of `main`
- Stappen: Lint → Test → Build → Deploy (indien main)

### E2E Tests (eap-qa/.github/workflows/e2e.yml)
- Actief bij: Schema (elke 4 uur) of handmatige trigger
- Stappen: E2E tests uitvoeren tegen gedeployde omgeving

### OpenAPI-validatie (eap-architecture/.github/workflows/validate.yml)
- Actief bij: Pull requests naar `main`
- Stappen: Syntaxis en volledigheid van OpenAPI-specificatie valideren

---

## Coördinatiemiddelen

### Jira

**Ticketstructuur:**
- Epic: Hoofdfunctie (bijv. "User Access Management")
- User Story: Cross-repo feature (bijv. "Gebruiker kan aanvraag indienen")
- Subtaken (optioneel): Implementatie per repo

**Koppeling:**
- PRs worden automatisch gekoppeld aan tickets via commit-berichten met ticket-ID
- Tickets tonen alle gerelateerde PRs uit alle repositories

### Microsoft Teams

**Er worden twee aparte Teams gebruikt:**

**1. EAP Project (Stagiairs + Staff)**
- Primaire communicatie voor projectwerk
- Alle stagiairs hebben toegang
- Staff neemt actief deel

**Kanalen:**
- `#general` – Projectupdates, aankondigingen, algemene vragen
- `#backend` – Backend-ontwikkelingsdiscussies
- `#frontend` – Frontend-ontwikkelingsdiscussies
- `#qa` – Testen en kwaliteitsborging
- `#devops` – CI/CD, deployments, infrastructuur
- `#architecture` – Architectuurdiscussies en ADR-reviews
- `#random` – Sociaal en niet-werkgerelateerd

**2. EAP Staff Only (uitsluitend Staff)**
- Staffcoördinatie en privédiscussies
- Stagiairs hebben GEEN toegang
- Volledig gescheiden van het stagiairsteam

**Kanalen:**
- `#general` – Staffcoördinatie en planning
- `#assessments` – Beoordelingsdiscussies (privé)
- `#incidents` – Incidentobservaties (privé)
- `#coaching` – Coachingstrategieën (privé)

**Belangrijk:** Staffgesprekken (beoordelingen, incidenten, coachingnotities) vinden UITSLUITEND plaats in het staffteam, nooit in het stagiairsteam.

### Daily Standup

**Formaat:**
- Wat heb je gedaan? (vermeld repo indien relevant)
- Wat ga je doen? (vermeld repo indien relevant)
- Blokkades? (vooral cross-repo afhankelijkheden)

---

## Veelvoorkomende valkuilen en oplossingen

### Valkuil 1: API-mismatch

**Probleem:** Backend implementeert API anders dan frontend verwacht.

**Oplossing:**
- Werk altijd eerst de OpenAPI-specificatie bij in `eap-architecture`
- Backend valideert responses op basis van specificatie in tests
- Frontend genereert types uit specificatie
- QA valideert contracten

### Valkuil 2: Circulaire afhankelijkheden

**Probleem:** Backend PR heeft frontend PR nodig die weer backend PR nodig heeft.

**Oplossing:**
- Ontwerp APIs vóór implementatie
- Gebruik mocks/stubs tijdens parallelle ontwikkeling
- Backend implementeert eindpunt met voorbeelddata
- Frontend ontwikkelt op basis van mocks
- Integratietests valideren de verbinding

### Valkuil 3: Vergeten ADRs

**Probleem:** Beslissing genomen in Teams, niet gedocumenteerd in ADR.

**Oplossing:**
- Sprint Retrospective: "Hebben we deze Sprint significante beslissingen genomen?"
- Schrijf achteraf ADRs voor belangrijke beslissingen
- Maak ADR-schrijven onderdeel van de Definition of Done

### Valkuil 4: Versieverwarring

**Probleem:** Onduidelijk welke backendversie werkt met welke frontendversie.

**Oplossing:**
- Synchroniseer versielabels aan het einde van elke Sprint
- Documenteer versiecompatibiliteit in README
- Gebruik overeenkomende versienummers bij deployment

---

## Aan de slag

### Checklist eerste week

**Voor alle teamleden:**
- [ ] Alle 4 repositories klonen
- [ ] Toegang tot alle repositories verifiëren
- [ ] README.md van elke repository lezen
- [ ] Git Flow workflow begrijpen
- [ ] ADR-template in eap-architecture bekijken
- [ ] Aanmelden bij Microsoft Teams-kanalen

**Voor de DevOps lead:**
- [ ] Controleren of CI/CD pipelines werken
- [ ] Deployment naar TransIP VPS testen
- [ ] Controleren of branch protection rules actief zijn
- [ ] Jira-GitHub-integratie verifiëren

**Voor de Product Owner:**
- [ ] Structuur van eap-architecture bekijken
- [ ] ADR-categorisering begrijpen
- [ ] Eerste architecturale beslissingen voorbereiden voor documentatie
- [ ] AVG-vereisten ontvangen van staff/FG vóór Sprint Planning

**Voor Staff (vóór Sprint 1):**
- [ ] FG/juridische consultatie over AVG-vereisten
- [ ] Rechtmatige grondslag voor gegevensverwerking vaststellen
- [ ] Retentiebeleid voor persoonsgegevens instellen
- [ ] AVG-vereisten verstrekken aan Product Owner
- [ ] Voorgestelde AVG-nalevingsaanpak beoordelen (ADR)

---

## Verder lezen

- [eap-architecture ADR-001: Repository Strategy](https://github.com/org/eap-architecture/blob/main/decisions/ADR-001-repository-strategy.md)
- [Architecture Decision Record Template](./Architecture_Decision_Record_Template_v1.0.md)
- [Git Flow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [Semantic Versioning](https://semver.org/)
- [OpenAPI Specification](https://swagger.io/specification/)

---

**Documentbeheer**
- Aangemaakt: 2026-01-06
- Eigenaar: Motopp Staff
- Herzieningsfrequentie: Na Sprint 1
- Status: Goedgekeurd
