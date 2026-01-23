# Capstone Project: European Fire and Threatened Species Risk Analysis

## Environmental Challenge

Fire activity is increasing in frequency and intensity across Europe, placing growing pressure on ecosystems, protected habitats, and species of conservation concern. Environmental agencies require clear, evidence-based insight into where fire exposure and ecological vulnerability intersect in order to prioritise monitoring, prevention, and conservation action.

---

## Business Requirement

To develop a data-driven spatial risk framework that identifies regions where fire activity overlaps with threatened biodiversity, highlighting geographic areas where conservation assets may be disproportionately exposed to fire risk.

---

## Intended Audience

This project is intended for European environmental protection and conservation agencies responsible for:

- fire preparedness and land management  
- biodiversity protection and monitoring  
- regional conservation prioritisation and policy planning  

The dashboard and README are designed for non-technical stakeholders, while the supporting notebooks provide full technical transparency.

---

## Project Solution

This project analyses five years of NASA FIRMS satellite fire detections across Europe alongside threatened-species occurrence data sourced from GBIF.

Due to the scale of the datasets involved, a grid-based spatial aggregation approach is used to combine fire exposure and biodiversity presence into consistent spatial units. Rather than relying on computationally intensive polygon intersections, fire detections and biodiversity occurrences are aggregated into regular latitude–longitude grid cells.

This approach enables efficient identification of fire–biodiversity hotspot regions while retaining sufficient spatial resolution for continental-scale risk analysis.

Machine-learning techniques are applied selectively to support interpretation rather than operational prediction, ensuring the modelling component complements the spatial risk narrative without obscuring it.

---

## Key Statistical and Data Analysis Methods Used

- Descriptive statistics (counts, averages, distributions)  
- Temporal aggregation (daily → monthly / yearly trends)  
- Spatial analysis (bounding box filtering, grid-based aggregation)  
- Data quality considerations (confidence levels, satellite limitations)  
- Correlation versus causation assessment  

---

## Project Outputs

- A reproducible Python analytics pipeline demonstrating data acquisition, cleaning, spatial aggregation, and modelling  
- A grid-level fire–biodiversity risk table identifying hotspot regions  
- An interactive Power BI dashboard presenting:
  - fire exposure patterns  
  - threatened-species hotspot regions  
  - priority geographic corridors for conservation attention  

This project is not deployed as a web application. Analysis outputs are presented via Jupyter notebooks and an external Power BI dashboard.

**Power BI Dashboard:**  
ADD FINAL LINK HERE

The Power BI dashboard is additionally supplied as a `.pbix` file in the GitHub folder `PowerBI` for transparency and reproducibility.

---

## Dataset Content

### 1. Fire Detection Data

Fire data is sourced from NASA FIRMS (Fire Information for Resource Management System) using the VIIRS satellite product. The dataset covers five consecutive years of European fire detections, providing consistent spatial and temporal coverage.

Each record represents a satellite-detected fire point.

Key attributes include:

- `latitude`, `longitude` – detection coordinates  
- `acq_date`, `acq_time` – detection timestamp  
- `confidence` – detection confidence classification  
- `frp` – Fire Radiative Power (proxy for fire intensity)  
- `daynight` – day/night detection flag  

---

### 2. Threatened Species Occurrence Data

Threatened-species occurrence records are retrieved from the GBIF API and filtered to:

- European geographic extent  
- IUCN threat categories: Critically Endangered (CR), Endangered (EN), and Vulnerable (VU)  

These records provide a spatial representation of biodiversity vulnerability for integration with fire exposure. Occurrence data is aggregated to grid cells to derive:

- total threatened-species records  
- CR / EN / VU category presence  
- multi-category risk indicators  

---

### 3. Protected Areas (Contextual Layer)

A European protected-area spatial dataset is retained as contextual information to support interpretation of hotspot regions.

Due to dataset scale and performance constraints, protected areas are not used as the primary spatial aggregation unit. Instead, hotspot grid cells provide a scalable means of identifying candidate regions where protected-area exposure may warrant further investigation.

---

## Data Extraction and Processing

### Code Evaluation and Improvement

The initial data extraction and processing approach focused on validating access to the NASA FIRMS API and confirming that fire detection data could be retrieved successfully for the study region. While effective for testing, this early approach had limitations when scaled to multi-year analysis.

### Initial Approach and Limitations

- API requests were structured for short time periods and not optimised for large-scale extraction  
- Configuration values were embedded directly within code, reducing reusability  
- Limited handling of partial failures or empty API responses  
- Outputs were not compressed, increasing storage requirements  

### Improvements Implemented

- Introduction of a configuration-driven extraction approach  
- Multi-day windowed downloads to support stable API extraction across five years  
- Automated handling of empty or failed API responses  
- Gzip-compressed CSV outputs to reduce storage overhead  

### Outcome

These improvements resulted in a more reliable, maintainable, and scalable data pipeline suitable for repeated execution and downstream analysis.

---

## Analytical Questions Addressed

- How does fire activity vary across Europe over a five-year period?  
- Are fire detections spatially clustered rather than evenly distributed?  
- Where do fire exposure and threatened biodiversity co-occur?  
- Do fire–biodiversity hotspots represent isolated species risk or compounded conservation risk?  
- Which geographic corridors show disproportionately high fire–biodiversity overlap?  

