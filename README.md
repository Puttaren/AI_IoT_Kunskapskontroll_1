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
![Energiflöden per timme 2024-04-25](Diverse%20filer/demo_floden_2024-04-25.png')
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