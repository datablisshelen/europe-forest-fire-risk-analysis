# Capstone Project: European Fire and Threatened Species Risk Analysis

## Environmental Challenge

Fire events are increasing in frequency and intensity across Europe, placing growing pressure on ecosystems, protected habitats, and species of conservation concern. Environmental agencies require clear, evidence-based insight into where fire exposure and ecological vulnerability intersect in order to prioritise monitoring, prevention, and conservation action.

---

## Business Requirement

To develop a data-driven spatial risk framework that identifies regions where fire activity overlaps with threatened biodiversity, highlighting geographic areas where conservation assets may be disproportionately exposed to fire risk.

---

## Intended Audience

European environmental protection and conservation agencies responsible for:

- Fire preparedness and land management  
- Biodiversity protection and monitoring  
- Regional conservation prioritisation and policy planning  

The dashboard and README are designed for non-technical stakeholders, while the supporting notebooks provide full technical transparency.

---

## Project Solution

This project analyses five years of NASA FIRMS satellite fire detections across Europe alongside threatened-species occurrence data from GBIF.

Due to the scale of the datasets involved, a grid-based spatial overlay approach is used to aggregate fire exposure and threatened-species presence into consistent spatial units. Rather than relying on memory-intensive polygon intersections, fire detections and biodiversity occurrences are aggregated to regular latitude–longitude grid cells. This enables efficient identification of fire–biodiversity hotspot regions while retaining sufficient spatial resolution for continental-scale risk analysis.

Unsupervised machine-learning techniques (PCA and KMeans clustering) are applied to group grid cells into distinct fire–threatened-species risk typologies. These typologies are translated into conservation-oriented priority levels, enabling actionable interpretation rather than abstract statistical outputs.

---

## Key Statistical & Data Analysis Methods Used

- Descriptive statistics (counts, averages, distributions)  
- Temporal aggregation (daily → monthly → yearly trends)  
- Spatial analysis (bounding box filtering, grid-based binning)  
- Data quality considerations (satellite confidence levels, detection limits)  
- Grid-based spatial aggregation  
- Unsupervised clustering (PCA + KMeans) for risk typology discovery  
- Static and interactive visualisation (Matplotlib, Seaborn, Plotly, Power BI)

Machine-learning methods are used to support exploratory risk profiling rather than operational fire prediction.

---

## Project Outputs

- A reproducible Python analytics pipeline for data acquisition, cleaning, spatial aggregation, and modelling  
- A grid-level fire–threatened-species risk table identifying hotspot regions  
- A clustering model defining four distinct fire–threatened-species risk typologies  
- An interactive Power BI dashboard presenting:
  - fire exposure patterns  
  - threatened-species hotspot regions  
  - priority geographic zones for conservation attention  
  - species-level listings of the most threatened taxa in highest-priority zones  

---

## Dataset Content

### 1. Fire Detection Data

Fire data is sourced from NASA FIRMS (Fire Information for Resource Management System) using the VIIRS satellite product. The dataset covers five consecutive years of European fire detections, providing consistent spatial and temporal coverage.

Each record represents a satellite-detected fire point.

Key attributes include:

- latitude, longitude — detection coordinates  
- acq_date, acq_time — detection timestamp  
- confidence — detection confidence classification  
- frp — Fire Radiative Power (proxy for fire intensity)  
- daynight — day/night detection flag  

---

### 2. Threatened Species Occurrence Data

Threatened-species occurrence records are retrieved from the GBIF API, filtered to:

- European geographic extent  
- Critically Endangered (CR)  
- Endangered (EN)  
- Vulnerable (VU)  

Occurrence data is aggregated to grid cells to derive:

- total threatened-species records  
- CR / EN / VU category counts  
- multi-category risk indicators  

Additionally, GBIF occurrence records are linked back to priority grid cells within Power BI to provide species-level drill-down tables for Priority-1 zones, allowing conservation agencies to vi
