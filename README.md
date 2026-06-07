# Tel Aviv Light Rail Connectivity Analysis

## Project Overview

This project analyzes the connectivity between Tel Aviv's existing light rail network and Israel's intercity train stations, using geospatial data from Israel's Ministry of Transport.

The research question guiding this analysis:

> **"How well does the current Tel Aviv light rail network connect residents to intercity train stations, and which stations leave riders most underserved?"**

This question was born from a personal frustration: Living near the Red Line but still facing a long walk to reach HaShalom station for intercity travel to Jerusalem. The goal was to determine whether this is an isolated experience or a systemic issue across the network.

---

## Data Sources

- **Light Rail Stations:** [Israel Ministry of Transport - LRT Stations (Existing & Planned)](https://data.gov.il/datasets/ministry_of_transport/lrt_stat)
  - Existing and planned light rail stations across Israel
  - Coordinates in ITM (Israeli Transverse Mercator) format - converted to WGS84 (standard lat/long) for analysis

- **Transit Stations Reference File:** [Israel Ministry of Transport — Bus, LRT & Rail Stations](https://data.gov.il/datasets/ministry_of_transport/bus_stops)
  - Spatial reference file containing bus stops, light rail, and Israel Railways stations
  - Coordinates already in WGS84 format
  - Used to extract intercity Israel Railways stations in the Tel Aviv metro area

---

## Geospatial Methodology

A key challenge in this project was working with two datasets that used **different coordinate systems**:

- The light rail station dataset used **ITM (EPSG:2039)**, Israel's national coordinate system
- The intercity train station dataset used **WGS84 (EPSG:4326)**, the standard latitude/longitude system used globally

To verify station locations and confirm data accuracy, coordinates were **reverse geocoded** using the `geopy` library — converting raw coordinate pairs into real-world addresses. This allowed cross-referencing against known station names (e.g., confirming that coordinates `32.073348, 34.793203` corresponded to HaShalom station by pasting them into Google Maps).

After verifying the data, ITM coordinates were converted to WGS84 using the `pyproj` library, enabling consistent distance calculations across both datasets using the **geodesic distance** formula.

---

## Tools Used

- Python, pandas, matplotlib — data loading, cleaning, and visualization
- `pyproj` - coordinate system conversion (ITM → WGS84)
- `geopy` — reverse geocoding for station verification and distance calculation
- Jupyter Notebook

---

## Key Finding

**Intercity rail connectivity is unequal across Tel Aviv's Red Line.**

Only 3 out of 10 existing light rail stations are within a 10-minute walk (800 meters) of an intercity train station. The northern end of the Red Line is particularly disconnected — Gesher Em HaMoshavot sits nearly 4 kilometers from the nearest intercity station, a roughly 50-minute walk.

| Light Rail Station | Distance to Nearest Intercity Station |
|---|---|
| Arlozorov | 279 m ✓ |
| Shaul HaMelech | 452 m ✓ |
| Yehudit | 568 m ✓ |
| Aba Hillel | 522 m ⚠ |
| Karlibach | 1,249 m x |
| Allenby | 1,353 m x |
| Bialik | 1,504 m x |
| Ben Gurion | 2,340 m x |
| Aharonovitch | 3,460 m x |
| Gesher Em HaMoshavot | 3,968 m x |

✓ Within 10-minute walk | ⚠ Borderline | x Significant gap

---

## Business / Planning Implication

These findings reinforce the urgency of Tel Aviv's planned light rail expansion. The current network leaves large portions of the city with poor intercity connectivity - a gap that disproportionately affects residents in northern Tel Aviv neighborhoods who must travel long distances just to access intercity rail.

---

## Project Structure

```
israel-transit-analysis/
│
├── README.md                        ← You are here
└── analysis.ipynb                   ← Full Jupyter Notebook with code and findings
```

---

## About

This project was built as part of a data analytics portfolio to demonstrate skills in geospatial data analysis, coordinate system conversion, distance calculations, and business-oriented storytelling with real-world public transit data.

## Tools Used
Python · Pandas · Matplotlib · Seaborn · Jupyter Notebook

## Author
Sadie Greenberg | [LinkedIn](https://www.linkedin.com/in/sgbrg) | 
[Email](mailto:sadieagberg@gmail.com)
