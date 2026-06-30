# Ultima Dawn — Spildesign-kompagnon

Ultima Dawn er et personligt kreativt projekt: et server-side spildesign bygget på ModernUO (Ultima Online-serveremulator). Det er ikke klientarbejde eller et kommercielt produkt — det er en designsandkasse til at bygge systemer, mekanikker, lore og visuelle elementer fra bunden.

Dette projekt findes her for at demonstrere, at agentsystemet er **general-purpose**. Den samme infrastruktur, der håndterer jobansøgninger og site-audits, håndterer også kreativt arbejde — gennem domænespecialiserede agentprofiler og en orkestrator der ruter opgaver til den rigtige profil.

## Hvad systemet gør for dette projekt

Spillet berører flere discipliner — serverkode, kampbalance, narrativ skrivning, visuelt design, dokumentation — og hver kræver en anden tilgang. I stedet for at bruge én agent til alt, vedligeholder systemet **specialiserede profiler**, der vælges automatisk baseret på opgavetype:

| Profil | Håndterer | Fastlåst model |
|---|---|---|
| `uodawn-systems` | C# serverkode, mekanik, matematik | deepseek-v4-pro |
| `uodawn-pvp` | Kampregler, balancetuning | deepseek-v4-pro |
| `uodawn-lore` | Narrativ, verdensopbygning, navngivning | kimi-k2.6 |
| `uodawn-visual` | UI, Gump-layouts, ikoner, farver | kimi-k2.6 |
| `uodawn-roadmap` | Dokumentation, fase-tracking | deepseek-v4-flash |
| `uodawn-director` | Orkestrering, tværdomæne-designbeslutninger | deepseek-v4-flash |

Orkestratoren (`dispatch-route.py`) klassificerer indkommende opgaver efter indhold og ruter dem til den matchende profil. Når en opgave berører flere domæner — et væsen der har brug for både mekanik og lore, for eksempel — arbejder begge profiler på den og director-profilen forener resultaterne. Alt arbejde spores gennem en fælles kanban-tavle med en Vikunja-frontend til menneskelig gennemgang.

## Også relevant

Dette afspejler en personlig interesse for spil- og interaktivt design — den samme slags systemtænkning, afbalancering og brugervenlighed, der gælder for interaktive læringsværktøjer, quizbyggere eller ethvert digitalt oplevelsesdesign.
