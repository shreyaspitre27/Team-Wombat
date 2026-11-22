# Modelling Marine Debris Movement and Ocean Behaviour in the North Atlantic

**Group Wombat**

**Members:** Ayantika Jana, Shreyas Siddhartha Pitre, Caleb Khor, Jason Kwok, Kyle Lawther

## 1. Abstract
One of the most prevalent environmental issues for our oceans is marine debris. Given the vast size of the ocean and its complex and interconnected system of currents, tracking and cleaning up waste in the oceans is often more difficult than it appears.

Locating marine debris is highly complex and deceptively difficult. While scientists know where the five major ocean gyres are (Mitchell & Shirah, 2014), finding the actual garbage inside them is not as simple as looking at a satellite photograph. Ocean behaviour is far from uniform: fast currents, swirling eddies and seasonal changes, all move water differently. Debris released close together can end up in very different places depending on the ocean behaviour it encounters. This inconsistency makes debris tracking unreliable with uniform assumptions, motivating approaches that utilize modelling regional ocean behaviour.

This study forecasts drifter positions, as a proxy for marine debris, in the North Atlantic (10°-45°N, 80°-20°W), and compares three forecasting models. 

**Model 1** divides the region into 0.1° × 0.1° cells and models drifter movements using a Markov chain, with a single transition matrix estimated from observed 6-hour cell-to-cell movements. Forecasts are made by propagating this matrix forward in time.

**Model 2** extends this approach by estimating four seasonal transition matrices to test whether accounting for seasonal changes in currents changes forecasts. 

**Model 3** takes a different, regression-based approach: it predicts each drifter’s displacement over the forecast horizon directly from its current position and recent movement. 

All three models are trained and tested using 5-fold cross-validation by drifter and evaluated against a persistence baseline using Mean Absolute Error (MAE), Skill score and the Energy Score. Together, they assess how well data-driven models can predict where debris ends up, to support more effective tracking and clean-up.

## 2. Background & Significance

The ocean plays a vital role for life on Earth and for modern humanity. They regulate the planet's climate  (NOAA, 2021)  and mitigate the effects of climate change by absorbing carbon emission and excess heat (UN, 2022). 80% of goods by volume are traded through marine transport (UNCTAD, 2025). They also provide 17% of the world’s meat (Costello et al., 2020) and fisheries support tens of millions of jobs (UN, 2022). The oceans are also home to over 260,000 species (WWF, 2019).

However, the ocean is also threatened by marine debris. In the Great Pacific Garbage Patch, over 46% consisted of fishing nets, and whilst microplastics consisted of only 8% of mass, they were over 94% of the 1.8 trillion pieces in the garbage patch (Leberton et al., 2018). According to a study in the North Atlantic (Reisser et al., 2015), plastics are more concentrated in the first few metres of the ocean.The UN estimated that 5 to 12 million tonnes of plastic enters the oceans each year (UN, 2020). 

This is harmful to marine life, which can become entangled in or consume plastics, causing them harm (WWF, 2025). It also estimated that damages from marine debris cost over $21 billion USD annually as of 2020, and the cumulative costs could be as high as $434 billion USD by 2050. These damages are incurred across multiple sectors, including shipping and tourism (McIlgorm, 2022). 

The importance of the oceans and the threats posed by marine debris motivated the following research questions and objectives.

## 3. Research questions and objectives

|     | Questions |
| --- | --- |
| Question 1 | Are drifters a good proxy for ocean rubbish?  |
| Question 2 | Do ocean cells form clusters based on characteristics measured by drifters?  |
| Question 3 | If drifters proxy marine debris, can we forecast the location they end up in? | 

|     | Objectives |
| --- | --- |
| Objective 1 | Classify the ocean cells in the North Atlantic into distinct regions based on their features, providing local researchers, authorities and organisations a better understanding of the ocean |
| Objective 2 | Create visualisations of marine debris forecast to provide authorities and organisations with the best information on where cleanup is needed  |
| Objective 3 | Exploring how seasonality affects marine debris dispersion |
| Objective 4 | Investigate whether linear regression with latitude, longitude and lag of displacements in both directions acts as a good baseline model |


## 4. Existing Studies & Opportunities

There are studies that focus on the accumulation of garbage and prove the location of several garbage patches across the Earth’s surface, including the Great Pacific Garbage Patch, which is the largest accumulation of plastic in the world. This includes research of drifters and their ability to track garbage accumulation by also analysing ocean behaviour through the GDP data (Lee et al., 2025).

