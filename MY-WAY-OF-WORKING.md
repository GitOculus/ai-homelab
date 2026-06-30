# Min måde at arbejde på

Det her er en syntese af, hvordan Thomas arbejder, baseret på samtale-logs og interaktionshistorie — ikke en selvvurdering eller en personlighedsramme.

## Når noget nyt skal i gang

Thomas starter småt og itererer. Da han havde brug for et agentsystem, tegnede han ikke en monolitisk arkitektur først — han satte Hermes op, kørte det, fandt ud af hvad der gik i stykker, og fiksede det. Optik-job-pipelinen voksede på samme måde: hver bug fundet i produktion — raw-extract der lækkede felter, en hardcoded output-skabelon, mapper, der manglede ved første kørsel — blev til en fix, der blev ved med at virke, fordi den blev indbygget i en skill, som agenten følger. Han planlægger på beslutningspunktsniveau, ikke hele vejen.

## Læring

Han lærer ved at bygge. Han satte et autonomt agentsystem op, før han læste dybt om, hvordan de skal fungere. Da han havde brug for at forstå et nyt domæne — en medlemsorganisations digitale økosystem — fik han en agent til at besøge siderne én for én og producere resultater, i stedet for at læse om UX-audit-metodologi først.

## At afgrænse opgaver for andre

Han giver præcise, strukturerede briefs — afgrænsede leverancer, tone-instruktioner, eksplicitte begrænsninger — uanset om modtageren er et menneske eller en agent. Uklare instruktioner bliver afklaret, før arbejdet starter. Han forventer samme tydelighed tilbage: specifikke, verificerbare outputs, ikke opsummeringer.

## Når noget går i stykker

Han sporer den egentlige årsag i stedet for at lappe symptomet. Da et provider-navnemismatch blev ved med at dukke op i logs, ryddede han den forældede konfiguration fra hver fil i stedet for at vedligeholde et workaround-map. Da instruktionerne i en skill var forældede, opdaterede han skillen — med det samme, ikke senere. Spørgsmålet er altid: hvad skal rent faktisk ændres, så det ikke sker igen?

## Delegation

Han tilrettelægger systemet med tillid for øje — ved at mekanikken kan håndteres automatisk, så han kun rører ved det, der kræver hans dømmekraft. Men tillid opnås gennem konsekvent verifikation: han læser outputs, tjekker ræsonnementet, og hvis noget består gennemgangen, er det færdigt. Ingen dvælende second-guessing. Agenten er en forlængelse af hans arbejdshukommelse — ikke en instans, som han overlader problemer til og vender ryggen.
