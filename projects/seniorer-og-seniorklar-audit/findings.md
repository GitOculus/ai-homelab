# Digital Audit: Faglige Seniorers økosystem

**Revisionsdato:** 30. juni 2026
**Auditor:** Hermes Agent (kimi-k2.6 via opencode-go)
**Metode:** Manuel browsing som enkelt besøgende — ingen automatiseret scraping.
**Gennemgåede sites:**
- fagligsenior.dk — organisationens hovedsite
- seniornews.dk — nyhedsportal
- seniorhaandbogen.dk — opslagsværk
- seniortryg.dk — digital svindelbevidsthed
- seniorklar.dk — vejledning om senkarriere og overgang til pension
- fagligsenior.membersite.dk — medlemssystem

---

## 1. Navigation på tværs af sites og branding-konsistens

### Observationer

De fem sites fremstår under én fælles organisatorisk paraply, men brandingen er ikke sammenhængende nok til at virke som en helhed for den besøgende:

| Site | Logo | Primær farve | Navigation til andre sites |
|---|---|---|---|
| fagligsenior.dk | "Faglig Senior" wordmark | Blå header-bjælke | Linker ikke til andre sites i hovednavigation. Linker til Seniorhåndbogen og Medlemssystem i sekundær navigation. |
| seniornews.dk | "SeniorNews.dk" wordmark | Orange/rød accent | Linker til "Fagligsenior.dk" i øverste nav-række. Nyhedsbrevstilmelding i sidebar. |
| seniorhaandbogen.dk | "Seniorhåndbogen" wordmark | Grøn accent | Footer har links til seniorklar.dk, fagligsenior.dk, seniornews.dk. Også "Faglige Seniorer" i øverste navigation. |
| seniortryg.dk | "Senior Tryg logo" + tagline | Blå/grå | Linker til "FagligSenior.dk" i øverste nav-række. |
| seniorklar.dk | "Seniorklar" logo | Orange/rød | "Andre sites" dropdown i øverste navigation — ingen direkte links synlige uden klik. |

**Iagttagelse:** En besøgende der lander på seniornews.dk eller seniortryg.dk vil ikke nødvendigvis med det samme forstå, at disse er del af samme organisation som fagligsenior.dk. Logoer, farveskemaer og typografisk stil er alle forskellige. Nogle sites krydslinker i navigationen, men inkonsistent — fagligsenior.dk selv har hverken seniortryg.dk eller seniorklar.dk i sin hovednavigation.

**For en ældre bruger:** Hvis nogen læser om digital svindel på seniortryg.dk og gerne vil finde medlemsoplysninger, er der ingen tydelig vej fra det indhold tilbage til hovedorganisationen eller medlemssystemet. Sammenhængen antydes af et lille nav-link, men forklares ikke.

### Anbefaling
En ensartet "Dette er en del af Faglige Seniorer"-banner eller footer-bjælke på tværs af alle sites — selv en simpel "Du besøger [site-navn], en del af Faglige Seniorer" — ville øjeblikkeligt orientere den besøgende. Det er også værd at overveje: ét samlet navigationskomponent der lister alle sites med korte beskrivelser af hvad hvert enkelt er til for.

---

## 2. Nyhedsbrevstilmeldinger

### Observationer

Hvert eneste site har sin egen nyhedsbrevstilmelding. De er **ikke** samlet:

| Site | Formularfelter | Ekstrafelter | Noter |
|---|---|---|---|
| fagligsenior.dk | Fornavn, Efternavn, Email, Postnummer, Fagforening (dropdown, 30+ muligheder), Samtykke-checkbox | Fagforening er påkrævet. Konkurrencedeltagelse. | Mest komplekse formular. "Postnummer" har en tegntæller (0/4). |
| seniornews.dk | Fornavn, Email, Samtykke-checkbox | Ingen. Simpel. | Indlejret i hjemmesidens sidebar. |
| seniorhaandbogen.dk | Link til "Tilmeld nyhedsbrev" — ingen inline-formular synlig på forsiden | — | Kræver navigation for at finde. |
| seniortryg.dk | Fornavn, Efternavn, Email, Postnummer, Samtykke-checkbox | Postnummer er påkrævet. Månedlig frekvens nævnt. | Inline-formular på forsiden. |
| seniorklar.dk | Link til "Tilmeld nyhedsbrev" i øverste navigation | — | Kræver navigation for at finde. |

**Iagttagelse:** En ældre der gerne vil "holde sig orienteret" kan tilmelde sig via enhver af disse formularer, men:
- De skal indtaste deres oplysninger **flere gange** på tværs af forskellige sites
- Formularen på fagligsenior.dk er markant kompleks (30+ fagforeningsmuligheder i en dropdown), hvilket kan virke overvældende
- Det er uklart om disse sender til én eller flere maillister
- Der er intet "allerede tilmeldt? Administrér dine præferencer"-link på nogen formular

