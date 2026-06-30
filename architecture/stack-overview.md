# Arkitektur & Stack

## Kort fortalt

Systemet kører en autonom AI-agent (Hermes) inde i en Proxmox Linux-container. Agenten kommunikerer over Signal, modtager opgaver fra en kanban-tavle (Vikunja), og kan browse på nettet, læse og skrive filer, køre scripts og starte subagenter. Når en opgave ankommer, klassificerer den typen af arbejde — skrivning, ræsonnement, kode, research — og skifter til den bedste model til jobbet. Output løber tilbage gennem kanban-tickets, vault-noter eller direkte beskeder. Et letvægts bridge-API og en n8n-automationsserver, begge i containere ved siden af agenten, binder det hele sammen.

---

## Fuld teknisk gennemgang

### Host

- Proxmox VE hypervisor
- Uprivilegeret Debian 13 Trixie LXC (`ailab`)
- 4 GB RAM · 20 GB disk · en enkelt offentlig IP

### Agent

- **Hermes Agent** (v0.17.0) af Nous Research — CLI AI-agentframework
- Kører via `opencode-go` provider (OpenRouter-kompatibel, ingen API-nøgle nødvendig for basismodeller)
- Standardmodel: `deepseek-v4-flash` (1M kontekst, $0,14/$0,28 per 1M tokens)
- Evnebevidst modelrouting via `model-classifications.yaml` (18 modeller × 8 evnedimensioner)
- Når en opgave ankommer, klassificerer `route.py` den og skifter til den bedst egnede model — `deepseek-v4-pro` til dybdegående analyse, `kimi-k2.6` til skrivning, `minimax-m3` til billig opsummering
- Falder tilbage til `step-3.7-flash:free` på Nous Portal, når primær provider er utilgængelig

### Agentprofiler

Otte Hermes-profiler, hver fastlåst til en formålstilpasset model:

| Profil | Model | Rolle |
|---|---|---|
| `default` | deepseek-v4-flash | Primær interaktion, Optik-pipeline |
| `orchestrator` | deepseek-v4-flash | Kanban-dispatch, opgavekoordinering |
| `uodawn-director` | deepseek-v4-flash | Designoverblik, gennemgang |
| `uodawn-systems` | deepseek-v4-pro | Kode, mekanik, matematik |
| `uodawn-pvp` | deepseek-v4-pro | Kampregler, balance |
| `uodawn-lore` | kimi-k2.6 | Narrativ, verdensopbygning |
| `uodawn-visual` | kimi-k2.6 | UI, kreativt, visuelt design |
| `uodawn-roadmap` | deepseek-v4-flash | Dokumentation, tracking |

To routingstrategier arbejder sammen: `dispatch-route.py` klassificerer kanban-opgavetitler til den rigtige profil ved oprettelse; `route.py` skifter model inden for en session per opgave.

### Menneskegrænseflade

- **Signal** — primær kanal. Thomas sender beskeder, PDF'er, links. Agenten svarer med tekst og filer.
- **Signal-quirk:** daemonens websocket-forbindelse forhindrer iPhone-push-beskeder i at komme frem. Kendt, uløst.

### Kanban & Automation

- **Vikunja** (Podman) — menneskevenlig kanban. Tre projekter (director, systems, visual) med hver seks buckets (Triage → Todo → Ready → Running → Blocked → Done). Webhooks affyres ved opgaveoprettelse, opdatering og kommentar.
- **Bridge API** (`bridge_api.py`) — custom Python HTTP-server. Synkroniserer tovejs: Vikunja-webhooks → Hermes kanban-DB, og Hermes kanban-ændringer → Vikunja (via en inotify-watcher på DB-filen). Kører som systemd-service `hermes-vikunja-bridge.service`.
- **n8n** (Podman) — automationshub. Overvåger Obsidian-vaultet for ændringer og fodrer nye eller opdaterede noter ind i bridgeen som opgaver.
- **Planka** (Podman) — skrivebeskyttet spejl af kanban-tavlen. MCP-wrapper på `planka_mcp.py`.

### Skills-system

84 skills organiseret efter kategori. Skills er agentens proceduremæssige hukommelse — markdown-filer med YAML-frontmatter, der definerer gentagne opgave-workflows. Vigtigste custom skills:

- `optik-application-mentor` — end-to-end jobansøgningspipeline
- `model-router` / `provider-router` — evnebevidst modelskift
- `kanban-orchestrator` — kanban-dispatch med obligatorisk outputregistrering på tickets
- `humanizer` — post-processing, der af-AI-fiser genereret tekst
- `uodawn-intake-routing` — dynamisk profiltrouting til spildesignopgaver
- Operationelle skills: smoke-test, code-review, systematic-debugging

### Videnslag

- **Hermes memory** (~2200 tegn) — brugerpræferencer, miljøfakta, holdbare konventioner
- **Hermes skills** — proceduremæssige workflows (ubegrænset)
- **Obsidian vault** (`vault/`) — delt videnslag. Projektnoter, arkitekturbeslutninger, dyb reference. n8n overvåger det; nye noter kan blive til kanban-opgaver.

### Pipeline-eksempel: Seniorer og SeniorKlar Audit

Agenten fik et brief om at revidere et medlemsorganisations digitale økosystem på fem websites for brugervenlighed, tilgængelighed og medlemsrejse-friktion. Ved at bruge browserautomation som en enkelt besøgende bruger besøgte den hvert site side for side, katalogiserede tværgående navigationshuller, nyhedsbrevsduplikering, login-friktion og mobil-brugervenlighed. Den producerede et struktureret findings-dokument med prioriterede anbefalinger og annoterede screenshots — alt sammen leveret gennem den samme Signal-kanal, Thomas bruger til alt andet. Opgaven viste agenten som research-assistent, ikke som kodegenerator.
