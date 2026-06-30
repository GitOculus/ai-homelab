# Optik — Jobansøgningspipeline

Optik er en agentstyret pipeline, der tager et stillingsopslag og producerer et målrettet CV og en ansøgning. Den eksisterer, fordi den repetitive del af jobansøgninger — at matche erfaring til et stillingsopslag, vælge den rigtige CV-variant, ramme tonen — er præcis den slags arbejde, en agent med den rette kontekst kan håndtere. Mennesket beholder de strategiske beslutninger.

Pipelinen blev bygget iterativt. Hver reel brug afslørede et hul — en hardcoded skabelon, en manglende output-mappe, et OCR-felt, der blødte ind i det næste — og hvert hul blev fikset og låst fast i en skill, så det ikke kunne ske igen.

## Sådan virker det

1. **Intake** — Et stillingsopslag ankommer som PDF eller link. Agenten udtrækker strukturerede felter: virksomhed, rolle, krav, ansvarsområder.
2. **Normalisering** — Råintakten bliver til en struktureret kontrakt med evidenskortlægning og kravscoring.
3. **Variantvalg** — Agenten scanner et bibliotek af CV-varianter, sammenligner deres dækning mod stillingsopslaget, og vælger den bedste.
4. **Målrettet udkast** — En ansøgning skrives med en stemme lært fra et korpus af tidligere ansøgninger, derefter efterbehandlet for naturlig tone.
5. **Multi-output** — Fem artefakter produceres: CV, ansøgning, stillingskontrakt, evidenskort og forbedringsefterslæb.

Hvert trin er en Hermes-skill, hvilket betyder at agenten kan forklare, ændre eller genkøre ethvert stadie isoleret.
