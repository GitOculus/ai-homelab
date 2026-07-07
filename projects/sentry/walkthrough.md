# Gennemgang: Fra regneark til signalmotor

Sentrys signalregler opstod ikke som kode. De sad i et Google Sheet — 443 måneders AAII Asset Allocation-data med Thomas' annoteringer, farvekodede celler og håndindtastede signalvurderinger. At gøre dem til en eksekverbar motor krævede ikke bare at oversætte formler, men at forstå hvilke regler der **holdt stik** og hvilke der var **støj**.

## Første udgave: Hvad reglerne sagde

Da Sentrys signalmotor først blev bygget, blev alle Thomas' Sheet-noter læst som regler. Det gav et system med syv signaltyper, et kompositscore-system og flere købs- og salgstrin — WEAK BUY, MODERATE BUY, STRONG BUY, SELL, DE-RISK, RE-ENTER.

Problemet var, at mange af dem ikke holdt til backtest.

## Kopitesten: Hvad der rent faktisk virkede

En måned inde i udviklingen kørte en grundig kopitest mod det oprindelige Sheet. Hver regel blev testet: finder den de rigtige tidspunkter? overlever den et skiftende regime? giver den falske alarmer?

Resultatet reducerede motoren til én salgsregel og én købsregel:

**Salg.** Obligationer under 10% i tre måneder — intet andet. Alt andet, der så ud som et salgssignal (rotation, deleverage, sentiment), blev til konfidensmodifikatorer. De vises i dashboardet, men de udløser ikke handler.

**Køb.** Kun STRONG BUY — aktier under 50%, kontanter over 30% i to måneder, og arbejdsløshed over 5,5%. WEAK BUY og MODERATE BUY blev testet og droppet — de spredte kontantreserven på for mange positioner og forringede afkastet.

## Backtest-resultatet

| Strategi | CAGR | Max DD |
|----------|------|--------|
| Fuld system | **10,8%** | **−24,5%** |
| S&P 500 B&H | 9,0% | −51,6% |
| Uden salgsregler | 8,5% | −49,2% |

Systemet med kun to signalregler slog både buy-and-hold (betydeligt) og en version med alle impulssignaler (mærkbart). Den lavere drawdown kommer fra salgsreglen — den fangede toppunkterne i både 2000 og 2007. Den højere CAGR kommer fra at blive siddende i kontanter i stedet for at jagte afkast med for svage købssignaler.

## Kodetest: Hvad der sad tilbage

Efter regelreduktionen blev selve koden gennemgået — det viste sig, at den første implementering havde efterladt død kode fra tidligere iterationer:

- DE-RISK og DE-RISK HIGH havde næsten identiske tærskler
- En kompositscore med syv vægtede komponenter, hvoraf to modstridde signalreglerne (arbejdsløshed talte for lav risiko, når signalet brugte høj UE som købssignal)
- Bullish Z-score-modifikatoren fremtvang MAXIMUM på ethvert signal — meningsløst

Kodetesten ryddede op. Sentry har i dag én signalside med én salgsregel, én købsregel og fire visningsmodifikatorer — intet andet. Dashboardet har siden da gennemgået yderligere revisioner: frygtmåler, kreditstressindikator, rentekurve og en værdiansættelsessektion.

## Hvad dette viser

Sentrys historie er ikke én om at bygge det perfekte system første gang. Det er historien om at tage et eksisterende sæt menneskelige regler, oversætte dem til kode, teste dem mod virkeligheden — og have disciplin nok til at smide dem ud, der ikke bestod testen.