Past studies have shown a link between seasonality and drifter behaviour. A notable paper was able to divide the year into clusters based on the seasons/SST changes and drifter behaviour (Rodríguez-Méndez et al., 2026). This allows for the opportunity to potentially look into the differences in drifter movement depending on the season through analysing SST and current velocity.

<p align="center">
  <img width="512" height="275" alt="season" src="https://github.com/user-attachments/assets/3ba9ad16-229a-4cbc-9af1-4c911915dd68" />
</p>

Previous research into garbage accumulation mainly visualise the projection of garbage using current GDP data, and project marine debris movement over a longer time period. We aim to create a final product that can predict where garbage will end up by extrapolating from the data, which is a prime opportunity for clear and certain paths to garbage patches for future clean up. We also wish to forecast in the short term, aiming to forecast up to 30 days into the future.



## 5. Data & Region description
**Dataset:** GDP 6-hour Drifter (clouddrift.datasets.gdp6h()) <br>
**Region:** North Atlantic Ocean from 10°N 80°W to 45°N 20°W <br>
**Time Period:** 1990-2022 <br>
**Key Variables:** Latitude, Longitude, Eastward Velocity, Northbound Velocity, Temperature <br>

|   Data Summary  |     |
| --- | --- |
|  Total observations (Complete Observations)   | 6,116,067 (5,712,403) |
| Number of Drifters | 3,896  |
| Number of Ocean Cells | 194,571 |
| Cell Size   | 0.1° x 0.1° (approximate 11 x 11 km at Equator) | 

The North Atlantic Ocean was selected as our study region due to its vast geographic scale, rich marine biodiversity, high concentration of major shipping lanes, and substantial economic and geopolitical significance. Since accurately predicting drifter movements over extended horizons requires a high volume of observational data, a 30-year study period was selected.

## 6. Data Setup and Technical Instructions

All analysis was carried out in a Python environment using Jupyter Notebook (`.ipynb`), with one notebook for each model. The notebooks can also be run in Google Colab without any environment installation, by uploading the `.ipynb` files.

The first cell of every notebook installs the package the study needs: <br>
Install Python version **3.10** or later and install **Juptyer** with `pip install notebook`. <br>
`!pip install -q "zarr<3" "xarray==2025.1.2" clouddrift` <br>
`!pip install -q cartopy` <br>
  a. `CloudDrift` gives direct access to the Global Drifter Program. Its `gdp6h()` downloads the 6-hourly drifter dataset the first    time it is called <br>
  b. `xarray` handles the dataset returned. It is pinned to version 2025.1.2 to ensure compatibility and uniformity across every model <br>
  c. `zarr` is the storage format the dataset is read from <br>
  d. `Cartopy` draws the geographic maps used in the models <br>

Additional libraries imported in the model are as follows-

| Library | Imported as / from | Used for |
|---|---|---|
| **NumPy** | `numpy` | Numerical calculations and arrays |
| **pandas** | `pandas` | Data tables (DataFrames) and time handling |
| **SciPy** | `scipy.sparse` (`coo_matrix`, `csr_matrix`) | Sparse transition matrices |
| **scikit-learn** | `KFold`, `train_test_split`, `StandardScaler`, `GaussianMixture` | Cross-validation, feature scaling and clustering |
| **Matplotlib** | `pyplot`, `colors` (`Normalize`, `LogNorm`), `cm.ScalarMappable`, `patches`, `patheffects` | Plots, colour scales and map annotations |
| **seaborn** | `seaborn` | Statistical plot styling |
| **Shapely** | `shapely.geometry`, `shapely.prepared.prep`, `shapely.ops.unary_union` | Land and ocean masking of grid cells |
| **Python standard library** | `re`, `warnings` | Text pattern matching and suppressing warnings |

## 7. Initial analysis and visualization (`Initial_Analysis.ipynb`)
### 7.1 Drifters as a Marine Debris proxy

Prior research validated using Global Drifter Program (GDP) trajectories as a proxy for floating marine debris. For instance, NASA’s Scientific Visualisation Studio, 2015 uses GDP drifter data to model surface garbage accumulation, while UNSW researchers (van Sebille et al., 2012) used drifter data to track macro-scale marine debris dispersion. Following van Sebille et al., we decided to use both drogued and undrogued drifters: drogued drifters follow the sub-surface currents closely while undrogued ones experience wind effects, together capturing the variety of buoyancy and drag profiles of real ocean debris while also maximising sample size.

