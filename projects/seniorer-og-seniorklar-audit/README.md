# Seniorer og SeniorKlar Audit

Dette er et eksempel på at bruge en autonom agent til at få et hurtigt, struktureret overblik over et ukendt digitalt økosystem — i dette tilfælde de fem offentlige websites for en medlemsorganisation, der betjener et ældre, mindre digitalt vant publikum.

Pointen er at demonstrere **metoden**, ikke konklusionen. Tilgangen kan reproduceres for enhver organisation med en multi-site webtilstedeværelse:

1. Besøg hvert site som en rigtig bruger ville, side for side — ingen automatiseret scraping
2. Katalogiser fund per site: struktur, styrker, friktionspunkter
3. Krydsreferer: kortlæg hvordan siderne hænger sammen (eller ej) fra en brugers perspektiv
4. Sammenfat til en prioriteret kortliste — de 3-5 vigtigste ting at fikse først

Dette var en første-gennemgang. En dybere audit ville inkludere analysedata, brugertests og stakeholder-interviews. Men til en hurtig orientering — den slags man måske leverer i sine første uger i en ny rolle — fanger den de mønstre, der betyder noget.

## Leverancer

| Fil | Hvad det er |
|---|---|
| [`findings.md`](findings.md) | Fuld struktureret audit — observationer per site, tværgående problemstillinger, prioriterede anbefalinger |
| `screenshots/` | Annoterede skærmbilleder fra hvert site under gennemgangen |

## Værktøj

Bygget med Hermes Agent (kimi-k2.6 på opencode-go), ved brug af hensynsfuld manuel browserautomation — én side ad gangen, ingen bulk-crawling. Skærmbilleder fanget under live browsing, præcis som en rigtig bruger ville se dem.
