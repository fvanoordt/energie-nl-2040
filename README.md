# Energieportfolio Nederland 2040
### Interactief systeemkostenmodel voor de elektriciteitstransitie

> *Geen enkele technologie in dit systeem staat op zichzelf: meer wind drukt de prijs van wind, meer kern verandert wat batterijen waard zijn, meer interconnectie verschuift een probleem eerder dan dat het verdwijnt. Welke mix van wind, zon, batterijen, kernenergie, interconnectie en gas(+CCS) daaruit volgt, en wat die kost, is precies wat dit model laat zien.*

**→ [Open de tool](https://jouwnaam.github.io/energie-nl-2040)**

---

## Waar dit model wel en niet voor is

Dit is een **leerinstrument over systeemdenken**, geen pleidooi vóór of tegen een technologie. Het maakt één argument inzichtelijk: beslissingen over het elektriciteitssysteem zijn geen optelsom van losse technologiekeuzes — elke toevoeging verandert de waarde van alles wat er al in zit. Wind drukt de marktwaarde van bestaande wind. Kern die doordraait tijdens overaanbod drukt zijn eigen terugverdientijd. Batterijen en interconnectie dempen dat effect, maar lossen het niet op — en kosten zelf ook geld.

Het model rekent geen technologie rijk of arm. Waar uitkomsten een technologie duur of gunstig laten lijken, is dat een uitkomst van de aannames die je zelf instelt (inclusief de expliciete keuze tussen twee kern-bouwrealiteiten, zie verderop) — niet een ingebouwd oordeel. De bedoeling is dat je zelf concludeert, of op zijn minst ziet dát het een afweging is.

De methodiek is gebaseerd op het werk van **Lion Hirth** (value factor / marktwaardedepreciatie, 2013–2015), uitgebreid met:

- **Kannibaliseringseffect op kapitaalkosten** — niet alleen de marktwaarde van stroom daalt bij hoge penetratie, ook de financieringskosten stijgen doordat banken het terugverdienrisico inprijzen via een hogere WACC
- **Load duration curve in 4 segmenten** — verdeelt het jaar in schaarste, twee schouderconditie en overschot, waardoor curtailment realistisch wordt berekend per marktsegment
- **Vermogensadequaatheid met endogene gasvloot** — een aparte toets of er op het piekmoment genoeg beschikbaar vermogen staat, waarbij de benodigde gasvloot meebeweegt met de rest van de mix
- **Capaciteitsmechanisme** — een expliciete, aparte kostenpost voor het in stand houden van die gasvloot, los van hoeveel gas daadwerkelijk draait
- **Interconnectie-correlatiemodel** — vervangt een platte de-ratingaanname door een 2-groepen-model (gecorreleerde NW-Europese buren vs. Noorse waterkracht), gebaseerd op Malvaldi et al. (2017)
- **Volledige systeemkosten** — inclusief netcongestie, curtailment/export, flexibiliteitspremie, interconnectie-infrastructuur en importpremie
- **Nederlandse parameters voor 2040** — geen fictief land, maar reële getallen

---

## Wat het model berekent

### Zes KPI's per portfoliomix

> **Reikwijdte systeemkosten:** dit model omvat aanbodzijde-effecten (curtailment, flexibiliteitspremie, interconnectie-infrastructuur, capaciteitsmechanisme). Vraagzijde-netwerkkosten voor warmtepompen, EV en industriële elektrificatie zijn buiten scope qua netwerkkosten — de vráág die warmtepompen genereren zit wél in het model (zie "Elektriciteitsvraag 2040" hieronder). Nederland wordt behandeld als één knooppunt zonder interne transportbeperkingen ("koperen plaat") — redispatch-kosten voor lokale netcongestie zitten er dus niet in (zie Beperkingen).

| KPI | Wat het meet |
|---|---|
| Systeemkosten | €/MWh all-in, inclusief kannibalisering en capaciteitsmechanisme |
| Curtailment / export | % weggegooid of geëxporteerd — 0% betekent niet automatisch "geen kannibalisering", zie toelichting verderop |
| Kernmeerkosten | €/MWh extra t.o.v. zelfde leveringszekerheid zonder kern — alleen zichtbaar als kern > 0 GW |
| Interconnectiekosten | €/MWh infrastructuur + importpremie |
| Gas+CCS variabel | €/MWh — puur variabele kosten; de capaciteitscomponent is verhuisd naar het capaciteitsmechanisme |
| Benodigd back-upvermogen | GW gasvloot die endogeen nodig is om het vereiste piekvermogen te dekken, plus de bijbehorende kostprijs via het capaciteitsmechanisme |

### Dark doldrums — leveringszekerheid in concrete uren

Van de ~500 uur/jaar dat wind én zon vrijwel niets leveren, toont het model per dekkingsbron hoeveel uur wordt gedekt — er is *altijd* stroom, maar de herkomst verschilt:

| Bron | Rol |
|---|---|
| 🔋 Batterij / V2G | Opgeslagen wind/zon uit dal-uren |
| ⚛️ Kern + restproductie wind/zon | Doorlopende kernproductie plus het beetje wind/zon dat er nog is |
| 🏭 Gas (kaal / +CCS) | Capaciteitsmechanisme actief — binnenlands, dispatchable |
| 🌍 Import | Laatste redmiddel — Europese marktprijs, onzeker |

### Systeemkosten in € miljard/jaar — vergelijking, geen norm

Onder de Systeemkosten-KPI staat een verschil in € miljard/jaar t.o.v. een referentiescenario dat je zelf kiest (knop "Huidig scenario vastzetten als referentie", standaard "Gebalanceerd" — een neutraal startpunt, geen ingebouwde norm). De referentie wordt herrekend met dezelfde vraag en kern-bouwaanname als je huidige instelling, zodat de delta puur het effect van de portfoliokeuze isoleert.

**Precisie:** het bedrag is afgerond op €0,1 miljard en indicatief — het model heeft geen precisie op individuele-euro-niveau (zie Beperkingen). Een miljardenbedrag oogt overtuigender dan een €/MWh-verschil, maar heeft dezelfde onderliggende onzekerheid.

### Vermogensadequaatheid — endogene gasvloot

Een aparte toets naast de energiebalans hierboven: is er op het piekmoment zelf genoeg *beschikbaar vermogen* (GW), niet alleen genoeg energie over het jaar? De gasvloot ligt hierbij niet vast — hij vult endogeen aan wat kern, batterij, interconnectie en de restcapaciteit van wind/zon nog laten liggen tot het vereiste piekvermogen (piekvraag × 1,10 planningsreserve), met een kleine ondergrens van 4 GW voor strategische reserve. Kredietvermogen per bron:

| Bron | Kredietvermogen | Toelichting |
|---|---|---|
| Kern | 92% | Beschikbaarheid na onderhoud/uitval |
| Batterij | ontlaadvermogen / 5u × 85% | Korting voor meerdaagse schaarste |
| Interconnectie | ~11-15% (dynamisch) | 2-groepen correlatiemodel, daalt met eigen wind+zon-uitbouw — zie hieronder |
| Wind/zon | 4% | Kleine restcapaciteit, niet letterlijk nul |

Dit is een vermogens-momentopname, geen volledige probabilistische LOLE/EENS-studie zoals TenneT/ENTSO-E die uitvoeren.

**Batterij-GWh omhoog draaien beweegt de benodigde gasvloot minder dan je zou verwachten — dat is geen bug.** Voor deze toets telt niet de energie-inhoud van de batterij (GWh), maar het vermogen dat hij gedurende de aangenomen ontlaadduur van 5 uur kan leveren (× 85% korting voor meerdaagse schaarste). 15 GWh extra batterij levert dus maar (15/5) × 0,85 ≈ 2,6 GW extra kredietvermogen op — een sprong van 75% in GWh wordt maar een paar GW in vermogen. Het vereiste vermogen zelf verandert hierdoor nooit (gas vult per definitie exact aan wat ontbreekt); wat wél beweegt is de omvang van de gasvloot en de bijbehorende capaciteitsmechanisme-kost.

### Interconnectie-correlatiemodel (Malvaldi et al.)

Een vlakke de-ratingaanname voor interconnectie doet geen recht aan twee dingen. Ten eerste: NL-interconnectie is niet één ding. TenneT zelf: de vier landverbindingen met Duitsland en twee met België wisselen samen "bijna 12 GW" uit. Met de onderzeese kabels naar het VK (BritNed, 1,0 GW) en Denemarken (COBRAcable, 0,7 GW) erbij loopt ~13,7 GW naar landen die tijdens een Nederlandse dark doldrum vaak zélf ook nauwelijks wind hebben (Malvaldi et al. 2017: windcorrelatie tussen naburige NW-Europese landen is sterk en neemt pas geleidelijk af met afstand). Alleen NorNed (0,7 GW, Noorwegen) draait op een ander opslagmedium: waterkracht — nog geen 5% van de totale ~14,4 GW interconnectiecapaciteit.

| Groep | Aandeel | Basiskrediet | Toelichting |
|---|---|---|---|
| Gecorreleerde buren (DE/BE/DK/VK) | 95% | 15%, dalend | Vaak zelf ook schaars; krediet daalt verder naarmate eigen wind+zon-uitbouw toeneemt (proxy voor regionaal decarbonisatietempo) |
| Noorse waterkracht (NorNed) | 5% | 45% | Windonafhankelijk, maar gekort van het "solo"-krediet (~70%) omdat Duitsland, VK en Denemarken tijdens eenzelfde Europabrede schaarste op dezelfde Noorse capaciteit trekken — die kan maar één keer geleverd worden, én een klein aandeel van het totaal |

Blended krediet: ~17% bij lage regionale VRE-uitbouw tot ~11% bij volle uitbouw, ~11-15% over het bereik van de wind/zon-sliders in de praktijk — dynamisch, meebewegend met de wind/zon-sliders, in plaats van één vast getal. Lager dan een eerdere versie van dit model aannam, omdat Noorwegen — de enige echt windonafhankelijke koppeling — maar een klein deel van de totale NL-interconnectiecapaciteit vormt.

**Eén gedeelde functie, twee toepassingen.** Ditzelfde correlatiekrediet (`interconnCorrelationCredit()`) bepaalt ook hoeveel import wordt meegeteld in de dark-doldrums-uren-verdeling. Eerder waren dat twee losstaande aannames — een platte 50%-korting (effectief 25% na een dubbele toepassing) in de energiebalans, dit correlatiemodel (~11-15%) in de adequacy check — wat betekende dat de twee panelen impliciet een verschillend beeld gaven van hoeveel import je tijdens schaarste kunt vertrouwen. Nu gebruiken beide dezelfde onderliggende functie, getest op consistentie in `tests.js`.

### Capaciteitsmechanisme

Bij hoge VRE-penetratie draait de gasvloot te weinig uren om zichzelf via de energiemarkt terug te verdienen — het "missing money"-probleem. De (endogeen bepaalde, de-rated) vloot uit de adequacy check wordt daarom apart geprijsd via €45.000/MW/jaar (werkaanname; ter oriëntatie clearde de GB-capaciteitsmarkt T-4 recent op orde van grootte £27-65/kW/jaar voor bestaand/gerefurbished vermogen), omgeslagen over alle geleverde TWh. Omdat de vlootomvang endogeen is, verandert deze kostenpost mee met de sliders: meer kern/batterij/interconnectie → kleinere, goedkopere gasvloot.

### Het omslagpunt

Eén van de grafieken toont waar de **effectieve LCOE van kernenergie** de **geschatte systeemwaarde van firm capacity** overstijgt (energiewaarde plus een marginale capaciteitswaarde, afgeleid uit dezelfde adequacy-engine als hierboven). Dit is een beschrijving, geen oordeel: of een investering voorbij dat punt "gewenst" is, hangt af van afwegingen die dit model niet meeneemt (leveringszekerheid, strategische autonomie, industriebeleid). Zie ook "Twee kern-bouwrealiteiten" hieronder — dit omslagpunt ligt bij de huidige westerse first-of-a-kind-aanname (€160/MWh) al bij de laagste geteste penetratie, en pas bij een seriebouw-aanname (€70/MWh) rond 70-71% wind+zon-penetratie.

---

## Parameters en aannames

### Technologiekosten

| Technologie | Kosten | Toelichting |
|---|---|---|
| Wind offshore (nieuwbouw) | €117/MWh | NL kabinetsbrief 2025 (strike price SDE++) |
| Wind onshore (basis) | €85/MWh | Vaste 7 GW bestaand, grotendeels afgeschreven |
| Zon | €45/MWh | Huidige tenderprijzen utility-scale |
| Kernenergie — westerse FOAK | €160/MWh | Hinkley Point C-achtig: eerste bouw in decennia, kostenoverschrijdingen |
| Kernenergie — seriebouw | €70/MWh | OECD (2020) ~$66/MWh voor niet-westerse series (7% discontovoet); Zuid-Korea/VAE-achtig |
| Gas CCGT (variabel) | €77/MWh | Brandstof, CO₂, opex — capaciteit apart via capaciteitsmechanisme |
| Gas+CCS (variabel) | €135/MWh | Hogere capex CO₂-afvang/opslag/transport; afvangrate 90%; capaciteit apart |
| Batterijen + V2G | €10/MWh cycluskost | ~200 cycli/jaar; send-out 4-6 uur; incl. bidirectioneel laden EVs. Toegepast op de daadwerkelijk geladen energie, zichtbaar als aparte regel "Batterij (cycluskost)" in de kostenopbouw |

### Twee kern-bouwrealiteiten, geen bandbreedte

Het verschil tussen €160 en €70/MWh is geen onzekerheidsmarge rond één schatting — een bandbreedte ertussen (bijv. €130) zou de facto nog steeds bij het €160-niveau uitkomen qua uitkomst. Het zijn twee aantoonbaar verschillende bouwrealiteiten: westerse first-of-a-kind-projecten (Hinkley Point C, Vogtle, Flamanville — eerste bouw in decennia, kostenoverschrijdingen) versus Zuid-Koreaans/Emirati seriebouw met een ingespeelde toeleveringsketen (Barakah: eenheid 4 kostte ~40% van eenheid 1). Een eerste Nederlands programma van 1-2 centrales na decennia zonder nieuwbouw heeft die leercurve niet — het seriebouw-cijfer laat zien wat een langjarig, herhaald bouwprogramma *zou kunnen* opleveren, niet wat 1-2 centrales op zichzelf bereiken. De toggle in de tool bepaalt welke aanname overal wordt gebruikt (kostenopbouw, KPI's, omslagpuntgrafiek).

### Kannibaliseringsopslag (effectieve LCOE)

Standalone kosten missen het centrale probleem: naarmate penetratie stijgt, dalen marktprijzen precies op de uren dat een technologie produceert. Dit geldt voor élke technologie die hierboven staat, niet voor één in het bijzonder.

| Technologie | Opslag: Gebalanceerd-scenario / max. binnen sliderbereik | Reden |
|---|---|---|
| Wind offshore | +15% / +27% | Gecorreleerde productie; hogere WACC bij lage verwachte marktprijzen |
| Zon | +20% / +33% | Sterke dagcorrelatie; zomermiddag-concentratie |
| Kern | +20% / +53% | Lange investeringshorizon + baseload-inflexibiliteit; interconnectie helpt minder |

*Geteste waarden binnen het bereik van de sliders, niet de theoretische asymptoot van de onderliggende schaalparameters — die ligt hoger maar wordt in de praktijk (door batterij-, gas- en interconnectie-absorptie) nooit bereikt.*

**Interconnectie dempt dit niet gelijk voor wind en zon.** Stiewe, Xu, Eicke & Hirth (2025, *Energy Economics*) schatten in een panelanalyse van 30 Europese biedzones (2015-2023) dat interconnectie de eigen kannibalisering van wind sterker dempt dan het de prijsdruk van gecorreleerde buurlanden-opwek verergert — een reëel netto-voordeel ("moderate gains... only for wind generators"). Voor zon vallen die twee effecten vrijwel exact tegen elkaar weg ("these two effects almost exactly cancel each other out"). Het model past interconnectie-demping daarom voor wind vrijwel volledig toe, voor zon slechts voor een klein residu (10%).

**Curtailment op 0% en toch een opslag hierboven is geen tegenstrijdigheid.** Curtailment meet wat er ná batterijlading en export nog fysiek wordt weggegooid. Kannibalisering meet hoe vaak en hoe hard de marktprijs instort door overaanbod, ongeacht wat er met die energie gebeurt. Een batterij die al het overschot volledig absorbeert, verplaatst de energie naar een later, duurder moment — maar de lage (soms nul-)prijs tijdens het surplus-uur heeft wel degelijk gegolden, en drukt zo de gemiddelde opbrengst van alles wat in dat uur draaide. Curtailment op 0% betekent dus "niets weggegooid", niet "geen prijsdruk gehad".

### Load duration curve — 4 marktsegmenten

De segmenten zijn benoemd naar marktconditie (schaarste of overschot), niet naar tijdstip — namen als "dal zomermiddag" suggereren een kort, zeldzaam venster terwijl het in werkelijkheid om duizenden uren per jaar gaat.

| Segment | Uren/jaar | Marktconditie | Dominante bron |
|---|---|---|---|
| **Schaarste-uren** | ~500 | Weinig wind/zon, hoge vraag — *dark doldrums* | Gas(+CCS), kern, import |
| **Overschot-uren (matig)** | ~2.000 | Redelijk wind/zon, gemiddelde vraag — surplus mogelijk | Wind+zon, export, batterijlading |
| **Krapte-uren (regulier)** | ~3.000 | Weinig zon, wisselend wind — structureel tekort | Wind, gas, batterij ontlading |
| **Overschot-uren (hoog)** | ~3.260 | Veel wind/zon, lage vraag | Curtailment/export, batterijlading |

Curtailment ontstaat in de overschot-uren (matig én hoog) én op winderige nachten binnen de krapte-uren. Export is beperkt omdat buurlanden op dezelfde uren hetzelfde surplus hebben (Europese correlatie).

### Niet-fossiel aandeel van de jaarvraag

Onder de LDC-grafiek in de tool staat het percentage van de jaarvraag dat wordt gedekt door wind + zon + kern + batterij. Geen dubbeltelling: de batterij slaat alleen wind/zon/kern-elektronen op en verschuift die in tijd — de brutoproductie wordt eerst gecorrigeerd voor wat wordt weggegooid (curtailment) of geëxporteerd, vóórdat het als "dekt de vraag" wordt geteld. Import telt niet mee (herkomst onbekend/gemengd), en Gas(+CCS) evenmin. Rekensom: `(totalVRETWh − curtailment − export) / vraag`. Getest op sluitende optelling (niet-fossiel + gas + import ≈ 100% van de vraag) in `tests.js`.

**Een tweede getal ernaast: klimaatneutraal aandeel.** "Niet-fossiel" is met opzet streng gedefinieerd, en juist daardoor lastig voorbij de 70-75% te krijgen binnen realistische scenario's — dat weerspiegelt een reëel probleem (de ~3.500 uur/jaar schaarste/krapte waar marginale extra wind/zon weinig aan doet), geen modelfout. Het officiële Nederlandse beleidsdoel is bovendien geen "90-100% niet-fossiel in 2040": het Klimaatakkoord noemt 70% *hernieuwbaar* (excl. kern) in 2030, en 2040/2050 is geformuleerd als "klimaatneutraal energiesysteem", wat kernenergie én gas met CCS (afgevangen CO₂ telt niet als uitstoot) expliciet toestaat. Zelfs het 70%-doel voor 2030 is in de laatste KEV-raming (PBL) al bijgesteld van 72% naar 60%, vooral door vertraging bij wind op zee. Het "klimaatneutraal aandeel" telt daarom ook het afgevangen deel van Gas+CCS mee (90% capture rate): `niet-fossiel + gasCcsTWh × 0,90`, gedeeld door de vraag — een bredere maatstaf die dichter bij het echte beleidskader ligt.

### Interconnectiekosten (systeemkosten, los van adequacy-krediet)

Interconnectie is geen gratis optie:
- **Infrastructuur**: €1,75 mld/GW (subsea kabels + converterstations), geannualiseerd over 40 jaar
- **Importpremie**: oploopt bij Europabrede windstilte — als Nederland importeert tijdens dark doldrums, zijn Duitsland, België en Denemarken vaak in dezelfde situatie
- **Exportbeperking**: bij hoge VRE-penetratie is de exportwaarde laag — buurlanden hebben op zomermiddagen zelf ook surplus; max ~25-35% van surplus kan worden geëxporteerd

Dit is losstaand van het interconnectie-adequacykrediet hierboven — die twee dienen een ander doel (systeemkosten vs. leveringszekerheid) en zijn apart in het model verwerkt.

### Interconnectieslider — extra bouw, niet totaal

De interconnectieslider stelt niet het totale 2040-vermogen in, maar de **realistische extra bouw** bovenop de vaste basislijn van 15 GW (bestaande kabels, TenneT — zie hierboven). Bestaande verbindingen worden niet afgebroken, en hoogspanningsverbindingen in Nederland komen traag en moeizaam tot stand (netcongestie, ruimtelijke inpassing, vergunningen) — een realistische extra bouw tot 2040 ligt daarom in de orde van 0-10 GW, niet 0-15 GW zoals een eerdere versie van dit model liet zien. Het "Gebalanceerd"-scenario gaat uit van +5 GW extra (20 GW totaal). Scenario's die eerder een totaal ónder de 15 GW van vandaag aannamen ("Kern-zwaar", "NL als eiland") vlakken hierdoor af op de basislijn (15 GW, geen extra bouw) — die twee scenario's verschillen dus niet meer in interconnectie-aanname, wat inhoudelijk correct is: geen van beide vereist nieuwe verbindingen, en geen van beide kan de bestaande capaciteit laten verdwijnen.

### Windslider — extra bouw, niet totaal

Zelfde logica als bij zon en interconnectie: de slider stelt de **extra bouw** van wind offshore tot 2040 in, bovenop de vaste basislijn van 6,4 GW (huidig geïnstalleerd). Bestaande turbines worden niet afgebroken. "Gebalanceerd" gaat uit van +15,6 GW extra (22 GW totaal). Onshore wind is apart en vast op 7 GW (nauwelijks uitbreidbaar door ruimtegebrek) — die telt niet mee in deze slider maar wel in de systeemberekening.

### Zonslider — extra bouw, niet totaal

Zelfde logica als bij interconnectie: de slider stelt de **extra bouw** van zon-PV tot 2040 in, bovenop de vaste basislijn van ~30 GW (CBS: 29,4 GWp geïnstalleerd eind 2025). Bestaande panelen worden niet afgebroken. "Gebalanceerd" gaat uit van +8 GW extra (38 GW totaal). Anders dan bij interconnectie is zonnebouw in Nederland relatief snel gegaan (SolarPower Europe verwacht ~40 GW in 2028) — de bovengrens van de slider (+40 GW, dus 70 GW totaal) is daarom ruimer dan bij interconnectie, maar blijft een aanname, geen voorspelling.

### Elektriciteitsvraag 2040 — en waarom hogere vraag het systeem piekeriger maakt

Extra vraag boven het huidige niveau komt vooral van elektrificatie van warmte (hybride/volledige warmtepompen). Warmtepompvraag piekt bij koud én windstil weer — precies tijdens de schaarste-uren. Het model laat de piek/jaarvraag-verhouding en de intensiteit van de schaarste-uren daarom meeschalen met het gekozen vraagscenario, via lineaire interpolatie — bewust geen apart bedienbaar element, om het model toegankelijk te houden.

| Scenario | TWh/jaar | Piek/jaarvraag-verhouding | Toelichting |
|---|---|---|---|
| Laag | 120 TWh | 0,150 GW/TWh | Huidig verbruiksniveau |
| Midden | 160 TWh | 0,168 GW/TWh | TNO/PBL middenscenario (standaard) |
| Hoog | 200 TWh | 0,185 GW/TWh | Volledig elektrificatiescenario industrie + warmte |

---

## Snelscenario's

| Scenario | Wind offshore (totaal) | Zon (totaal) | Kern | Batterijen | Interconnectie (totaal) | Gas+CCS |
|---|---|---|---|---|---|---|
| Max wind, geen kern | 28 GW (+21,6) | 42 GW (+12) | 0 GW | 25 GWh | 18 GW (+3) | 20% |
| Gebalanceerd (basis) | 22 GW (+15,6) | 38 GW (+8) | 3,2 GW | 20 GWh | 20 GW (+5) | 30% |
| Kern-zwaar (4 EPR's) | 15 GW (+8,6) | 30 GW (+0) | 6,4 GW | 10 GWh | 15 GW (+0) | 50% |
| NL als eiland | 22 GW (+15,6) | 38 GW (+8) | 3,2 GW | 30 GWh | 15 GW (+0) | 60% |
| Batterij-optimum | 25 GW (+18,6) | 42 GW (+12) | 0 GW | 45 GWh | 18 GW (+3) | 20% |

*Wind offshore: vaste basislijn van 6,4 GW (huidig geïnstalleerd) + extra bouw tot 2040. Onshore: vaste 7 GW basis. Kern: 3,2 GW = 2 EPR's (huidig kabinetsplan — locatie nog niet definitief; 1 EPR ≈ 1,6 GW), 6,4 GW = 4 EPR's (verdubbeling). Interconnectie: vaste basislijn van 15 GW (bestaande kabels, TenneT) + realistische extra bouw tot 2040 (0-10 GW instelbaar) — bestaande capaciteit wordt niet afgebroken, dus "Kern-zwaar" en "NL als eiland" vlakken beide af op de basislijn. Zon: zelfde logica, vaste basislijn van ~30 GW (CBS, eind 2025) + extra bouw tot 2040 (0-40 GW instelbaar).*

---

## Beperkingen en disclaimer

Dit is een **beleidsvisualisatie-instrument**, geen vervanging voor volledige systeemstudies. Beperkingen:

- Het model gebruikt 4 marktsegmenten in plaats van een volledig uurresolutiemodel; curtailment wordt daardoor **structureel onderschat** (werkelijk 30-50% hoger dan de modeluitkomst). Dit betekent ook dat de systeemkosten aan de **conservatieve kant** zijn.
- Prijscorrelaties tussen landen zijn gesimplificeerd tot een 2-groepen-model, niet een volledige correlatiematrix
- **Nederland wordt behandeld als één knooppunt ("koperen plaat"), zonder interne transportbeperkingen** — redispatch-kosten voor lokale netcongestie (bijv. Noord- vs. Zuid-Nederland) en de bijbehorende regionale distributienet-investeringen zitten er niet in en komen in werkelijkheid nog bovenop de hier getoonde systeemkosten
- **Geen expliciete verdringingsvolgorde bij overaanbod:** kern draait met een vaste capaciteitsfactor door alle marktsegmenten (ook overaanbod-uren) — de must-run-eigenschap van kern zit dus in de kannibaliseringsopslag en de totale curtailment, maar het model wijst niet toe wélke technologie (kern of wind/zon) in een gegeven uur zou moeten terugschakelen als er een merit-order- of dispatchprioriteit zou gelden
- **WACC is geen aparte variabele:** marktwaardedepreciatie en de hogere financieringskosten (WACC) bij lage verwachte marktprijzen zijn samen verwerkt in één kannibaliseringsopslag per technologie, niet als twee los gemodelleerde effecten
- De benodigde gasvloot heeft een ondergrens van 4 GW (strategische reserve) die niet verder onderbouwd is dan een werkaanname
- Het capaciteitsmechanisme-prijsniveau (€45.000/MW/jaar) is een oriënterende werkaanname, geen NL-specifieke schatting
- Kernenergie wordt met twee expliciete bouwrealiteiten gemodelleerd (zie hierboven), niet met een fijnmazige kostencurve
- V2G-adoptie richting 2040 inherent onzeker

Voor beleidsbeslissingen: raadpleeg ENTSO-E TYNDP, ECN/TNO systeemstudies en PBL Klimaat- en Energieverkenning.

---

## Methodologische referenties

- Hirth, L. (2013). *The market value of variable renewables.* Energy Economics.
- Hirth, L. (2015). *The optimal share of variable renewables.* The Energy Journal.
- PBL/TNO (2023). *Klimaat- en Energieverkenning 2023.*
- ENTSO-E (2024). *Ten-Year Network Development Plan.*
- HM Government (2023). *Hinkley Point C — revised cost estimates.*
- OECD/NEA/IEA (2020). *Projected Costs of Generating Electricity.*
- Stiewe, C., Xu, A.L., Eicke, A., Hirth, L. (2025). *Cross-border cannibalization: Spillover effects of wind and solar energy on interconnected European electricity markets.* Energy Economics 143, 108251.
- Malvaldi, A. et al. (2017). *A spatial and temporal correlation analysis of aggregate wind power in an ideally interconnected European power system.* Wind Energy.
- TenneT. *Interconnectoren: stroom zonder grenzen.* tennet.eu.
- CBS. *Zonnestroom; vermogen en vermogensklasse, bedrijven en woningen, regio.* Geraadpleegd 2026.
- Klimaatakkoord. *Elektriciteit.* klimaatakkoord.nl (70% hernieuwbaar-doel 2030).
- PBL. *Klimaat- en Energieverkenning (KEV).* Meest recente raming.
- NL Kabinetsbrief (2025). *SDE++ tenderprijzen windenergie op zee.*

---

## Technische details

Zelfstandig HTML-bestand. Vereist internetverbinding voor D3.js (geladen via CDN). Werkt in elke moderne browser — geen installatie nodig.

```
index.html    ← het model
README.md     ← deze toelichting
```

*Ontwikkeld als communicatie-instrument voor het Nederlandse energiebeleidsdebat, 2025–2026.*
