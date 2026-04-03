# Data

## Overview

This directory contains four datasets reconstructed from the audit report tables. The underlying raw trip request logs (ride availability and EWT per individual request) are held separately — see the note on raw data below.

---

## neighborhoods.csv

All 20 neighborhoods included in the experiment: 10 Roma settlements and 10 control neighborhoods in the Community of Madrid.

| Field | Description |
|---|---|
| `neighborhood_id` | Unique ID (R01–R10 for Roma; C01–C10 for control) |
| `group` | `Roma` or `Control` |
| `type` | `settlement`, `municipality`, or `inner-city neighborhood` |
| `name` | Settlement or neighborhood name |
| `municipality` | Administrative area |
| `notes` | Selection rationale |

**Roma settlements** (n=10): Camino Camarma, Los Salobrales, Chinchón, Estremera, Humanes, Cañada Real, Las Sabinas, Cañada Real–Rivas-Vaciamadrid, Torrejón de la Calzada, Fuente el Saz de Jarama — identified with input from Fundación Secretariado Gitano.

**Control municipalities** (n=7): Cobeña, Ajalvir, Villaviciosa de Odón, Getafe, Pinto, Coslada, Pozuelo de Alarcón — selected for proximity to Roma settlements and above-median household income (INE 2022 data).

**Control inner-city neighborhoods** (n=3): Barajas, Fuencarral-El Pardo, Vicalvaro — inherited from Eticas's prior *(Un)Fairness in Mobility* study.

---

## experiment-design.csv

Full data collection protocol parameters: 240 total trip requests across 60 routes, 4 time windows, methodology for destination selection (OSM + K-Means clustering), and statistical tests used.

---

## ride-availability-results.csv

Ride availability outcomes disaggregated three ways: aggregate, by destination type, and by time of day. Test statistic: chi-squared test of association.

| Field | Description |
|---|---|
| `disaggregation` | Level of disaggregation: `aggregate`, `destination`, `time_of_day` |
| `category` | Specific category (e.g. `city_center`, `08:00-09:00`) |
| `group` | `Control` or `Roma` |
| `total_routes` | Total routes in this stratum |
| `available_rides` | Number of requests that received an EWT |
| `unavailable_rides` | Number of requests that received "not available" |
| `pct_unavailable` | Proportion of unavailable requests (0–1) |
| `p_value` | Chi-squared test p-value for the Roma/control comparison |
| `significant` | Whether p < 0.05 |

---

## ewt-results.csv

Estimated wait time (EWT) outcomes for available rides, disaggregated three ways: aggregate, by destination type, and by time of day. Test statistic: Welch's t-test.

| Field | Description |
|---|---|
| `disaggregation` | Level of disaggregation |
| `category` | Specific category |
| `group` | `Control` or `Roma` |
| `counted_routes` | Number of requests with an EWT (available rides only) |
| `sum_ewt_min` | Sum of EWT across all available requests (minutes) |
| `avg_ewt_min` | Mean EWT (minutes) |
| `roma_control_ratio` | Roma avg EWT ÷ control avg EWT (Roma rows only) |
| `p_value` | Welch's t-test p-value |
| `significant` | Whether p < 0.05 |

---

## route-example-chinchon.csv

An illustrative example showing the three destination types selected for the Roma settlement Chinchón, as reported in Table 2 of the audit report.

---

## Raw Data

The raw trip-level dataset (one row per trip request, with neighborhood, destination, time window, availability result, and EWT) is **not included** in this public repository. Reasons:

- Trip requests were submitted via sock puppet accounts. Publishing raw logs may reveal operational details of the data collection methodology that could be exploited to circumvent future audits of this kind.
- The audit report notes that "All code scripts and datasets are available on Eticas Foundation's GitHub" — this repository fulfils that commitment at the aggregate level. Contact Eticas Foundation for access to raw data for research replication purposes.

---

## External Data Sources Used

| Source | Purpose | URL |
|---|---|---|
| INE Household Income Distribution Map (2022) | Classifying municipalities by income | https://www.ine.es/dyngs/INEbase/en/operacion.htm?c=Estadistica_C&cid=1254736177088&idp=1254735976608 |
| OpenStreetMap | Commercial area and hospital geolocation | https://www.openstreetmap.org/ |
| Google Maps Routes API | Car travel time and distance per route | https://developers.google.com/maps/documentation/routes |
| Fundación Secretariado Gitano (2023) | Roma settlement identification and poverty data | https://www.gitanos.org/resources/research/study_of_the_characteristics_and_circumstances_of_people_living_in_slum_and_substandard_housing_settlements_in_spain/ |
