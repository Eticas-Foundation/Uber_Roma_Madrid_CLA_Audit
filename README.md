# Community-Led Audit: Uber & Roma Neighbourhoods in Madrid

**Eticas Foundation** | Community-Led Audit  
**Platform audited:** Uber (Madrid, Community of Madrid, Spain)  
**Phase:** I (preliminary)  
**Community partners:** Fundación Secretariado Gitano (FSG) · European Roma Rights Centre (ERRC)  
**Funded by:** DiversiFAIr (EU Project)

---

## Overview

This repository contains the datasets, analysis code, and methodology documentation supporting Eticas Foundation's community-led audit of Uber's algorithmic service delivery in Roma neighbourhoods in Madrid. The audit examines whether Uber's ride-hailing algorithms — including driver-rider matching, supply-and-demand prediction, and surge pricing — provide systematically less reliable service to riders originating from Roma settlements compared to riders from more affluent control neighbourhoods.

The audit is a Phase I investigation and a direct extension of Eticas's prior *(Un)Fairness in Mobility* study, which found differential pricing by socioeconomic neighbourhood in Madrid and Málaga. This study focuses specifically on Roma communities, the largest ethnic minority in the EU.

---

## Key Findings

All results are statistically significant (p < 0.05; chi-squared and Welch's t-tests).

### Ride Availability

| Group | Total requests | Unavailable | Unavailability rate |
|---|---|---|---|
| Control | 120 | 0 | **0.0%** |
| Roma | 120 | 32 | **26.7%** |

Uber was unavailable for over 1 in 4 trip requests from Roma neighbourhoods. It was **never** unavailable from control neighbourhoods. The pattern holds across all three destination types and all four time windows (p < 0.05 in all cases).

### Estimated Wait Time (available rides only)

| Group | Rides | Avg EWT | Ratio |
|---|---|---|---|
| Control | 120 | 6.23 min | — |
| Roma | 88 | 8.99 min | **1.44× longer** |

When Uber did offer service to Roma neighbourhoods, riders waited nearly 1.5 times longer than riders from control neighbourhoods. The highest disparity was during morning rush hours (1.67× longer).

---

## Repository Structure

```
.
├── data/
│   ├── neighborhoods.csv              # All 20 neighbourhoods with type and selection notes
│   ├── experiment-design.csv          # Full data collection protocol parameters
│   ├── ride-availability-results.csv  # Availability outcomes (aggregate, by destination, by time)
│   ├── ewt-results.csv                # EWT outcomes (aggregate, by destination, by time)
│   ├── route-example-chinchon.csv     # Illustrative route selection example (Chinchón)
│   └── README.md                      # Provenance, field definitions, external data sources
│
├── analysis/
│   └── audit_analysis.ipynb          # Reproducible Python notebook (4 figures, full stats)
│
└── README.md
```

---

## Neighbourhoods

**10 Roma settlements** (Community of Madrid, identified with FSG input):
Camino Camarma · Los Salobrales · Chinchón · Estremera · Humanes · Cañada Real · Las Sabinas · Cañada Real–Rivas-Vaciamadrid · Torrejón de la Calzada · Fuente el Saz de Jarama

**10 Control neighbourhoods:**
7 socioeconomically well-off municipalities near Roma settlements (Cobeña, Ajalvir, Villaviciosa de Odón, Getafe, Pinto, Coslada, Pozuelo de Alarcón) + 3 inner-city neighbourhoods from the prior study (Barajas, Fuencarral-El Pardo, Vicalvaro)

---

## Methodology Summary

- **60 routes** (20 neighbourhoods × 3 destination types: city centre, nearest commercial centre, nearest hospital)
- **240 trip requests** (60 routes × 4 time windows: two rush and two off-peak)
- Requests submitted via sock puppet accounts; **no actual trips were booked**
- Metrics: ride availability (binary) and estimated wait time (minutes)
- Tests: chi-squared (availability) and Welch's t-test (EWT)
- Destination selection: OpenStreetMap + K-Means clustering + Google Maps Routes API
- Income data: INE Household Income Distribution Map (2022)

Full methodology is documented in `data/README.md` and the analysis notebook.

---

## Running the Analysis

Requires Python 3.9+ and:

```bash
pip install pandas numpy matplotlib scipy jupyter
```

Run:

```bash
jupyter notebook analysis/audit_analysis.ipynb
```

The notebook reproduces all chi-squared and Welch's t-tests from the audit report, and generates 4 figures.

---

## Important Notes

- This is a **Phase I** audit. Results are preliminary and describe correlation, not causation. Phase II will control for additional socio-demographic factors.
- The **raw trip-level dataset** is not publicly distributed — see `data/README.md` for rationale and contact information.
- The audit report notes that code and datasets are available on this GitHub. This repository fulfils that commitment.

---

## Team

**Research Lead:** Dr. Gemma Galdon-Clavell, Founder of Eticas Foundation  
**Contributing Researchers:** Yung-Hsuan Wu (Project Manager & AI Auditing Specialist) · Luis Rodrigo González Vizuet (Ethics & Technology Researcher) · Shiran Dudy (AI Auditing Researcher) · Rubén González Sendino (Lead Data Scientist)

---

## License

Analysis code and datasets in this repository are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribution required: *Eticas Foundation, "Community-Led Audit: Roma and Ride-Hailing Platforms," 2025.*

Funded by the European Union (DiversiFAIr project). Views expressed are those of the authors and do not represent the European Union or EACEA.
