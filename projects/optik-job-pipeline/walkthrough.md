# Gennemgang: Optik i aktion

Denne gennemgang demonstrerer pipelinens mekanik ved hjælp af et illustrativt fiktivt stillingsopslag. Ingen reel virksomhed eller reel ansøgning refereres.

## Opslaget

En regional kommune udsender en opfordring til en **Digital Service Lead** — en der skal koordinere udrulningen af en ny borgerportal på tværs af fem afdelinger og arbejde med både tekniske og administrative teams. Opslaget nævner erfaring med tværgående projektkoordinering, digitalt servicedesign og forandringsledelse i en offentlig kontekst.

## Hvad pipelinen gjorde

### 1. Intake

Agenten modtog et link til den offentlige stillingsside. Den udtrak indholdet og parseserede det til strukturerede felter:

- **Rolle:** Digital Service Lead
- **Organisationstype:** Kommunal forvaltning
- **Primære ansvarsområder:** koordinere portaludrulning, stakeholder-management på tværs af fem afdelinger, servicedesign-workshops, leverandørkoordinering
- **Krav:** 3+ års digital projektkoordinering, offentlig erfaring foretrækkes, dansk sprog

### 2. Normalisering

Råintakten blev omdannet til en struktureret "jobkontrakt" — et maskinlæsbart dokument med scorede krav og et evidenskort. Dette er pipelinens interne arbejdsdokument, ikke noget mennesket ser direkte. Det afgrænser, hvad CV'et og ansøgningen skal adressere.

### 3. Variantvalg

Agenten vedligeholder et bibliotek af CV-varianter — ikke ét statisk CV, men flere versioner der fremhæver forskellige kombinationer af erfaring (digital transformation, projektledelse, offentligt arbejde, teknisk leverance). Hver variant scores mod jobkontraktens krav.

Til dette opslag havde varianten med stærkest dækning kombineret **digital transformationserfaring** med **tværgående projektkoordinering**. Den offentlige variant var tæt på, men smallere. Agenten valgte den bredere variant og markerede hullet — kendskab til dansk offentlig kontekst — til mennesket at adressere manuelt.

### 4. CV-udkast

Den valgte variant blev overlejret med opslagsspecifikt indhold: portaludrulningen blev kortlagt på lignende tidligere projekter, fem-afdelings-koordineringen blev forbundet til tidligere multi-stakeholder-arbejde, og forandringsledelsesvinklen blev hentet frem fra et projekt mennesket havde ledet, som ikke handlede eksplicit om forandringsledelse, men involverede de samme dynamikker.

### 5. Ansøgningsudkast

Ansøgningen blev genereret strukturelt først — matchende hvert nøglekrav til en konkret erfaring — derefter sendt gennem et stil-lag trænet på et korpus af tidligere ansøgninger. En sidste humaniseringsrunde fjernede skabelonsprog og justerede sætningsrytmen til menneskets faktiske stemme.

### 6. Outputs

Fem filer landede i output-mappen:

- `CV_DigitalServiceLead_DA.md` — det målrettede CV
- `ansoegning_DigitalServiceLead.md` — ansøgningen
- `jobkontrakt_DigitalServiceLead.json` — den strukturerede jobkontrakt
- `evidenskort_DigitalServiceLead.md` — hvilke krav der blev adresseret og hvordan
- `forbedringsefterslaeb_DigitalServiceLead.md` — hvad mennesket stadig skal gennemgå eller justere

## Bugs undervejs

Disse er mere lærerige end succesen:

**Raw-extract-læk.** Tidlige versioner af intake-pipelinen sammenkædede al udtrukket tekst fra en PDF til én klump, og mistede grænsen mellem "krav" og "om virksomheden." Systemet genererede derefter et CV, der hævdede erfaring med virksomhedens egen historie. Fikset ved at felt-opdele ekstraktionstrinnet.

**Hardcoded skabelon.** Den første ansøgningsskabelon var én struktur — åbning, brødtekst, afslutning — uanset rollen. En teknisk rolle og en strategisk rolle fik samme form. Løsningen var at lære fra et korpus på omkring 130 tidligere ansøgninger og lade skabelonen blive valgt dynamisk efter rollekategori.

**Manglende output-mapper.** Pipelinen skrev til stier som `output/cv/` og `output/ansoegning/` — men ingen af mapperne eksisterede ved første kørsel. Scriptet fejlede lydløst. Fikset ved at tilføje et mappe-sikringstrin ved pipelinestart.

## Hvad ændrede sig efter hver brug

Hver bug blev til en skill-opdatering. Pipelinen blev ikke bare fikset for den ene kørsel; agentens proceduremæssige hukommelse blev opdateret, så samme type bug ikke kunne gentage sig. Dette er kerne-designprincippet: systemet forbedres gennem brug, ikke gennem planlagte releases.