### 7.2 Summary of Data
Building on this approach, we conducted an initial exploratory analysis of the **gdp6h** dataset at both the global level and within our target region.

<p align="center">
  <img width="512" height="206" alt="initial" src="https://github.com/user-attachments/assets/81afafb7-6b34-435a-a21e-4bfca3f9bafd" />
</p>

### 7.3 Velocity and Sea Surface Temperature

For each 0.1° × 0.1° cell, the $mean_{ve}$, $mean_{vn}$, and $mean_{sst}$ were calculated and then, visualizations below were made to analyze our region in more detail. It was found to have a resultant maximum net speed of **0.54 m/s**, along with the SST ranging from **12.85°C** to **28.55°C**.

<div align="center">
  <table>
    <tr>
      <td> <img width="512" height="436" alt="velocity" src="https://github.com/user-attachments/assets/7b9e1a1d-e34e-49cb-9a1a-6acc146818cf" />
 </td>
      <td> <img width="512" height="433" alt="sst" src="https://github.com/user-attachments/assets/21443c7f-c3e2-4480-9552-ff4e6b9729d2" />
 </td>
    </tr>
  </table>
</div>

In the velocity heat map on the left, the Gulf Stream stands out immediately off the North American coast. The Caribbean also has some faster moving waters. Whilst the central North Atlantic seems quiet, there are streaks of gradually moving currents throughout.
As expected, sea surface temperature generally cools towards higher latitudes. Notable features include the Gulf Steam, which is warmer than its surrounding regions,and the sudden transition to cool waters, represented by dark blue, near New England and Atlantic Canada.The Caribbean is also warmer than other areas at the same latitudes.

### Ocean Clustering

To answer our first objective, an unsupervised machine learning model was used to classify our region, the North Atlantic Basin, into distinct ocean clusters. A **Gaussian Mixture Model** (GMM) was applied to the valid spatial grid cells.
GMM was chosen over simpler distance-based clustering methods (such as K-Means) because representing the data as a combination of overlapping multi-dimensional normal (Gaussian) distributions would allow the model to capture the natural, irregularly shaped patterns typical of ocean current and temperature fronts.

The clustering workflow consisted of three core stages:<br>
  - **Independent Feature Standardization and Equal Weighting:** As current velocities (m/s) and sea surface temperatures (°C) have different units and scales, they were standardized separately using StandardScaler - one scaler for the east-west and north-south velocities (`mean_ve`, `mean_vn`) and another for temperature (`mean_sst`). <br>
Equal weights of 1.0 were applied before using them so that flow and temperature contributed equally.  <br>
  - **Hyperparameter Tuning and  Automated Model Selection using BIC:** Candidate cluster counts (k $\in$ [2,3,4,5,6,7,8,10,12]) were tested using full covariance matrices so clusters could take elliptical shapes. <br>
Using the Bayesian Information Criterion (BIC), *k=4*  was automatically selected  -  adding another cluster yielded less than 1% relative gain in BIC. <br>
  - **Cluster Assignment and Profiling:** Finally, the GMM was refitted using 4 clusters, assigning each grid cell to its most probable regime, along with a probabilistic confidence score. <br>
  <br>
Mapping and profiling these clusters clearly highlighted major oceanographic features, including the Sargasso Sea, North Equatorial Current, Gulf Stream, and North Atlantic Current. <br>
<br>

<p align = "centre">
<img width="1222" height="1038" alt="clusters" src="https://github.com/user-attachments/assets/1fcbb3b0-0b8c-47a8-a73e-a8204b888b76" />
  </p>
  
<div align="center">

### Table of Ocean Cluster Profiles

| cluster | n_cells | ve_mean | vn_mean | speed_mean | sst_mean | sst_std | confidence | share_% |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 0 | 130939 | -0.040 | -0.000 | 0.071 | 24.6000 | 2.192 | 0.888 | 67.307 |
| 1 | 34139 | 0.069 | -0.003 | 0.130 | 17.7740 | 3.933 | 0.862 | 17.549 |
| 2 | 22025 | -0.184 | 0.040 | 0.245 | 27.5050 | 0.835 | 0.821 | 11.322 |
| 3 | 7436 | 0.158 | 0.221 | 0.583 | 24.0050 | 3.722 | 0.874 | 3.822 |

