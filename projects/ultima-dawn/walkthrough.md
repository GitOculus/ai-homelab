# Gennemgang: Orkestrator-routing i aktion

Dette er et virkeligt eksempel på kanban-orkestratoren, der ruter opgaver til den rette domæneprofil, taget fra en aktiv udviklingssession.

## Kontekst

Ultima Dawns kanban-tavle var blevet nulstillet — alle gamle tickets arkiveret, databasen renset til blank tavle. Tre nye test-tickets blev oprettet for at validere den dynamiske routing og outputregistreringsworkflow. Orkestratorens opgave var at klassificere hver ticket ved at læse opgavebeskrivelsen og tilgængelige profil-skills, og derefter sende den til den rigtige profil.

## Opgaverne

### Opgave 1: Fase 1-udviklingsplan

**Indhold:** *Lav en udviklingsplan for Fase 1 af projektet — prioriter de kernesystemer der skal eksistere, før noget andet kan bygges.*

Dette var en tværdomæne-planlægningsopgave — ingen enkeltprofil ejede den. Orkestratoren scannede de tilgængelige profiler og deres skill-beskrivelser, og sendte den til **uodawn-director**, standardprofilen. Direktøren producerede en faset køreplan med systemskabelsesskelet, lore-fundament og visuel asset-pipeline, og gav derefter den formaterede version til uodawn-roadmap til dokumentation.

### Opgave 2: EarthDawn-loreplan

**Indhold:** *Skitsér lore-fundamentet for EarthDawn-udvidelsen — centrale fraktioner, zoner og den narrative krog der binder dette indhold til den eksisterende verden.*

Opgavereferencen handlede om lore, narrativ og verdensopbygning. Orkestratoren matchede dette til **uodawn-lore**-profilen, hvis skills nævner navngivning, narrativ og zone-identitet. Lore-profilen producerede en fraktionsoversigt med narrative kroge og zonebeskrivelser, skrevet i en stil, der var konsistent med den eksisterende verdenskanon. Outputtet blev postet direkte som en struktureret ticket-kommentar.

### Opgave 3: Forklaring af threading-mekanik

**Indhold:** *Forklar hvordan threading-mekanikken fungerer på systemniveau — kurven der binder færdighedsniveau til tråd-styrke, attunement-modellen, og hvordan den interagerer med eksisterende mekanikker.*

Dette var et systemsdesign-spørgsmål med numeriske elementer. Orkestratoren sendte den til **uodawn-systems** (fastlåst til deepseek-v4-pro for sin ræsonneringsevne). Systems-profilen producerede en detaljeret teknisk forklaring med den underliggende kurvemodel, attunement-regler og interaktionsnoter. Igen postet som en struktureret ticket-kommentar.

## Hvad dette demonstrerer

Tre forskellige opgavetyper, tre forskellige profiler, én orkestrator, der træffer routing-beslutningen uden hardcodede regler. Routing udledes fra hver profils deklarerede skill-beskrivelser på dispatcher-tidspunktet — hvis en ny profil blev tilføjet studiet, ville orkestratoren naturligt route til den, når dens skills matchede.

Alle outputs blev registreret som strukturerede ticket-kommentarer, ikke efterladt i worker-logs eller workspace-filer — en regel håndhævet af orkestratorskillen, patchet efter en tidligere kørsel hvor outputs forsvandt.
