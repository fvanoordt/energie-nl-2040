# Energieportfolio Nederland 2040
### Interactief systeemkostenmodel voor de elektriciteitstransitie

> *Welke mix van wind, zon, batterijen, kernenergie, interconnectie en gas(+CCS) levert de laagste totale systeemkosten bij voldoende leveringszekerheid — en wanneer wordt kernenergie een nettoverlies voor de samenleving?*

**→ [Open de tool](https://jouwnaam.github.io/energie-nl-2040)**

---

## Achtergrond

Dit model is gebouwd om één fundamenteel argument inzichtelijk te maken: beslissingen over het elektriciteitsysteem zijn geen optelsom van losse technologiekeuzes. Elke toevoeging verandert de waarde van alles wat er al in zit.

De methodiek is gebaseerd op het werk van **Lion Hirth** (value factor / marktwaardedepreciatie, 2013–2015), uitgebreid met:

- **Kannibaliseringseffect op kapitaalkosten** — niet alleen de marktwaarde van stroom daalt bij hoge penetratie, ook de financieringskosten stijgen doordat banken het terugverdienrisico inprijzen via een hogere WACC
- **Volledige systeemkosten** — inclusief netcongestie, curtailment, flexibiliteitspremie, interconnectie-infrastructuur en importpremie
- **Load duration curve** in drie segmenten die de realiteit van wind- en zoncorrelatie weerspiegelen
- **Nederlandse parameters** voor 2040 — geen fictief land, maar reële getallen

---

## Wat het model berekent

### Drie kernvragen per portfoliomix

| Vraag | Metric |
|---|---|
| Wat kost het systeem werkelijk? | Totale systeemkosten in €/MWh, all-in |
| Hoe zeker is de levering? | % van dark-doldrums-uren gedekt door binnenlandse bronnen |
| Is kernenergie een netto-investering of nettoverlies? | Kernmeerkosten vs. alternatief zonder kern bij gelijke zekerheid |

### Load duration curve — 3 segmenten

Het model rekent geen jaargemiddelden maar simuleert drie marktsegmenten:

| Segment | Uren/jaar | Typische situatie | Dominante bron |
|---|---|---|---|
| **Piek (A)** | ~500 | Winter, windstil, avond — *dark doldrums* | Gas(+CCS), kern, import |
| **Schouder (B)** | ~5.000 | Gemiddeld aanbod en vraag | Wind, zon, batterijen |
| **Dal (C)** | ~3.260 | Zomermiddag, veel zon/wind, lage vraag | Curtailment, batterijlading, export |

Curtailment is daardoor geen ruwe penetratieproxy maar een directe berekening van wat in segment C overblijft ná batterijlading en export via interconnectie.

### Het kantelpunt

De centrale grafiek toont waar de **effectieve LCOE van kernenergie** de **systeemwaarde van firm capaciteit** overstijgt. Voorbij dat punt is kernsubsidie per definitie een structurele overdracht aan de samenleving, geen efficiënte investering.

---

## Parameters en aannames

### Technologiekosten (standalone LCOE)

| Technologie | Standalone LCOE | Bron/toelichting |
|---|---|---|
| Wind offshore | €117/MWh | NL kabinetsbrief 2025 (strike price SDE++) |
| Zon | €45/MWh | Huidige tenderprijzen utility-scale |
| Kernenergie | €160/MWh | Hinkley Point C benchmark; exclusief extra infra |
| Gas CCGT | €95/MWh | Incl. capaciteitsvergoeding |
| Gas+CCS | €135/MWh + €18/MWh capaciteitsvergoeding | Hogere capex CO₂-afvang/opslag/transport; 90% afvangrate |
| Batterijen (V2G) | €10/MWh cycluskost | Inclusief bidirectioneel laden EVs |

### Kannibaliseringsopslag (effectieve LCOE)

Standalone LCOE's missen het centrale probleem: naarmate penetratie stijgt, dalen marktprijzen precies op de uren dat een technologie produceert. Dit verlengt terugverdientijden en verhoogt via hogere WACC de effectieve kapitaalkosten.

| Technologie | Opslag per 10pp penetratie |
|---|---|
| Wind | +5,5% op LCOE |
| Zon | +6,5% |
| Kern | +9,0% — zwaarder gewogen vanwege 25-jarige blootstelling en inflexibiliteit |

Interconnectie vermindert het kannibaliseringseffect (surplus kan worden geëxporteerd), maar dit voordeel erodeert wanneer buurlanden in dezelfde situatie zitten.

### Interconnectiekosten

Interconnectie is geen gratis optie:

- **Infrastructuur**: €1,75 mld/GW (gemiddelde van €1,5–2 mrd, geannualiseerd over 40 jaar)
- **Importpremie**: oploopt bij Europabrede windstilte — als Nederland importeert tijdens dark doldrums, zijn Duitsland, België en Denemarken vaak in dezelfde situatie

### Elektriciteitsvraag 2040

| Scenario | TWh/jaar | Toelichting |
|---|---|---|
| Laag | 120 TWh | Huidig verbruiksniveau |
| Midden | 160 TWh | TNO/PBL middenscenario (standaard) |
| Hoog | 200 TWh | Volledig elektrificiatiescenario industrie + warmte |

### Leveringszekerheid — definitie

Het model meet het percentage van de *dark-doldrums-uren* (~400–600 uur/jaar: wind <10% én zon ~0) dat wordt gedekt door **binnenlandse bronnen** — batterijen, kernrestproductie, gas(+CCS). Dit meet niet "hebben we wel of geen stroom" (Nederland heeft doorgaans voldoende gasvermogen om elk gat te vullen), maar hoeveel van het systeem op binnenlandse, prijszekere bronnen draait versus afhankelijk is van import tegen onzekere Europese schaarsteprijzen.

---

## Scenario's

| Scenario | Wind | Zon | Kern | Batterijen | Interconnectie | Gas+CCS |
|---|---|---|---|---|---|---|
| Max wind, geen kern | 28 GW | 42 GW | 0 GW | 25 GWh | 18 GW | 20% |
| Gebalanceerd (basis) | 22 GW | 38 GW | 3,2 GW | 20 GWh | 15 GW | 30% |
| Kern-zwaar (2 EPR's) | 15 GW | 30 GW | 6,4 GW | 10 GWh | 10 GW | 50% |
| NL als eiland | 22 GW | 38 GW | 3,2 GW | 30 GWh | 4 GW | 60% |
| Batterij-optimum | 25 GW | 42 GW | 0 GW | 45 GWh | 18 GW | 20% |

---

## Beperkingen en disclaimer

Dit is een **beleidsvisualisatie-instrument**, geen vervanging voor volledige systeemstudies. Beperkingen:

- Het model gebruikt drie marktsegmenten in plaats van een volledig uurresolutiemodel
- Prijscorrelaties tussen landen zijn gesimplificeerd (logaritmisch saturerend)
- Netcongestiekosten zijn als proxy meegenomen, niet als volledig netwerkmodel
- Kernenergie-aannames zijn gebaseerd op Hinkley Point C; Nederlandse EPR-kosten zijn onzeker
- V2G-adoptie richting 2040 is inherent onzeker

Voor beleidsbeslissingen: raadpleeg ENTSO-E TYNDP, ECN/TNO systeemstudies en PBL Klimaat- en Energieverkenning.

---

## Methodologische referenties

- Hirth, L. (2013). *The market value of variable renewables.* Energy Economics.
- Hirth, L. (2015). *The optimal share of variable renewables.* The Energy Journal.
- PBL/TNO (2023). *Klimaat- en Energieverkenning 2023.*
- ENTSO-E (2024). *Ten-Year Network Development Plan.*
- HM Government (2023). *Hinkley Point C — revised cost estimates.*

---

## Technische details

Het model is een zelfstandig HTML-bestand zonder externe afhankelijkheden behalve D3.js (geladen via CDN). Geen installatie nodig — open in elke moderne browser.

```
energie-portfolio-nl-2040.html   ← hernoem naar index.html voor GitHub Pages
README.md
```

*Ontwikkeld als communicatie-instrument voor het Nederlandse energiebeleidsdebat, 2025.*