---

## Analysis Techniques Used

- Data cleaning and temporal standardisation  
- Feature engineering (seasonality, spatial binning, biodiversity indicators)  
- Single-variable and multi-variable exploratory analysis  
- Grid-based spatial aggregation  
- Unsupervised clustering (KMeans) to profile fire–biodiversity risk patterns  
- Static and interactive visualisation (Matplotlib, Seaborn, Plotly)  

Machine-learning techniques are used to support exploratory risk profiling rather than operational prediction.

---

## Key Analytical Findings

### Exploratory Analysis

- Fire–biodiversity risk is spatially concentrated rather than evenly distributed across Europe  
- Distinct longitudinal corridors, notably 0–10°E and a corridor near ~38°E, show over-representation of hotspot grid cells  
- Approximately two-thirds of hotspot grid cells contain multiple threatened categories (CR, EN, VU), indicating compounded conservation risk  
- Several hotspot regions combine moderate fire exposure with high biodiversity vulnerability, highlighting areas where relatively small increases in fire pressure may have disproportionate ecological impact  

### Cluster Modelling: Method and Rationale

Unsupervised clustering (KMeans) was applied to grid-level fire and biodiversity indicators to identify distinct risk profiles without imposing predefined thresholds.

Clustering supports comparative risk interpretation by grouping grid cells with similar fire exposure and biodiversity characteristics, enabling prioritisation based on relative rather than absolute risk.

### Cluster Modelling: Findings

Four distinct fire–biodiversity risk clusters were identified, representing progressively increasing combinations of fire frequency, fire intensity, and threatened-species presence. These clusters form the basis for prioritisation tiers used within the dashboard.

---

## Dashboard Design

The final dashboard prioritises clarity and accessibility for non-technical users. Statistical analysis is embedded within intuitive visuals and summary metrics rather than exposed as technical outputs.

The dashboard presents:

- five-year fire exposure patterns using aggregated counts and average intensity metrics  
- spatial fire–biodiversity hotspot maps derived from grid-based overlays  
- identification of priority geographic corridors based on comparative fire density and persistence  
- simple, interpretable summary statistics to support conservation prioritisation  

Detailed modelling techniques are intentionally excluded from the dashboard interface and documented fully within the supporting notebooks.

---

## Actionable Insights

The dashboard translates analytical findings into four prioritisation groups:

- **Priority 1:** Highest combined fire exposure and biodiversity vulnerability  
- **Priority 2:** High biodiversity vulnerability with moderate fire exposure  
- **Priority 3:** High fire exposure with lower biodiversity vulnerability  
- **Priority 4:** Lower relative risk across both dimensions  

These groupings enable focused conservation attention and resource allocation.

---

## Ethical Considerations

- All datasets are publicly available and contain no personal data  
- Satellite fire detections may include false positives or missed events  
- Biodiversity occurrence data may be spatially biased toward surveyed regions  
- Outputs are intended for educational and analytical purposes, not operational emergency response  
- Interpretations remain within the limits of available data  

---

## Tools and Libraries

- Python  
- Pandas, NumPy  
- Matplotlib, Seaborn, Plotly  
- GeoPandas, Shapely, PyProj, Rtree  
- Scikit-learn, Feature-engine, Imbalanced-learn, XGBoost  
- YData Profiling, PPSCore  
- Requests  
- Jupyter Notebook  
- Power BI  

---

## Notebook–README Alignment

| Notebook | Purpose | README Section |
|--------|--------|---------------|
| Notebook 01 | Data acquisition | Dataset Content |
| Notebook 02 | Cleaning and feature engineering | Analysis Techniques |
| Notebook 03 | Exploratory analysis | Analytical Questions |
| Notebook 04 | Modelling (clustering) | Key Analytical Findings |
| Notebook 05 | Spatial hotspot analysis | Key Findings |
| Dashboard | Visual communication | Dashboard Design |

---

## Limitations

- Satellite detections may be affected by cloud cover, sensor resolution, and orbital timing  
- Fire confidence values are categorical rather than probabilistic  
- The five-year analysis window does not capture longer-term climate variability  
- Bounding-box spatial filtering introduces minor spatial generalisation  
- Near-real-time fire data is treated as unverified and excluded from modelling  

GBIF-provided IUCN categories reflect the status recorded at the time of data indexing and may not always match the most recent Red List classification.

---

## Future Work

- Extend analysis to longer historical time series  
- Integrate meteorological variables to support predictive modelling  
- Refine spatial resolution through alternative grid or hex-based aggregation  
- Validate results against ground-reported fire datasets  
- Expand dashboard to support scenario-based conservation planning  
- Implement monitored live-data pipelines with quality checks  
- Integrate direct IUCN API validation for updated threat classifications  

---

## Credits

- Code Institute course materials  
- Python library official documentation  
- VS Code Copilot  
- ChatGPT  
- Power BI Copilot  

---

## Acknowledgements

This project was completed as part of the Code Institute Data Analytics programme.

---

## Reflections

This project reinforced the importance of scalable spatial analysis techniques when working with continental-scale environmental datasets. The use of grid-based aggregation and interpretable clustering enabled meaningful conservation insights while maintaining analytical transparency and reproducibility.
