# AI & IoT: Kunskapskontroll 1
### AV: MICHAEL BROSTRÖM

Här finns en komplett inlämning för Kunskapskontroll 1 i kursen AI & IoT. 

## 📂 Innehållsförteckning

Projektet är strukturerat i fem huvuddelar:

### 1. Del 1: Teorifrågorna
* **Fil:** `Del 1 - Teori.ipynb`

### 2. Del 2: Molnbaserad Bildanalys – Amazon Rekognition
* **Fil:** `Del 2 - Amazon Rekognition.ipynb`
* Teknisk implementering av bilddetektering via Amazons molntjänst.
    * **Data Sourcing:** Automatiserad hämtning av bildmaterial från egen webbsida till AWS S3.
    * **API-analys:** Användning av Amazon Rekognition för identifiering av objekt och miljöer.
    * **Redovisning:** Cirkeldiagram samt ett antal exempelbilder med AI-identifierade labels.

### 3. Del 3: Energioptimering & Investeringsanalys
![Energiflöden per timme 2024-04-25](Diverse%20filer/demo_floden_2024-04-25.png)
* **Fil:** `Del 3 - Elprojekt.ipynb`
* **Innehåll:** Projektets tekniska tyngdpunkt. En prediktiv modell för AI-styrning av ett smart hem i elområde SE4.
    * **Data:** Integration av Solis Cloud API (IoT), SMHI SNOW1G (Väderprognos) och NASA POWER (Historisk strålning).
    * **ML-modell:** Prediktion av solproduktion via en `HistGradientBoostingRegressor`.
    * **Optimering:** Linjärprogrammering med biblioteket `PuLP` för schemaläggning av laster (EV, vitvaror) och batteristyrning.

### 4. Självutvärdering
* **Fil:** `Självutvärdering.ipynb`
* **Innehåll:** Sammanfattning av uppgiften och en motivering till varför jag förtjänar VG.

### 5. Projektpresentation
* **Fil:** `Presentation.html`
* **Innehåll:** Visualisering i korthet av del 3, skapad i HTML med Tailwind CSS. Diagram, KPI:er, slutsatser och kommentarer. Öppnas i valfri webbläsare.

## 🛠 Teknisk Stack
* **Språk:** Python (Pandas, Scikit-learn, PuLP, Requests, Matplotlib).
* **Molntjänster:** Amazon Web Services (S3, Rekognition, IAM).
* **API:er:** Solis Cloud, SMHI Open Data (SNOW1G), NASA POWER API, Nord Pool.
* **API-nycklar:** Dessa hanteras via .env som av naturliga skäl inte finns uppladdad på github.

## 📁 Arkiv & Övrigt
* `/Datainsamling`: (Lokal mapp - ej på github) Innehåller rådata-filer och master-datasets (CSV) som ligger till grund för analysen i Del 3.
* `/Diverse filer`: Samlingsplats för diverse filer som använts under resans gång.

## 💡 Viktigaste insikterna från del 3 
Paradoxalt nog kan ökad digital intelligens (AI-styrning) minska det ekonomiska incitamentet såväl för dyra investeringar i hushållsbatterier som faktiskt även AI-styrningen i sig. Genom prediktiv *Load Shifting* kan en betydande del av den gröna omställningen genomföras med mjukvara, vilket kan göra energiomställningen mer tillgänglig för alla, även de som saknar större resurser.

## 💡 Nästa steg: App som stöd för att styra elförbrukningen
Projektets naturliga nästa steg är att lyfta den prediktiva modellen från en experimentell miljö till en helautomatiserad produktionstjänst. Genom att implementera en molnbaserad arkitektur kan analysen transformeras till ett aktivt värdeskapande verktyg som dagligen analyserar morgondagens day ahead-priser och väderprognoser i syfte att skapa en matematiskt optimal körplan för hushållets elförbrukning.

Min idé var en app som dels mailar rekommendationer dagligen och dels skickar notiser i mobilen en timme innan det växlar från "rött" till "grönt" och tvärtom så att jag får en bra påminnelse om jag t.ex. vill ladda bilen dagtid eller göra extra varmvatten. 

Tyvärr fanns inte tiden till att färdigställa denna app innan inlämningen av den här uppgiften, men jag ska göra den ändå - för mitt eget höga nöjes skull och för att det nog kan spara en och annan krona. 

## 🛠 Teknisk fördjupning: Metodik & Modellering

Här följer en detaljerad genomgång av projektets databehandling, val av algoritm och optimeringslogik.

### 📦 Data, Datakällor & Feature Engineering

Modellen vilar på en databas bestående av 21 961 rader med timvis energidata (2023-07-01 till 2025-12-31).

**Datakällor:**

| Källa | Beskrivning |
|---|---|
| `masterenergydatacleaned.csv` | Huvudfil med historisk förbrukning och produktion |
| **SMHI STRNG** (`strang1g`) | API för timvis global solinstrålning (W/m²) |
| **SMHI metobs** | Timvis lufttemperatur från Halmstad Flygplats (station 62410) |
| **NASA ALLSKY_KT** | Klarhetsindex (0–1) från NASA POWER-databasen. Förbättrade modellens precision |
| **SMHI snow1g** | SMHIs 10-dygns timprognos (*Swedish National Operational Weather*, uppdateras var 15:e minut) |

