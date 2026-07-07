# Sentry — Investeringsdashboard med signalmotor

Sentry er et selv-hostet investeringsdashboard, der overvåger aktieindeks, makroøkonomiske indikatorer, markedsstemning og en signalmotor bygget på Thomas' egne AAII Asset Allocation-regler. Det viser, at agentsystemet ikke kun håndterer tekstopgaver og kodearbejde — det kan også drive et dataintensivt, regeldrevet system med scraping, backtesting og en webfrontend.

Samme agent, der skriver jobansøgninger og designer spilmekanikker, har også bygget, revideret og vedligeholder en investeringsplatform med realtidsdata og egne handelssignaler.

## Hvad systemet gør

Sentry samler data fra seks kilder i ét dashboard og evaluerer Thomas' akkumulerede allokeringsregler hver måned:

| Kilde | Data | Frekvens |
|-------|------|----------|
| Yahoo Finance | 12 globale indeks, aktier, råvarer, krypto | Dagligt |
| FRED | CPI, UE, BNP, Fed Funds, rentekurve | Varierer |
| AAII Sentiment Survey | Ugentlig stemningsmåling | Ugentligt |
| AAII Asset Allocation .xls | Månedlig allokeringsdata (443 måneder) | Månedligt |
| CBOE | VIX-futures (term structure) | Dagligt |
| multpl.com | Shiller CAPE, P/E, earnings yield | Dagligt |

### Signalregler

Kun ét købs- og ét salgssignal — resten er konfidensmodifikatorer, der vises som kontekst:

| Signal | Betingelse | Handling |
|--------|-----------|----------|
| **SELL** | Obligationer <10% i 3 sammenhængende måneder | Sælg, gå til kontanter |
| **STRONG BUY** | Aktier <50%, kontanter >30% i 2 måneder, UE >5,5% | Invester 75% af kontanter |
| Modifikatorer | Sentiment spread, UE vs sidste salg, rotation/deleverage | +1/+2 konfidensniveauer |

### Backtest (1990–2026, 100.000 USD start)

| Strategi | Slutbeløb | CAGR | Max drawdown |
|----------|-----------|------|-------------|
| **Fuld system** | **4,22M USD** | **10,8%** | **−24,5%** |
| S&P 500 buy-and-hold | 2,28M USD | 9,0% | −51,6% |
| Uden salgsregler | 1,95M USD | 8,5% | −49,2% |
| DCA 500 USD/måned | 1,10M USD | 6,8% | −48,7% |

Systemet lander på 10,8% CAGR mod S&P 500's 9,0% — men maks drawdown er under halvdelen (−24,5% mod −51,6%). Salgsreglen fangede toppene i både 2000 og 2007, og købsreglen fordelte kontanterne i de rigtige bunde.

## Hvad dette viser om systemet

Sentry demonstrerer tre ting, der ikke fremgår af de andre projekter:

**Dataintegration.** Agenten henter data fra seks uafhængige kilder med forskellige formater, frekvenser og adgangsmetoder — en FRED API, et Excel-ark fra en forenings hjemmeside, et Yahoo-finans-feed og en ugentlig sentimentmåling. Hver kræver sin egen scraper og fejlhåndtering.

**Regelautomation.** Thomas' allokeringsregler sad i et Google Sheet i årevis. Sentry oversatte dem til en eksekverbar signalmotor — ikke som en sort boks, men som et system agenten selv har revideret og forbedret gennem kopitest og backtest-iterationer.

**Backtesting som bevis.** Signalets værdi er ikke påstået — den er målt. Fire backtest-strategier med 36 års data, samme startbetingelser, samme målepunkter. Det giver et ærligt billede af, hvad reglerne kan og ikke kan.
