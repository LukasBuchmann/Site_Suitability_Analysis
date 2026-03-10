# Site Suitability Analysis for Wind Energy in Canton Thurgau

![QGIS](https://img.shields.io/badge/QGIS-3.40.12-green?logo=qgis)
![Spatial Analysis](https://img.shields.io/badge/Analysis-Raster%20MCA-blue)
![ZHAW](https://img.shields.io/badge/Institution-ZHAW-red)

## Project Overview
[cite_start]This project identifies suitable locations for wind turbine development in Canton Thurgau (Switzerland) by balancing economic, legal, and social requirements[cite: 40]. [cite_start]The analysis was conducted as part of the GISScience and Geodatabases module at the Zurich University of Applied Sciences (ZHAW)[cite: 1, 6]. 

[cite_start]Due to complex topography, high population density, and landscape protection laws, finding suitable sites for wind energy on the Swiss Plateau is highly challenging[cite: 34, 36]. [cite_start]This project tackles this issue by utilizing a **Geographic Information System (GIS)-based Multi-Criteria Analysis (MCA)** within QGIS[cite: 41, 49].

---

## Methodology

[cite_start]The analysis employs a **Hybrid MCA Approach**, which distinguishes between strict Binary Constraints (Exclusion Zones scored 0 or 1) and Weighted Suitability Factors (scored 1-10)[cite: 67].

### 1. Exclusion Criteria (Constraints)
[cite_start]Areas legally or technically unsuitable were assigned a value of 0[cite: 104]:
* [cite_start]**Settlements:** Conservative 300m noise protection buffer[cite: 105, 107].
* [cite_start]**Protected Areas:** Federal Inventory of Landscapes and Natural Monuments (BLN)[cite: 108].
* [cite_start]**Topography:** Slopes > 20% (technically unfeasible for cranes/construction)[cite: 109, 110].
* [cite_start]**Infrastructure:** 50m safety buffer around roads[cite: 111].

### 2. Weighted Suitability Factors
[cite_start]The remaining areas were scored from 1 (Low) to 10 (High)[cite: 117]:
* [cite_start]**Wind Speed (60% Weight):** Derived from the Swiss Wind Atlas at 100m height[cite: 58, 118].
* [cite_start]**Slope Suitability (30% Weight):** Flatter terrain ($0-5^{\circ}$) received the highest scores to minimize civil engineering costs[cite: 127, 128].
* [cite_start]**Road Proximity (10% Weight):** Areas within 50-500m of existing roads scored highest to minimize access construction costs[cite: 129, 130].

### Map Algebra Model
[cite_start]The final suitability map was generated using the following raster calculation[cite: 132]:
[cite_start]`Final Score = (0.6 * Wind + 0.3 * Slope + 0.1 * Roads) * Constraints` [cite: 134]

*(Insert your Map Algebra / Flowchart image here: `![Process Flowchart](images/flowchart.png)`)*

---

## Key Results

* [cite_start]**Suitable Area:** A total of 2,231 hectares ($22.3~km^{2}$) were identified as suitable for development (Score ≥ 4.4), representing approximately 2.3% of the canton's total surface area[cite: 188].
* [cite_start]**Maximum Potential:** The maximum score observed was 7.0 (out of 10)[cite: 190]. [cite_start]No sites achieved an "Excellent" suitability (Score > 8)[cite: 189].
* [cite_start]**Conclusion:** The model confirms that Thurgau is a "low-wind" region[cite: 198]. [cite_start]Economic viability will heavily depend on maximizing infrastructure access and utilizing modern "weak-wind" turbines[cite: 198]. [cite_start]The model successfully identified specific, technically feasible positions that align with the official Wind Energy Areas designated in the Cantonal Structure Plan[cite: 207, 247].

*(Insert screenshots of your final maps here: `![Suitability Map](images/map_thurgau.png)`)*

---

## Data Sources & Reproducibility

[cite_start]To ensure high spatial accuracy, official open geodata from Swiss federal authorities were used[cite: 55]. [cite_start]All datasets were processed in the Swiss coordinate system CH1903+/LV95 (EPSG: 2056)[cite: 56]. 

**Note on Data Storage:** To maintain a lightweight repository and adhere to best practices, the raw spatial datasets (Raster and Vector files) are *not* included in this GitHub repository. [cite_start]The analysis can be fully reproduced by acquiring the following public datasets[cite: 58]:

| Dataset | Source | Description |
|---------|--------|-------------|
| **Wind Atlas of Switzerland** (100m) | Swiss Federal Office of Energy (BFE) | Mean annual wind speed |
| **DHM25** (Digital Elevation Model) | Swisstopo | Elevation & Slope derivation |
| **swissTLM3D** | Swisstopo | Roads and Settlements vectors |
| **BLN Inventory** | Federal Office for the Environment (FOEN) | Protected Areas (Strict exclusion) |

📄 **Full Project Report:** For a detailed breakdown of the methodology, statistical analysis, and discussion of limitations, please refer to the complete [Project Report PDF](docs/Buchmann_Lukas_Project_Report_GISScience_GDB.pdf) included in the `docs/` folder.