</div>

Across all four identified regimes, the mean assignment confidence remained consistently high (> 80%), indicating well-separated, statistically reliable cluster boundaries. <br>
With the ocean basin reliably segmented into distinct regimes, we next applied a first-order Markov Chain transition matrix to the 6-hourly drifter trajectories to capture a macro-level picture of marine debris movement between regimes. <br>
<br>

<p align = "center"> <b>Initial first-order Markov Chain </b></p>
<p align = "centre">
  <img width="1210" height="940" alt="initial_markov" src="https://github.com/user-attachments/assets/b0571771-33ca-49d5-a82b-8a1ddc277956" />
</p>

However, the results were largely inconclusive for two main reasons: <br>
  - **High Same-Cluster Retention:** Drifters mostly stayed within their current cluster (with self-transition probabilities between 0.698 and 0.964), which undermined the idea of using clusters to track macro-level movement across regimes. <br>
  - **Broad Spatial Clusters:** These high self-transition probabilities were observed because each cluster covered huge areas - with Cluster 0 alone taking up 67.307% of valid grid cells. Drifters could easily travel long distances locally without changing cluster labels, causing fine-scale movements to go unrecorded. <br>
  <br>
Thus, for further analysis, we decided to stick with dividing the region into fine  0.1° × 0.1° cells and conducting the analysis at that grid resolution.

## 8. Methodology


## Model 1 (`Model_1.ipynb`)

## Model 2 (`Model_2.ipynb`)

## Model 3 (`Model_3.ipynb`)

## 9. Discussion of Results

## 10. Conclusion

## 11. Scope and Limitations

1. Since data about the ocean will be collected from drifters, not all cells are guaranteed to have drifter data, especially after filtering for incomplete data. It may be substituted with other data, such as meteorological data, but finding a proper format and combining it with the drifter data may be technically challenging.
2. Due to computation limitations, the six hourly dataset was used instead of a higher frequency. This study relies on this aggregated dataset to be a good approximation of ocean conditions at the measured time.
3. A key assumption of this project and its usefulness is that drifters are a good proxy for plastic waste. Whilst drifters have been used as a proxy for plastic waste in previous studies, they establish that not all plastic waste behaves the same and that drouged and undrouged drifters are more useful for modelling different types of plastics (England et al, 2012). 


## 12. Future Work

## 13. AI Usage Statement & Reflection
### References

1. Furner, Haynes, Jones, Munday, Paige & Shuckburgh (2025). The Challenge of land in a Neural Network Ocean Model, Environmental Data Science https://www.cambridge.org/core/journals/environmental-data-science/article/challenge-of-land-in-a-neural-network-ocean-model/845CF0FEF5898072DA1262564D52B494
2. Lee, D.-K., & Maximenko, N. (2025). Surface drifters and Ocean Dynamics: A review of technological advancements and scientific contributions. Ocean Science Journal, 60(2). https://doi.org/10.1007/s12601-025-00217-x
3. McIlgorm, A., Raubenheimer, K., McIlgorm, D. E., Nichols, R. (2022). The cost of marine litter damage to the global marine economy. International Knowledge Hub Against Plastic Pollution. https://ikhapp.org/stories-and-research-brief/the-cost-of-marine-litter-damage-to-the-global-marine-economy/
4. Nikolai, M., Hafner, J., & Niiler, P. (2012). Pathways of marine debris derived from trajectories of Lagrangian drifters. At-Sea Detection of Derelict Fishing Gear, 65(1), 51–62. https://doi.org/10.1016/j.marpolbul.2011.04.016
5. Rodríguez-Méndez, V., Ser-Giacomi, E., Ramasco, J. J., López, C., Hernández-García, E. (2026). A Comparative Analysis of Clustering Algorithms for Characterizing Surface Ocean Variability in the Western Mediterranean [Campus Universitat de les Illes Balears]. https://arxiv.org/html/2605.26666v1#bib.bib20
6. Shirah, G., & Mitchell, H. (2015, August 10). Garbage patch visualization experiment. NASA Scientific Visualization Studio. https://svs.gsfc.nasa.gov/4174
7. van Sebille, E., England, M. H., & Froyland, G. (2012). Origin, dynamics and evolution of ocean garbage patches from observed surface drifters. Environmental Research Letters, 7(4), 044040. https://doi.org/10.1088/1748-9326/7/4/044040


