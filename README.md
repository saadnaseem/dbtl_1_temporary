# DBTL1 Analysis

Media and OD600 analysis for DBTL1 (Design-Build-Test-Learn cycle 1).

## Purpose

Analyze OD600 growth data across media conditions, assess replicate variability (CV), remove outliers, and explore relationships between media components and growth.

## Inputs

- **Results.xlsx** – Primary input (288 rows × 21 columns). Required.
- **df_combined_low_cv.csv** – Optional intermediate; can be loaded for plotting if the notebook was run previously.

## Data Structure

Main columns in `Results.xlsx`:

| Column | Description |
|--------|-------------|
| Condition_ID | Unique condition identifier (e.g., MPOB_001, ctrl_media_1) |
| MPOB_Condition_Number | Numeric condition index |
| Well, plate | Well and plate identifiers |
| Total_Phosphate_mM, (NH4)2SO4_mM, CoCl2 mM, Succinate_mM, Methanol_mM, PQQ mM | Media components |
| OD600_t1, OD600_t2, OD600_t3 | Optical density at timepoints 1–3 |
| Abs660_*_arsenazo_assay | Arsenazo assay absorbances |
| Nd_uM_t1, Nd_uM_t2, Nd_uM_t3 | Neodymium concentration (μM) |

## Analysis Steps

1. **Setup** – Imports and load `Results.xlsx`
2. **Data Overview** – Shape, columns, and first rows
3. **OD600 Summary by Condition** – Mean and standard deviation of OD600_t2 per Condition_ID
4. **CV Analysis** – Color-coded CV table and bar chart
5. **Outlier Removal (Triplicates)** – Leave-one-out for 4-replicate conditions; triplicate CV
6. **Filter Low-CV Conditions** – Keep conditions with CV < 20%
7. **Combined Dataset** – Merge media components with OD600 stats; filter to low-CV conditions
8. **Exploratory Plots** – Univariate scatter plots, pairwise interactions, correlation heatmaps, parallel coordinates, response surfaces, PCA

## Outputs

- **df_combined_low_cv.csv** – Filtered dataset (media + OD600 stats, CV < 20%), saved to parent `analysis/` folder
- Plots – CV bar charts, scatter plots, heatmaps, response surfaces

## Dependencies

- pandas
- matplotlib
- numpy
- openpyxl (for Excel)

## Usage

Run cells top to bottom. The notebook will:

1. Load `Results.xlsx` from the same directory
2. Compute OD600 statistics and CV
3. Filter to low-CV conditions
4. Export `../df_combined_low_cv.csv`
5. Generate exploratory plots