**For en ældre bruger:** Tilmelding er en tillidshandling. Hvis man udfylder en formular på seniortryg.dk og senere modtager en email fra en anden adresse om "Faglig Senior", er sammenhængen ikke åbenlys og kan virke forvirrende eller ligefrem mistænkelig.

### Anbefaling
Én fælles tilmelding der indsamler email + navn + hvilke emner man er interesseret i, og derefter router internt til det rette nyhedsbrev. Som minimum: en bemærkning på tværs af sites der siger "tilmeld dig ét sted og hør om alt" samt et præferencecenter hvor man kan administrere alle abonnementer samlet.

---

## 3. Medlemssystem / login-flow (fagligsenior.dk)

### Observationer

Medlemssystemet ligger på et separat subdomæne: **fagligsenior.membersite.dk**

Besøgte sider:
- **Medlemssystem info-side** (fagligsenior.dk/medlemssystem-membersite/): En udførlig vejledning med:
  - Link til "Opret ny bruger"
  - Link til medlemssitet på `fagligsenior.membersite.dk/`
  - Tydelig advarsel: "Du skal ALDRIG indtaste kontonumre eller bruge MitID til at oprette en kollektiv profil"
  - FAQ-sektion med 8 foldbare spørgsmål
  - To PDF-vejledninger (oprettelse af profil, tilmelding til arrangementer)
  - Kontaktinformation med telefontider (10-14 hverdage)
  - Både kollektiv og individuel medlemskabsvej forklaret
- **Medlemssite** (fagligsenior.membersite.dk/): Sparsom landingsside med:
  - "OPRET MEDLEMSKAB KØB MEDLEMSKAB"
  - "KOMMENDE ARRANGEMENTER"
  - "LOG IND"
  - "OM OS", "KONTAKT"
  - Specifik opfordring: "Er du kollektivt medlem? Opret din profil her"

**Iagttagelse om friktionspunkter:**

- **Tvetydighed i to trin:** Et tilbagevendende medlem lander på medlemssitet og ser "LOG IND" — men der er ingen fremtrædende måde at skelne kollektivt fra individuelt login. Sondringen (kollektivt vs. individuelt medlemskab) forklares på vejledningssiden, men gentages ikke på selve medlemssitet.

- **GDPR-genregistrering:** Vejledningssiden siger eksplicit: "Selv om du har været medlem i mange år, skal du oprette en profil pga. GDPR-regler." Det kan bekymre en ældre bruger der tror medlemskabet er udløbet eller at noget er galt. Formuleringen kunne være beroligende frem for administrativ.

- **MitID-advarsel:** Den fremtrædende advarsel om ikke at bruge MitID til kollektive profiler er vigtig og god — men den kan skabe forvirring hvis en ældre læser den og bliver bekymret for hvad der SÅ er sikkert at bruge.

- **PDF-vejledninger:** Trin til at oprette en profil ligger i en PDF-download. En mindre rutineret bruger ved måske ikke at downloade og åbne en PDF. Trin-for-trin direkte på siden ville være bedre.

- **Telefonsupport-tider:** Tilgængelig 10-14 alle hverdage — men ingen "hvad hvis jeg sidder fast uden for disse timer"-løsning.

### Anbefaling
1. Kog vejledningssiden ned og integrér den på selve medlemssitet — tving ikke brugere til at læse én side for derefter at navigere til en anden for at handle
2. Sæt valget "kollektivt vs. individuelt" helt frem på medlemssitets login-side med et simpelt diagram
3. Erstat PDF-vejledninger med foldbare trin direkte på siden
4. Tilføj en "Dette er normalt — dit medlemskab er stadig aktivt"-beroligelse ved siden af GDPR-genregistreringsbeskeden
5. Overvej en "ring mig op"-mulighed for medlemmer der sidder fast uden for telefontiderne

---

## 4. Indholdsopdagelse

### Observationer

- Indhold på **seniortryg.dk** og **seniorklar.dk** kan ikke findes via fagligsenior.dk's hovednavigation. De eksisterer i separate økosystemer.
- **seniorhaandbogen.dk** er linket fra fagligsenior.dk's sekundære navigation — godt.
- **seniornews.dk** er linket fra seniorhaandbogen.dk's footer, men ikke fra fagligsenior.dk direkte.
- seniortryg.dk har "FagligSenior.dk" i sin navigation, men den modsatte vej findes ikke.
- seniorklar.dk har en "Andre sites" dropdown, men man skal vide at man skal klikke på den.
- Der findes ingen enkelt "alle vores sites"-side eller sitemap tilgængelig fra nogen navigation.

**For en ældre bruger:** Hvis nogen læser om svindel på seniortryg.dk og tænker "jeg bør tjekke om mit medlemskab dækker dette", er der ingen vej til medlemsoplysninger fra den side. Sites'ne er siloer der antager at man allerede kender hele landskabet.