**Feature Engineering:**

- **Lag-features** – Inkluderar historisk produktion (t-1 dag/vecka) för att ge modellen kontext kring trender. Alltid beräknade med `.shift(1)` eller mer för att undvika *data leakage*.
- **Rolling mean** – 7 och 14 dagars glidande medelvärde för produktion och instrålning. Fångar trenden utan att bli känslig för enstaka outliers.
- **Cirkulär kodning** – `sin/cos`-transformationer för timmar (`hoursin`/`hourcos`), veckodagar och säsonger (`seasonsin`/`seasoncos`), för att bevara tidens cykliska natur (t.ex. att timme 23 gränsar till timme 0).
- **Solvinkel** (`solarangle`) – Beräknad via $\sin(\pi \cdot (hour-6)/14)$, klippt till 0 på natten. Approximerar solens position och peakar vid 13:00. Modellen tränas *enbart* på timmar med dagsljus för att minimera brus.

---

### 🤖 AI-Modellen: HistGradientBoostingRegressor

Valet föll på **HistGradientBoostingRegressor** från Scikit-learn (som jag ju redan var bekant med). Denna används i **två steg**:

1. **Daglig prognos** – Features på dagsnivå, predikterar nästa dags totala solproduktion (kWh).
2. **Timvis prognos** – Features på timnivå, predikterar produktion per timme med logaritmisk transformation av target (`log1p`).

- **Varför denna modell?** Den hanterar saknade värden (`NaN`) internt, kräver ingen normalisering av features och är robust mot outliers. Som en *ensemble*-modell korrigerar varje nytt träd felen från det föregående. Snabbare än XGBoost och har inbyggd early stopping. Random Forest saknar boosting-steget och presterar sämre på tidsserier.
- **Logaritmisk transformation** – Target-variabeln (kWh) transformeras via `log1p` för att hantera den högersnedfördelade datan (många nollvärden) och skapa en mer symmetrisk fördelning för loss-funktionen. Konverteras tillbaka med `expm1`.
- **Early stopping** (`n_iter_no_change=50`) – Träningen avbryts automatiskt när valideringsfelet planar ut. Förhindrar *overfitting* utan manuellt val av iterationer. Dagliga modellen stannade vid iteration 186 (av max 1 000).

---

### 📊 Utvärderingsmått (Testdata)

| Mått | Beskrivning | Resultat |
|---|---|---|
| **MAE** | Genomsnittligt absolut fel (kWh). Enklast att tolka. | Timmodell: 0.49 kWh/timme |
| **RMSE** | Kvadratroten ur medelkvadratfelet. Straffar stora avvikelser hårdare. | Timmodell: 0.80 kWh |
| **R²** | Förklaringsgrad (0–1). Hur stor andel av variansen modellen förklarar. | Daglig: 0.62 · Timvis: 0.87 |
| **Permutation Importance** | Viktigaste features mättes genom att permutera varje variabel och mäta MAE-försämringen. | `seasoncos` viktigast, veckodag minst viktig |

---

### ⚡ Optimering & Styrning

Projektet använder två parallella strategier för att maximera ekonomisk nytta:

1. **Load Shifting** – Regelbaserad logik som flyttar hushållslast *från* dyra timmar (hög gridimport) *till* timmar med solöverskott. Max 10 kWh/dygn, 100 % verkningsgrad och noll investeringskostnad.
   > 💡 *"Load Shifting stjäl de mest lönsamma timmarna från batteriet."*
2. **PuLP (Linjär optimering)** – Schemalägger batteri (SOC 1.8–18 kWh), elbil och vitvaror för att minimera nettokostnaden $\text{(import} \times \text{pris} - \text{export} \times \text{pris} \times \text{exportfaktor)}$ över ett 24-timmarsfönster.
   - **Bivillkor** – Exempel: `prob += soltobat[t] <= solar24[t]` (batteri laddas *bara* från sol, ej elnätet). Elbilen laddas endast vid hemmatider (kl 00–07 och 17–24).
   - **EXPORTF = 0.90** – Exportfaktorn innebär att man tillgodoräknas 90 % av spotpriset vid export, p.g.a. nätavgifter.

---

### 🛡 Metodik & Robusthet

- **TimeSeriesSplit** – Korsvalidering anpassad för tidsdata. Data delas strikt kronologiskt (`TRAIN_CUTOFF = 2025-07-01`), vilket ger 710 träningsdagar och 182 testdagar. Förhindrar *data leakage*.
- **Data leakage** – Om modellen "ser framåt i tiden" under träning får den artificiellt bra resultat men misslyckas i produktion. Lag-features är alltid beräknade med `.shift(1)` eller mer.
- **Day-ahead-priser (SE4)** – Elpriser för Sydsverige publiceras kl 13:00 för nästa dag. Systemet är designat för att köras antingen efter 14:00 (med prisdata) eller före (med förväntad prognos).
- **Fallbacks** – Vid API-bortfall (t.ex. 404-fel eller breaking changes) faller systemet tillbaka på interpolation och historiska medelvärden för att bibehålla driftsäkerhet.
- **Optuna** – Användes under experimentfasen för hyperparameteroptimering av LightGBM. Valdes bort till förmån för HistGradientBoostingRegressor med manuell tuning i den slutliga modellen.
