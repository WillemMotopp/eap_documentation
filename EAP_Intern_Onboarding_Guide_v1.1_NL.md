---
Document: EAP_Intern_Onboarding_Guide
Version: 1.1
Status: Approved
Audience: Interns
Approval required: No
Changes from v1.0: Added tooling infrastructure section and architecture documentation expectations
Taal: Nederlands (vertaling van v1.1)
---

# Onboardinggids voor Stagiairs – Enterprise Application Project (EAP)

## Doel van deze gids

Welkom bij het **Enterprise Application Project (EAP)**.

Deze gids legt uit:
- hoe je als team wordt verwacht samen te werken;
- welke rollen er zijn en wie ze vervult;
- hoe planning en oplevering zijn georganiseerd;
- wat "kwaliteit" betekent in dit project;
- welke tools en infrastructuur beschikbaar zijn.

Deze gids geeft je **context en verwachtingen**.
Gedetailleerde regels, templates en afspraken staan in aparte documenten.

---

## De projectmentaliteit

Dit project is opgezet als een **professioneel softwareontwikkelingsproject**.

Dat betekent:
- je werkt in een Scrum team;
- je neemt verantwoordelijkheid voor planning, kwaliteit en oplevering;
- problemen, defects en operationele kwesties zijn onderdeel van normaal werk;
- staff ondersteunt en coacht je, maar neemt jouw rollen niet over.

Je wordt verwacht te handelen als een **professioneel team**, niet als studenten die stap-voor-stap instructies volgen.

---

## Teamrollen en verantwoordelijkheden

### Product Owner (teamrol)

Één teamlid vervult de rol van **Product Owner**.

De Product Owner:
- definieert en ordent de Product Backlog;
- verduidelijkt vereisten en acceptatiecriteria;
- neemt beslissingen over scope en prioriteit;
- vertegenwoordigt stakeholderbelangen binnen het team.

De Product Owner rol wordt vervuld door een **teamlid**, niet door staff.

Staff kan optreden als stakeholder of adviseur, maar neemt **geen** productbeslissingen.

---

### Scrum Master (teamrol)

Één teamlid vervult de rol van **Scrum Master**.

De Scrum Master:
- faciliteert Scrum events;
- zorgt ervoor dat Scrum-regels en timeboxes worden nageleefd;
- helpt het team impediments te identificeren en weg te nemen;
- ondersteunt transparantie en samenwerking binnen het team.

De Scrum Master is een **teamrol**, geen staffrol.

Staffleden treden op als **Scrum Coaches**.
Zij ondersteunen en daagen de Scrum Master uit, maar leiden geen Scrum events en nemen de verantwoordelijkheden van de Scrum Master niet over.

---

### DevOps verantwoordelijkheid (teamverantwoordelijkheid)

Één of meer teamleden nemen verantwoordelijkheid voor **DevOps-activiteiten**, zoals:
- CI/CD pipelines;
- deployments;
- monitoring en logs;
- operationele kwesties.

DevOps is een **teamverantwoordelijkheid**.

Je wordt verwacht:
- problemen vroeg te signaleren;
- leverings- en pipelinefouten te onderzoeken;
- helder te communiceren over operationele problemen;
- samen te werken aan herstel of rollback wanneer nodig.

---

### Ontwikkelverantwoordelijkheid (gedeelde verantwoordelijkheid)

Alle teamleden dragen bij aan **het bouwen, testen en verbeteren van het product**.

Ontwikkelwerk omvat:
- code schrijven (frontend en backend);
- tests aanmaken en onderhouden;
- code reviews;
- debuggen en defects verhelpen;
- refactoring en technische verbeteringen.

---

### Gedeelde verantwoordelijkheid

Alle teamleden dragen bij aan het bouwen, testen, verbeteren en beheren van het product.

Jullie delen verantwoordelijkheid voor:
- het behalen van het Sprint Goal;
- productkwaliteit;
- professioneel gedrag;
- samenwerking en communicatie.

---

## Beschikbare tools en infrastructuur

### Versiebeheer

**GitHub (private repositories)**
- Alle code wordt opgeslagen in private GitHub repositories
- Git Flow workflow is verplicht:
  - `main` branch: productieklare code
  - `dev` branch: integratietak
  - `feature/*` branches: individuele feature-ontwikkeling
- Branch protection rules zijn actief op `main` en `dev`
- Pull requests zijn vereist voor mergen

### Projectbeheer

**Jira (betaalde licentie)**
- Sprint planning en tracking
- Product Backlog beheer
- Scrum board voor Sprintwerk
- Toegangsgegevens worden verstrekt door staff

### CI/CD

**GitHub Actions**
- Geautomatiseerd testen bij pull requests
- Continuous integration pipeline
- Deployment-automatisering naar de doelomgeving
- Pipeline-configuratie maakt deel uit van je repository

### Deploymentplatform

**TransIP VPS (Linux)**
- Productieachtige deploymentomgeving
- Linux-gebaseerde server
- SSH-toegang voor deployment
- Toegangsgegevens worden verstrekt door staff

### Communicatie