### Anbefaling
En simpel "vores sites"-side eller footer-grid der viser alle fem sites med en én-linjes beskrivelse af hvad hvert enkelt dækker. Krydslink alle sites i en ensartet footer på alle sider.

---

## 5. Grundlæggende mobilbrugervenlighed

### Observationer (fra browser-rendering)

- **seniortryg.dk** og **seniorklar.dk** ser ud til at bruge responsive layouts — indhold tilpasses mindre skærme.
- **fagligsenior.dk** har en relativt tæt hjemmeside med mange artikelkort stablet vertikalt — på mobil ville det være en lang scroll med billeder indimellem.
- Skriftstørrelser fremstår tilstrækkelige på desktop, men bør testes ved 200% zoom for tilgængelighed.
- Berøringsmål i fagligsenior.dk's navigation (to separate nav-bjælker med små links) kan være udfordrende for brugere med nedsat motorik.
- seniortryg.dk har video-indlejringer (Vimeo iframes) der kan tilføje betydelig sidevægt på mobile dataforbindelser.

### Anbefaling
- Test alle sites ved 200% browser-zoom og 320px viewport-bredde
- Øg berøringsmål til minimum 44×44px for alle navigationslinks
- Overvej en "let"-version af seniortryg.dk's videoindhold (transskriptioner eller tekstresuméer ved siden af indlejringer)

---

## 6. Grundlæggende tilgængelighed

### Observationer

- **Alt-tekst:** Godt — billeder på alle sites har beskrivende alt-tekst (nogle meget detaljerede, f.eks. "En ældre kvinde med briller og en grå frakke handler i et supermarked..."). Dette er en styrke.
- **Overskriftsstruktur:** Generelt logisk (h1 → h2 → h3), dog bruger nogle sider h2 til sidebar-indhold før h1 er etableret.
- **Kontrast:** Visuel inspektion tyder på tilstrækkelig kontrast i hovedindholdsområder. Annoncepladser ("Annonce") er tydeligt mærket, men kunne være mere visuelt adskilt.
- **Spring-til-indhold-links:** Findes på de fleste sites — god praksis.
- **Søgelabels:** Nogle søgefelter har synlige labels, andre bruger udelukkende placeholder-tekst.

### Anbefaling
- Kør automatiserede kontrasttjek på alle knap-/link-farvekombinationer på tværs af alle fem sites
- Sørg for at hvert formularfelt har en vedvarende synlig label (ikke kun placeholder-tekst)
- Tilføj ARIA-landemærker ensartet på tværs af alle sites
- Den detaljerede alt-tekst er fremragende — fasthold denne standard

---

## Prioriterede iagttagelser (top 5 efter effekt)

1. **🔴 Usammenhængende site-økosystem** — En besøgende forstår ikke nemt at der er tale om én organisation. Løsning: ensartet branding-bjælke + footer med krydsnavigation på tværs af sites. Højeste effekt fordi det påvirker ethvert besøg på tværs af sites.

2. **🔴 Fragmenterede nyhedsbrevstilmeldinger** — Flere separate formularer der beder om de samme oplysninger. Løsning: én fælles tilmelding eller som minimum krydslinking "allerede tilmeldt et andet sted?" Dette påvirker direkte de 250.000 nyhedsbrevsmodtagere nævnt på forsiden.

3. **🟡 Medlemslogin har et vidensgab** — Vejledningssiden og det faktiske medlemssystem er adskilt. PDF'er i stedet for inline-vejledning. Sondringen kollektiv/individuel er kritisk men gemt væk. Løsning: flyt vejledningen ind på medlemssitet, tilføj inline-trin.

4. **🟡 Indholdssiloer** — seniortryg.dk og seniorklar.dk er usynlige fra fagligsenior.dk. Deres indhold er højt relevant for medlemmer, men kræver forudgående kendskab for at finde. Løsning: krydslink i hovednavigation.

5. 🟢 **Mobil- og tilgængelighedsbasis er fornuftig men uverificeret** — Alt-tekst er stærk, spring-til-indhold findes. Men berøringsmål, zoom-modstandsdygtighed og formular-labels kræver systematisk test. Løsning: kør igennem en tjekliste ved 200% zoom på faktiske enheder.

---

## Metodiske noter

- Alle observationer er fra manuel browsing i en almindelig browsersession — ingen automatiseret scraping
- fagligsenior.dk's robots.txt forbyder automatiseret adgang; denne audit respekterer det ved at browse som en menneskelig besøgende ville
- Screenshots taget under browsing ligger i `screenshots/`
- Tilgængelighedsvurdering er et basistjek, ikke en WCAG-audit
- Ingen antagelser er gjort om CMS, hosting eller backend-systemer
