# Energieportfolio Nederland 2040
### Interactief systeemkostenmodel voor de elektriciteitstransitie

> *Welke mix van wind, zon, batterijen, kernenergie, interconnectie en gas(+CCS) levert de laagste totale systeemkosten bij voldoende leveringszekerheid — en wanneer wordt kernenergie een nettoverlies voor de samenleving?*

**→ [Open de tool](https://jouwnaam.github.io/energie-nl-2040)**

---

## Achtergrond

Dit model maakt één fundamenteel argument inzichtelijk: beslissingen over het elektriciteitssysteem zijn geen optelsom van losse technologiekeuzes. Elke toevoeging verandert de waarde van alles wat er al in zit.

De methodiek is gebaseerd op het werk van **Lion Hirth** (value factor / marktwaardedepreciatie, 2013–2015), uitgebreid met:

- **Kannibaliseringseffect op kapitaalkosten** — niet alleen de marktwaarde van stroom daalt bij hoge penetratie, ook de financieringskosten stijgen doordat banken het terugverdienrisico inprijzen via een hogere WACC
- **Load duration curve in 4 segmenten** — verdeelt het jaar in piek, schouder-hoog, schouder-laag en dal, waardoor curtailment realistisch wordt berekend per marktsegment
- **Volledige systeemkosten** — inclusief netcongestie, curtailment/export, flexibiliteitspremie, interconnectie-infrastructuur en importpremie
- **Nederlandse parameters voor 2040** — geen fictief land, maar reële getallen

---

## Wat het model berekent

### Vijf KPI's per portfoliomix

> **Reikwijdte systeemkosten:** dit model omvat aanbodzijde-effecten (curtailment, redispatch, flexibiliteitspremie, interconnectie-infrastructuur). Vraagzijde-netwerkkosten voor warmtepompen, EV en industriële elektrificiatie zijn buiten scope — deze zijn grotendeels technologieneutraal en beïnvloeden de onderlinge vergelijking tussen wind, zon en kern nauwelijks.

| KPI | Wat het meet |
|---|---|
| Systeemkosten | €/MWh all-in, inclusief kannibalisering |
| Curtailment / export | % weggegooid of geëxporteerd (in praktijk grotendeels curtailment — buurlanden hebben op dezelfde uren ook surplus) |
| Kernmeerkosten | €/MWh extra t.o.v. zelfde zekerheid zonder kern — toont ook hoeveel TWh kern levert tijdens overaanbod-uren (feitelijke productiestatistiek, geen curtailment-toewijzing) |
| Interconnectiekosten | €/MWh infrastructuur + importpremie |
| Gas+CCS all-in | €/MWh inclusief capaciteitsvergoeding |

### Dark doldrums — leveringszekerheid in concrete uren

Van de ~500 uur/jaar dat wind én zon vrijwel niets leveren, toont het model per dekkingsbron hoeveel uur wordt gedekt — er is *altijd* stroom, maar de herkomst verschilt:

| Bron | Rol |
|---|---|
| 🔋 Batterij / V2G | Opgeslagen wind/zon uit dal-uren |
| ⚛️ Kernenergie | Doorlopende baseload-productie |
| 🏭 Gas (kaal / +CCS) | Capaciteitsmechanisme actief — binnenlands, dispatchable |
| 🌍 Import | Laatste redmiddel — Europese marktprijs, onzeker |

### Load duration curve — 4 marktsegmenten

De segmenten zijn benoemd naar marktconditie (schaarste of overschot), niet naar tijdstip — namen als "dal zomermiddag" suggereren een kort, zeldzaam venster terwijl het in werkelijkheid om duizenden uren per jaar gaat.

| Segment | Uren/jaar | Marktconditie | Dominante bron |
|---|---|---|---|
| **Schaarste-uren** | ~500 | Weinig wind/zon, hoge vraag — *dark doldrums* | Gas(+CCS), kern, import |
| **Overschot-uren (matig)** | ~2.000 | Redelijk wind/zon, gemiddelde vraag — surplus mogelijk | Wind+zon, export, batterijlading |
| **Krapte-uren (regulier)** | ~3.000 | Weinig zon, wisselend wind — structureel tekort | Wind, gas, batterij ontlading |
| **Overschot-uren (hoog)** | ~3.260 | Veel wind/zon, lage vraag | Curtailment/export, batterijlading |

Curtailment ontstaat in de overschot-uren (matig én hoog) én op winderige nachten binnen de krapte-uren. Export is beperkt omdat buurlanden op dezelfde uren hetzelfde surplus hebben (Europese correlatie).

### Het kantelpunt

De centrale grafiek toont waar de **effectieve LCOE van kernenergie** de **systeemwaarde van firm capaciteit** overstijgt. Voorbij dat punt is kernsubsidie per definitie een structurele overdracht, geen efficiënte investering.

---

## Parameters en aannames

### Technologiekosten (standalone LCOE)

| Technologie | Standalone LCOE | Bron/toelichting |
|---|---|---|
| Wind offshore (nieuwbouw) | €117/MWh | NL kabinetsbrief 2025 (strike price SDE++) |
| Wind onshore (basis) | €85/MWh | Vaste 7 GW bestaand, grotendeels afgeschreven |
| Zon | €45/MWh | Huidige tenderprijzen utility-scale |
| Kernenergie | €160/MWh | Hinkley Point C benchmark; excl. extra infrastructuur |
| Gas CCGT (kaal) | €95/MWh | Incl. capaciteitsvergoeding |
| Gas+CCS | €135 + €18/MWh | Hogere capex CO₂-afvang/opslag; 90% afvangrate; €18 = capaciteitsvergoeding |
| Batterijen + V2G | €10/MWh cycluskost | ~200 cycli/jaar; send-out 4-6 uur; incl. bidirectioneel laden EVs |

### Kannibaliseringsopslag (effectieve LCOE)

Standalone LCOE's missen het centrale probleem: naarmate penetratie stijgt, dalen marktprijzen precies op de uren dat een technologie produceert. De effectieve LCOE wordt afgeleid uit de LDC-uitkomsten (surplusFrac en segBpressure), consistent met de curtailment-berekening.

| Technologie | Maximale opslag bij hoge penetratie | Reden |
|---|---|---|
| Wind offshore | ~45% | Gecorreleerde productie; hogere WACC bij lage verwachte marktprijzen |
| Zon | ~55% | Sterke dagcorrelatie; zomermiddag-concentratie |
| Kern | ~80% | 25-jarige blootstelling + baseload-inflexibiliteit; interconnectie helpt minder |

### Interconnectiekosten

Interconnectie is geen gratis optie:
- **Infrastructuur**: €1,75 mld/GW (subsea kabels + converterstations), geannualiseerd over 40 jaar
- **Importpremie**: oploopt bij Europabrede windstilte — als Nederland importeert tijdens dark doldrums, zijn Duitsland, België en Denemarken vaak in dezelfde situatie
- **Exportbeperking**: bij hoge VRE-penetratie is de exportwaarde laag — buurlanden hebben op zomermiddagen zelf ook surplus; max ~25-35% van surplus kan worden geëxporteerd

### Elektriciteitsvraag 2040

| Scenario | TWh/jaar | Toelichting |
|---|---|---|
| Laag | 120 TWh | Huidig verbruiksniveau |
| Midden | 160 TWh | TNO/PBL middenscenario (standaard) |
| Hoog | 200 TWh | Volledig elektrificiatiescenario industrie + warmte |

---

## Snelscenario's

| Scenario | Wind offshore | Zon | Kern | Batterijen | Interconnectie | Gas+CCS |
|---|---|---|---|---|---|---|
| Max wind, geen kern | 28 GW | 42 GW | 0 GW | 25 GWh | 18 GW | 20% |
| Gebalanceerd (basis) | 22 GW | 38 GW | 3,2 GW | 20 GWh | 15 GW | 30% |
| Kern-zwaar (2 EPR's) | 15 GW | 30 GW | 6,4 GW | 10 GWh | 10 GW | 50% |
| NL als eiland | 22 GW | 38 GW | 3,2 GW | 30 GWh | 4 GW | 60% |
| Batterij-optimum | 25 GW | 42 GW | 0 GW | 45 GWh | 18 GW | 20% |

*Wind offshore is nieuwbouw bovenop 6,4 GW bestaand. Onshore: vaste 7 GW basis.*

---

## Beperkingen en disclaimer

Dit is een **beleidsvisualisatie-instrument**, geen vervanging voor volledige systeemstudies. Beperkingen:

- Het model gebruikt 4 marktsegmenten in plaats van een volledig uurresolutiemodel; curtailment wordt daardoor **structureel onderschat** (werkelijk 30-50% hoger dan de modeluitkomst, vergelijkbaar met ~12-18% bij 85%+ penetratie vs. ~8-10% in dit model). Dit betekent ook dat de systeemkosten aan de **conservatieve kant** zijn — het werkelijke nadeel van hoge VRE-penetratie zonder adequate opslag/export is groter dan dit model toont.
- Prijscorrelaties tussen landen zijn gesimplificeerd
- Netcongestiekosten zijn als proxy meegenomen, niet als volledig netwerkmodel
- Kernenergie-aannames gebaseerd op Hinkley Point C; Nederlandse EPR-kosten zijn onzeker
- V2G-adoptie richting 2040 inherent onzeker

Voor beleidsbeslissingen: raadpleeg ENTSO-E TYNDP, ECN/TNO systeemstudies en PBL Klimaat- en Energieverkenning.

---

## Methodologische referenties

- Hirth, L. (2013). *The market value of variable renewables.* Energy Economics.
- Hirth, L. (2015). *The optimal share of variable renewables.* The Energy Journal.
- PBL/TNO (2023). *Klimaat- en Energieverkenning 2023.*
- ENTSO-E (2024). *Ten-Year Network Development Plan.*
- HM Government (2023). *Hinkley Point C — revised cost estimates.*
- NL Kabinetsbrief (2025). *SDE++ tenderprijzen windenergie op zee.*

---

## Technische details

Zelfstandig HTML-bestand (~81KB). Vereist internetverbinding voor D3.js (geladen via CDN). Werkt in elke moderne browser — geen installatie nodig.

```
index.html    ← het model (hernoem energie-portfolio-nl-2040.html naar index.html)
README.md     ← deze toelichting
```

*Ontwikkeld als communicatie-instrument voor het Nederlandse energiebeleidsdebat, 2025–2026.*