**Microsoft Teams**
- Primair communicatiemiddel
- Daily standups (bij remote werken)
- Sprint ceremonies
- Teamdiscussies en beslissingen

---

## Hoe je werk plant

### Definition of Ready

Voordat werk in een Sprint wordt opgenomen, is het team het erover eens dat een backlog-item **Ready** is.

Dit betekent:
- het doel van het item is helder;
- de waarde voor het product of de gebruiker is begrepen;
- acceptatiecriteria zijn opgesteld en begrijpelijk;
- het item is klein genoeg om binnen één Sprint afgerond te worden;
- afhankelijkheden en openstaande vragen zijn bekend;
- technische en DevOps-gevolgen zijn overwogen;
- architecturele impact is geïdentificeerd (indien van toepassing).

De Definition of Ready ondersteunt **goede Sprint Planning**.

Het neemt de verantwoordelijkheid van de Product Owner of het team **niet** weg.
Het helpt je samen betere beslissingen te nemen.

---

## Hoe je werk oplevert

### Definition of Done

Werk wordt pas beschouwd als **Done** wanneer het team bevestigt dat het voldoet aan de Definition of Done.

Dit omvat:
- code die leesbaar is en beoordeeld is;
- geautomatiseerde tests die onderdeel zijn van de pipeline;
- een geslaagde build;
- deployment in de doelomgeving (indien van toepassing);
- voorspelbaar gedrag onder faalcondities;
- duidelijke logging en herstel- of rollback-mogelijkheden;
- bijgewerkte documentatie waar nodig;
- gedocumenteerde architecturale beslissingen (indien van toepassing).

"Done" betekent:
- klaar om te tonen in een Sprint Demo;
- klaar om door anderen gebruikt te worden.

Zie de **Definition of Done Template** voor de volledige checklist.

---

## Architecture en technische beslissingen

### Architectuurdocumentatie

Significante architecturale en technische beslissingen moeten worden gedocumenteerd met behulp van **Architecture Decision Records (ADRs)**.

**Wanneer schrijf je een ADR:**
- Bij het kiezen tussen meerdere haalbare technische alternatieven
- Bij beslissingen die later moeilijk of kostbaar zijn om te wijzigen
- Bij het afwijken van gevestigde patronen
- Wanneer beslissingen een significante impact hebben op niet-functionele vereisten

**ADR-proces:**
1. Stel de beslissing voor in ADR-formaat
2. Bespreek met het team
3. Beoordeling door minimaal 2 teamleden
4. Accepteer en merge wanneer consensus is bereikt

Zie de **ADR Template** voor het formaat en de structuur.

### Architecture governance

Sommige architecturale beslissingen zijn **voorgeschreven** door staff en niet onderhandelbaar (tech stack, beveiligingsvereisten, infrastructuurbeperkingen).

Andere architecturale beslissingen zijn **jouw verantwoordelijkheid** binnen die beperkingen (databaseschema, API-ontwerp, componentstructuur, implementatiepatronen).

Details over welke beslissingen in welke categorie vallen worden gedeeld tijdens Sprint 1.

---

## Scrum events

Je werkt in **Sprints van twee weken** en gebruikt het Scrum framework.

De Scrum events zijn:
- Sprint Planning;
- Daily Scrum;
- Sprint Review (Demo);
- Retrospective.

De Scrum Master faciliteert deze events.
De Product Owner zorgt voor duidelijkheid over doelen en prioriteiten.

Alle teamleden nemen actief deel.

---

## Professionele verwachtingen

In dit project:
- zijn problemen en defects normaal;
- kunnen leveringsproblemen optreden;
- gaat niet alles zoals gepland.

Wat telt is **hoe je reageert**:
- onderzoek kalm;
- communiceer helder;
- respecteer kwaliteit en overeengekomen processen;
- neem beslissingen als team.

Dit project richt zich op **professioneel gedrag**, niet op het vermijden van fouten.

---

## Checklist eerste week

Zorg er in je eerste week voor dat je:
- [ ] Toegang hebt tot de GitHub repository
- [ ] Toegang hebt tot het Jira-project
- [ ] SSH-toegang hebt tot de TransIP VPS
- [ ] Toegang hebt tot Microsoft Teams
- [ ] De Sprint Guide voor Stagiairs hebt gelezen
- [ ] Het Definition of Ready template hebt gelezen
- [ ] Het Definition of Done template hebt gelezen
- [ ] De Product Vision hebt gelezen (inclusief de AVG-vereisten)
- [ ] Je teamrol begrijpt (Product Owner, Scrum Master, DevOps lead of Developer)
- [ ] Hebt deelgenomen aan de eerste Sprint Planning

**Specifiek voor de Product Owner:**
- [ ] AVG-vereisten ontvangen van staff/DPO
- [ ] Privacy by design principes begrijpen

---

## Slotopmerking

Je wordt vertrouwd met echte verantwoordelijkheid.

Gebruik dat vertrouwen goed:
- praat met elkaar;
- maak beslissingen expliciet;
- reflecteer en verbeter elke Sprint.

Staff is er om te **coachen en uitdagen**, niet om problemen voor je op te lossen.

---

**Einde Onboardinggids voor Stagiairs v1.1**
