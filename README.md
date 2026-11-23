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

Previous studies on marine debris accumulation have identified major oceanic garbage patches and proved the location of several garbage patches across the Earth’s surface, including the Great Pacific Garbage Patch, which is the largest accumulation of plastic in the world (The Ocean Cleanup, 2025). There are also studies that have researched into drifter behaviour and how they can track marine debris movement through analysis of ocean current data (Lee et al., 2025).

Maximenko’s analysis into drifter movement shows that the “...probability for a drifter to travel between two locations depends only on the duration of the travel but does not depend on the selection of the start time moment” (Maximeko et al., 2012). This characteristic of drifters satisfies the Markov memoryless property, where the movement of a drifter is independent of its previous location. This provides for the possibility to conduct a probabilistic Markov approach for prediction of drifter movement.

Past studies have also shown a link between seasonality and drifter behaviour. A notable paper was able to divide the year into clusters based on the seasons/SST changes and drifter behaviour (Rodríguez-Méndez et al., 2026). This allows for the opportunity to look into the differences in drifter movement depending on the season.

<p align="center">
  <img width="512" height="275" alt="season" src="https://github.com/user-attachments/assets/3ba9ad16-229a-4cbc-9af1-4c911915dd68" />
</p>

Previous research into garbage accumulation mainly visualise the projection of garbage using current GDP data, and project marine debris movement over a longer time period. 

We aim to create a final product that can predict where garbage will end up in the short-term horizon by extrapolating from the data, which creates an opportunity for a more accurate, targeted cleanup. 


## 5. Data & Region description
**Dataset:** GDP 6-hour Drifter (clouddrift.datasets.gdp6h()) <br>
**Region:** North Atlantic Ocean from 10°N 80°W to 45°N 20°W <br>
**Time Period:** 1990-2022 <br>
**Key Variables:** Latitude, Longitude, Eastward Velocity, Northbound Velocity, Temperature <br>
<br>
<br>
|   Data Summary  |     |
| --- | --- |
|  Total observations (Complete Observations)   | 6,116,067 (5,712,403) |
| Number of Drifters | 3,896  |
| Number of Ocean Cells | 194,571 |
| Cell Size   | 0.1° x 0.1° (approximately 11 x 11 km at Equator) | 

The North Atlantic Ocean was selected as our study region due to its vast geographic scale, rich marine biodiversity, high concentration of major shipping lanes, and substantial economic and geopolitical significance. 

Since accurately predicting drifter movements over extended horizons requires a high volume of observational data, a 30-year study period was selected.

## 6. Data Setup and Technical Instructions

All analysis was carried out in a Python environment using Jupyter Notebook (`.ipynb`), with one notebook for each model. The notebooks can also be run in Google Colab without any environment installation, by uploading the `.ipynb` files.

The first cell of every notebook installs the package the study needs: <br>
Install Python version **3.10** or later and install **Juptyer** with `pip install notebook`. <br>
`!pip install -q "zarr<3" "xarray==2025.1.2" clouddrift` <br>
`!pip install -q cartopy` <br>
  a. `CloudDrift` gives direct access to the Global Drifter Program. Its `gdp6h()` downloads the 6-hourly drifter dataset the first time it is called <br>
  b. `xarray` handles the dataset returned. It is pinned to version 2025.1.2 to ensure compatibility and uniformity across every model <br>
  c. `zarr` is the storage format the dataset is read from <br>
  d. `Cartopy` draws the geographic maps used in the models <br>

Additional libraries imported in the model are as follows:

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

Prior research validated using Global Drifter Program (GDP) trajectories as a proxy for floating marine debris. For instance, NASA’s Scientific Visualisation Studio, 2015 uses GDP drifter data to model surface garbage accumulation, while UNSW researchers (van Sebille et al., 2012) used drifter data to track macro-scale marine debris dispersion. 
Following van Sebille et al., we decided to use both drogued and undrogued drifters: drogued drifters follow the sub-surface currents closely while undrogued ones experience wind effects, together capturing the variety of buoyancy and drag profiles of real ocean debris while also maximising sample size.

### 7.2 Summary of Data
Building on this approach, we conducted an initial exploratory analysis of the **gdp6h** dataset at both the global level and within our target region.

<p align="center">
  <img width="512" height="206" alt="initial" src="https://github.com/user-attachments/assets/81afafb7-6b34-435a-a21e-4bfca3f9bafd" />
</p>

### 7.3 Velocity and Sea Surface Temperature

For each 0.1° × 0.1° cell, the $mean_{ve}$, $mean_{vn}$, and $mean_{sst}$ were calculated and then, visualizations below were made to analyze our region in more detail. It was found that our region has a resultant maximum net speed of **0.54 m/s**, along with the SST ranging from **12.85°C** to **28.55°C**.

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

On the right, sea surface temperature generally cools towards higher latitudes. Notable features include the Gulf Steam, which is warmer than its surrounding regions,and the sudden transition to cool waters, represented by dark blue, near New England and Atlantic Canada. The Caribbean is also warmer than other areas at the same latitudes.

### 7.4 Ocean Clustering

To answer our first objective, an unsupervised machine learning model was used to classify our region, the North Atlantic Basin, into distinct ocean clusters. A **Gaussian Mixture Model** (GMM) was applied to the valid spatial grid cells.

GMM was chosen over simpler distance-based clustering methods (such as K-Means) because representing the data as a combination of overlapping multi-dimensional normal (Gaussian) distributions would allow the model to capture the natural, irregularly shaped patterns typical of ocean current and temperature fronts.

The clustering workflow consisted of three core stages:<br>
  - **Independent Feature Standardization and Equal Weighting:** As current velocities (m/s) and sea surface temperatures (°C) have different units and scales, they were standardized separately using StandardScaler - one scaler for the east-west and north-south velocities (`mean_ve`, `mean_vn`) and another for temperature (`mean_sst`). <br>
Equal weights of 1.0 were applied before using them so that flow and temperature contributed equally.  <br>
  - **Hyperparameter Tuning and  Automated Model Selection using BIC:** Candidate cluster counts (k $\in$ [2,3,4,5,6,7,8,10,12]) were tested using full covariance matrices so clusters could take elliptical shapes. <br>
Using the Bayesian Information Criterion (BIC), *k=4*  was automatically selected  -  adding another cluster yielded less than 1% relative gain in BIC. <br>
  - **Cluster Assignment and Profiling:** Finally, the GMM was refitted using 4 clusters, assigning each grid cell to its most probable regime, along with a probabilistic confidence score. <br>
Mapping and profiling these clusters clearly highlighted major oceanographic features, including the Sargasso Sea, North Equatorial Current, Gulf Stream, and North Atlantic Current. <br>
<br>

<p align = "center">
<img width="512" height="400" alt="clusters" src="https://github.com/user-attachments/assets/1fcbb3b0-0b8c-47a8-a73e-a8204b888b76" />
  </p>
  
<div align="center">

### Table of Ocean Cluster Profiles

| <sub>cluster</sub> | <sub>n_cells</sub> | <sub>ve_mean</sub> | <sub>vn_mean</sub> | <sub>speed_mean</sub> | <sub>sst_mean</sub> | <sub>sst_std</sub> | <sub>confidence</sub> | <sub>share_%</sub> |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <sub>0</sub> | <sub>130939</sub> | <sub>-0.040</sub> | <sub>-0.000</sub> | <sub>0.071</sub> | <sub>24.6000</sub> | <sub>2.192</sub> | <sub>0.888</sub> | <sub>67.307</sub> |
| <sub>1</sub> | <sub>34139</sub> | <sub>0.069</sub> | <sub>-0.003</sub> | <sub>0.130</sub> | <sub>17.7740</sub> | <sub>3.933</sub> | <sub>0.862</sub> | <sub>17.549</sub> |
| <sub>2</sub> | <sub>22025</sub> | <sub>-0.184</sub> | <sub>0.040</sub> | <sub>0.245</sub> | <sub>27.5050</sub> | <sub>0.835</sub> | <sub>0.821</sub> | <sub>11.322</sub> |
| <sub>3</sub> | <sub>7436</sub> | <sub>0.158</sub> | <sub>0.221</sub> | <sub>0.583</sub> | <sub>24.0050</sub> | <sub>3.722</sub> | <sub>0.874</sub> | <sub>3.822</sub> |

</div>

Across all four identified regimes, the mean assignment confidence remained consistently high (> 80%), indicating well-separated, statistically reliable cluster boundaries. 

With the ocean basin reliably segmented into distinct regimes, we next applied a first-order Markov Chain transition matrix to the 6-hourly drifter trajectories to capture a macro-level picture of marine debris movement between regimes. <br>
<br>

<p align = "center"> <b>Initial first-order Markov Chain </b></p>
<p align = "center">
  <img width="512" height="400" alt="initial_markov" src="https://github.com/user-attachments/assets/b0571771-33ca-49d5-a82b-8a1ddc277956" />
</p>

However, the results were largely inconclusive for two main reasons: <br>
  - **High Same-Cluster Retention:** Drifters mostly stayed within their current cluster (with self-transition probabilities between 0.698 and 0.964), which undermined the idea of using clusters to track macro-level movement across regimes. <br>
  - **Broad Spatial Clusters:** These high self-transition probabilities were observed because each cluster covered huge areas - with Cluster 0 alone taking up 67.307% of valid grid cells. Drifters could easily travel long distances locally without changing cluster labels, causing fine-scale movements to go unrecorded. <br>
  <br>
Thus, for further analysis, we decided to stick with dividing the region into fine  0.1° × 0.1° cells and conducting the analysis at that grid resolution.

## 8. Methodology
This study divides the North Atlantic basin region into grids of 0.1° × 0.1° cells and models drifter transition within these cells using the data. <br>
<br>
Each observation within the cleaned dataset records the drifter ID, time, latitude and longitude, velocities, temperature and drogue status sorted by ID and time so that each drifter’s trajectory could be followed step-by-step. <br>
<br>
To ensure that models were trained and tested in the same manner, all three models use the 5-Fold cross-validation split on drifter ID. Due to this, no trajectory appears in both the training and testing sets. Each drifter is held out exactly once and the results are averaged over the folds, with further assessment done on the best performing fold due to computational limits.<br>
<br>

**Markov Chain**
Models 1 and 2 model drifter movements using discrete-time Markov Chain. Using the coordinates, each position is mapped to a state/cell index using the following formulas: <br>

$$
row = \frac{\left[ LAT_{max} - lat \right]}{0.1}
$$
$$
col = \left\lfloor \frac{lon - LON_{min}}{0.1} \right\rfloor
$$
$$
state = row \times N_{lon} + col
$$
<br>

giving a total of 350 x 600 = **210,000** states. <br>
<br>
Subsequently, the central coordinates of the corresponding grid are mapped using the following formulas: <br>
<br>

$$
row = \left\lfloor \frac{state}{N_{lon}} \right\rfloor \qquad col = state \bmod N_{lon}
$$

$$
lat = LAT_{max} - (row + 0.5)\Delta \qquad lon = LON_{min} + (col + 0.5)\Delta
$$

<br>

A transition is defined as two consecutive observations from the same drifter exactly 6 hours apart. Counting all such transitions in the training data gives a count matrix `N` where `N_ij` is the number of moves from cell i to cell j. Normalising each row gives the transition probability matrix: <br>

$$
P_{ij} = \frac{N_{ij}}{\sum_k N_{ik}}
$$

<br>

`P` is stored as a sparse **210,000 x 210,000** matrix. To forecast `n_steps` ahead (`n_steps` x 6 hrs), an initial distribution $\pi^{(0)}$ concentrated on the start cell is propagated as $\pi^{(n)} = \pi^{(0)} P^n$.<br>
The point forecast is the most probable end cell. A probabilistic forecast is also produced by Monte-Carlo simulation of multiple simulated drifters taking random walks, forming a cloud of possible end positions.<br>

Model 2 follows the same procedure as Model 1 but estimates four matrices, one for each season: Mar-May, Jun-Aug, Sep-Nov, Dec-Feb. Each matrix is built only from training transitions whose starting falls in season `q`. Test windows that lie entirely within a single season are forecast using that season’s matrix. Model 2 therefore tests whether including seasonality affects results.

**Linear Regressiom**

Model 3 takes a regression-based approach and predicts a drifter’s total displacement over the forecast horizon without a grid structure. Using Ordinary Least Squares, the eastwards ($\Delta x$) and northward ($\Delta y$) displacements in km are modelled as: <br>

$$
\Delta x = \beta_{0,x} + \beta_{1,x} lat + \beta_{2,x} lon + \beta_{3,x} \Delta x_{lag1} + \beta_{4,x} \Delta y_{lag1} + \varepsilon_x
$$

$$
\Delta y = \beta_{0,y} + \beta_{1,y} lat + \beta_{2,y} lon + \beta_{3,y} \Delta x_{lag1} + \beta_{4,y} \Delta y_{lag1} + \varepsilon_y
$$

Lat and lon are the drifter’s current positions, and $\Delta x_{\text{lag1}}$ and $\Delta y_{\text{lag1}}$ are its east and north displacements over the previous 6 hours, capturing short term momentum. The errors are modelled as a bivariate normal distribution.

### 8.1. Persistence as a Baseline

The performance of the models are compared against a persistence forecast baseline, which assumes that after a duration of every 6 hours, a drifter would stay in the same cell it started in, predicting zero change. As the ocean is inertial (changes slowly), a persistence forecast provides a good baseline for ocean models (Furner et al., 2025). <br>
<br>
Persistence is a possible forecast and sets a standard: a useful model must outperform it.

### 8.2 Evaluation Metrics

All metrics are calculated on test drifters for forecasts of horizons of 3,10 and 15 days. Along with that, an extended horizon of 14 and 30 days, and Monte Carlo simulation is performed on the best performing fold. <br>
<br>
Point forecast error is measured as the great-circle distance between the forecasted and observed endpoint, calculated with the haversine formula, summarised by the Mean Absolute Error over all the test drifters:<br>

$$ 
MAE = \frac{1}{n}\sum_{i=1}^{n}|y_i - \hat{y}_i| 
$$

The probabilistic forecasts are evaluated using the Energy Score, a proper scoring guide for multivariate forecast distributions:<br>

$$
ES = \mathbb{E}\|X - y\| - \frac{1}{2}\mathbb{E}\|X - X'\|,
$$

where `X` and `X’` are independent draws from the forecast cloud `F` and `y` is the observed end position. The first term measures the average distance from the cloud to the observation, and the second term measures the spread of the cloud. The score therefore rewards forecasts that are both accurate and realistically dispersed. <br>
<br>
Performance relative to the persistence baseline is measured by the skill score:<br>

$$
Skill = 1 - \frac{Model}{Persistence}
$$

A positive skill score indicates that the model outperforms persistence, and a negative score indicates it performs worse.  

## Model 1 (`Model_1.ipynb`)

### Aggregate Markov Chain
**Pooled Discrete Time-Markov Chain**
A single, basin-wide discrete time markov chain across our region is built in this model. All historical transitions were pooled into one stationary transition matrix `P` per fold to maximize spatial coverage.

**How the model works**
  - **Spatial discretization:** Dividing our region into grids using grid to state transformations described earlier to get 210,000 discrete states/grids indexed row-wise from the north-west corner (45°N, 80°W).<br>
  - **5-fold cross validation:** For a rigorous analysis, a 5-fold cross validation with 80%/20% split per fold (assigning ~780 unseen drifters to each test fold) is conducted. <br>
  - **Transition matrix formation:** Utilizing `count_transitions`, we compute the transition matrices `P`, one per fold.<br>
  - **Analytical point forecasting using Top-1 and Expected Mean:** In `forecast_points`, we propagated the initial distribution `V` in chunks of 500 starting cells to manage memory, pruning negligible probabilities below $10^(-6)$. For the resulting distribution, the **Top-1** forecast selected the single highest-probability cell, while **Expected Mean** computed the probability-weighted geographic center of mass across all active cells.<br>
  - **Monte Carlo Simulation:** In `simulate_garbage_trajectories`, we simulated `n_sims` particles (500 for evaluation, 1000 for mapping) stepping forward across `n_steps` 6-hour increments. <br>
  - **Evaluation using Haversian MAE & Skill Score vs Persistence:** In `evaluate_cv_forecasts`, we extracted valid test pairs (via `build_pairs_xy`) for 3, 10, and 15 days across all 5 folds, measured the haversian error between the predicted `top1` cell center and true endpoint, comparing against persistence baseline.<br>
  - **Probabilistic Energy Score:** In `evaluate_fold_4_energy_score`, we evaluated the simulated dispersion cloud on Fold 4’s unseen test set across up to 500 starting cells (500 particles per start cell) over 3, 10 and 15 day horizons.<br>
  - **Case-Study Dispersion Forecasts:** To visually validate the model’s physical behavior, we simulated 1,000 particles over a 3, 10 and 15 day horizon in high impact marine zones and shipping lanes - spanning the western boundary current (Off Georgia/Florida, Cape Hatteras and New Jersey/ Virginia shelf-break), coastal fisheries (Georges Bank) and open-ocean subtropical gyre (Maersk Tukang container shear).

### Results and Interpretation

**5-Fold Cross-Validation Summary**

Across all 5 cross-validation folds (over 1 million unseen test pairs per fold), the pooled discrete-time Markov chain consistently outperformed the persistence baseline at every forecast horizon.<br>

| <sub>Fold</sub> | <sub>Horizon_Days</sub> | <sub>Markov_MAE_km</sub> | <sub>Persistence_MAE_km</sub> | <sub>Skill_vs_Persistence_%</sub> |
| :---: | :---: | :---: | :---: | :---: |
| <sub>1</sub> | <sub>3.0</sub> | <sub>50.66</sub> | <sub>51.87</sub> | <sub>+2.3%</sub> |
| <sub>1</sub> | <sub>10.0</sub> | <sub>125.57</sub> | <sub>133.05</sub> | <sub>+5.6%</sub> |
| <sub>1</sub> | <sub>15.0</sub> | <sub>165.35</sub> | <sub>176.98</sub> | <sub>+6.6%</sub> |
| <sub>2</sub> | <sub>3.0</sub> | <sub>48.87</sub> | <sub>49.53</sub> | <sub>+1.3%</sub> |
| <sub>2</sub> | <sub>10.0</sub> | <sub>121.82</sub> | <sub>127.63</sub> | <sub>+4.6%</sub> |
| <sub>2</sub> | <sub>15.0</sub> | <sub>160.69</sub> | <sub>170.05</sub> | <sub>+5.5%</sub> |
| <sub>3</sub> | <sub>3.0</sub> | <sub>48.86</sub> | <sub>49.77</sub> | <sub>+1.8%</sub> |
| <sub>3</sub> | <sub>10.0</sub> | <sub>121.83</sub> | <sub>128.52</sub> | <sub>+5.2%</sub> |
| <sub>3</sub> | <sub>15.0</sub> | <sub>160.93</sub> | <sub>171.72</sub> | <sub>+6.3%</sub> |
| <sub>4</sub> | <sub>3.0</sub> | <sub>49.22</sub> | <sub>50.33</sub> | <sub>+2.2%</sub> |
| <sub>4</sub> | <sub>10.0</sub> | <sub>122.59</sub> | <sub>130.30</sub> | <sub>+5.9%</sub> |
| <sub>4</sub> | <sub>15.0</sub> | <sub>161.92</sub> | <sub>174.32</sub> | <sub>+7.1%</sub> |
| <sub>5</sub> | <sub>3.0</sub> | <sub>50.17</sub> | <sub>51.19</sub> | <sub>+2.0%</sub> |
| <sub>5</sub> | <sub>10.0</sub> | <sub>125.17</sub> | <sub>132.28</sub> | <sub>+5.4%</sub> |
| <sub>5</sub> | <sub>15.0</sub> | <sub>165.61</sub> | <sub>176.85</sub> | <sub>+6.4%</sub> |
<br>
<br>
<br>
**Aggregating across all folds:**

| | <sub>Horizon_Days</sub> | <sub>Markov_MAE_km</sub> | <sub>Persistence_MAE_km</sub> | <sub>Skill_vs_Persistence_%</sub> |
| :---: | :---: | :---: | :---: | :---: |
| <sub>1</sub> | <sub>3.0</sub> | <sub>49.5554</sub> | <sub>50.5406</sub> | <sub>+1.944%</sub> |
| <sub>2</sub> | <sub>10.0</sub> | <sub>123.3979</sub> | <sub>130.3572</sub> | <sub>+5.334%</sub> |
| <sub>3</sub> | <sub>15.0</sub> | <sub>162.9018</sub> | <sub>173.9837</sub> | <sub>+6.364%</sub> |

Because ocean water has strong inertia and slow currents, drifters move smoothly over short windows, making persistence a tough short-term benchmark. <br>
Consistently outperforming it across all 5 folds and at very short horizons of 3, 10 and 15 days proved that our transition matrix learns real ocean movements and not just noise. 

**Extended Horizon Profiling** - Shows how skill scales over 30 days on Fold 4

As Fold 4 achieved the highest validation skill across all splits (+2.2% at 3 days, +5.9% at 10 days and +7.1% at 15 days), we evaluated Fold 4 over an extended 14 and 30 day horizons.

| | <sub>Horizon_Days</sub> | <sub>Markov_MAE_km</sub> | <sub>Persistence_MAE_km</sub> | <sub>Skill_vs_Persistence_%</sub> |
| :---: | :---: | :---: | :---: | :---: |
| <sub>1</sub> | <sub>3.0</sub> | <sub>49.2239</sub> | <sub>50.3306</sub> | <sub>+2.199%</sub> |
| <sub>2</sub> | <sub>10.0</sub> | <sub>122.5912</sub> | <sub>130.3039</sub> | <sub>+5.919%</sub> |
| <sub>3</sub> | <sub>14.0</sub> | <sub>154.5232</sub> | <sub>166.0518</sub> | <sub>+6.943%</sub> |
| <sub>4</sub> | <sub>15.0</sub> | <sub>161.9244</sub> | <sub>174.3233</sub> | <sub>+7.113%</sub> |
| <sub>5</sub> | <sub>30.0</sub> | <sub>255.2866</sub> | <sub>280.3197</sub> | <sub>+8.930%</sub> |

<p align = "center">
<img width="1788" height="662" alt="m1-1" src="https://github.com/user-attachments/assets/706acc3e-b86c-4ae9-a7c9-08ef509541d8" />
</p>

It is observed that the skill score climbs steadily across horizons to +8.93% at 30 days. Over short horizons, local fluid inertia kept persistence competitive, but over longer horizons, inertia broke down and the Markov chain gained an advantage over persistence.

**Probabilistic Energy Score**  - Shows why dispersion clouds beat single-point predictions

Evaluating 500 Monte Carlo particles across up to 500 starting cells on Fold 4’s unseen test set showed Model 1 beating persistence by **~26%** across all horizons.

| <sub>Fold</sub> | <sub>Forecast_Days</sub> | <sub>Mean_Energy_Score_Model</sub> | <sub>Mean_Energy_Score_Persistence</sub> | <sub>Skill_vs_Persistence_%</sub> |
| :---: | :---: | :---: | :---: | :---: |
| <sub>4</sub> | <sub>3.0</sub> | <sub>36.2973</sub> | <sub>48.9699</sub> | <sub>+25.878%</sub> |
| <sub>4</sub> | <sub>10.0</sub> | <sub>100.8931</sub> | <sub>135.8450</sub> | <sub>+25.729%</sub> |
| <sub>4</sub> | <sub>15.0</sub> | <sub>131.1569</sub> | <sub>178.4195</sub> | <sub>+26.490%</sub> |

Rather than relying on point forecasts, the Monte Carlo ensemble captured the realistic spatial spread of drifting debris, making it more practical for marine debris tracking.

**Spatial Case Studies** - Visualizing real ocean dispersions in high impact marine zones

| |
| :---: |
| <img width="1768" height="464" alt="m1-2" src="https://github.com/user-attachments/assets/5ee3f38f-e45b-4d47-b6cc-909b5e35f594" /> |
| <img width="1774" height="488" alt="m1-3" src="https://github.com/user-attachments/assets/a4f1b34b-efbf-4c9f-97e4-3a0f5a8efa5b" /> |
| <img width="1774" height="462" alt="m1-4" src="https://github.com/user-attachments/assets/873b9357-b035-4f9a-bdaa-7c3345370685" /> |
| <img width="1772" height="488" alt="m1-5" src="https://github.com/user-attachments/assets/5ea69a6f-fd38-4911-ba64-965ee38c1a27" /> |
| <img width="1770" height="480" alt="m1-6" src="https://github.com/user-attachments/assets/e1b1db02-f025-4ede-87e5-46d8f06dcb75" /> |

Visualizing dispersion across key marine zones confirmed realistic regional behavior. Simulated clouds stretch northeastward along the fast Gulf Stream while spreading radially in the calmer gyre interior, with actual drifter endpoints landing reasonably inside predicted zones.

### Execution

To execute the model, open `Model_1.ipnyb` from the repository and run all cells sequentially. It automatically installs the required dependencies, loads the 6-hourly drifter dataset and reproduces all the above results and dispersion plots.

## Model 2 (`Model_2.ipynb`)

### Seasonal Markov Chain 

In the second model, we followed the implementation of model 1, the only difference being that we split our cleaned dataset into four meteorological quarters to account for seasonality. 

**How the model works**

  - **Four separate seasonal transition matrices:** The dataset `df` was split into four quarters (`df_q1` for Mar-May, `df_q2` for Jun-Aug, `df_q3` for Sep-Nov, and `df_q4` for Dec-Feb), and separate 210,000210,000 sparse transition matrix Pq were constructed for each season q.<br>
  - **5-fold cross-validation split by drifter:** A 5-fold cross validation with 80%/20% split per fold was shared across all four seasons, ensuring a drifter never appears in training for one season and testing for another. <br>
  - **Strict seasonal and fold isolation:** Within each fold, `P_q` was estimated solely from consecutive 6-hourly fixes of that fold's training drifters occurring inside season *q*. <br>
  - **Same evaluation metrics as Model 1:** Haversian MAE of the most-likely cell (`top1`) vs. a persistence baseline and skill score at 3, 10, and 15 days (all 5 folds) and 14 and 30 days (Fold 4 only), along with Energy Score using 500 Monte Carlo particles at 3, 10, and 15 days (Fold 4) were used.<br>
  - **Intra-season window filtering and coverage:** Candidate test windows were constructed per season so that the **entire forecast window lies within a single season** (excluding cross-season transitions). A window was then scored only if its start cell was visited in that season's training data, with `Coverage_%` reporting the percentage of intra-season test windows that met this condition.<br>

### Results and Interpretation 

**5-Fold Cross-Validation Summary**

After executing the model, we got the following aggregated results across all 5 folds:

| | <sub>Horizon_Days</sub> | <sub>Markov_MAE_km</sub> | <sub>Persistence_MAE_km</sub> | <sub>Skill_vs_Persistence_%</sub> | <sub>Coverage_%</sub> |
| :---: | :---: | :---: | :---: | :---: | :---: |
| <sub>1</sub> | <sub>3.0</sub> | <sub>52.4435</sub> | <sub>51.0639</sub> | <sub>-2.709%</sub> | <sub>92.597%</sub> |
| <sub>2</sub> | <sub>10.0</sub> | <sub>127.9616</sub> | <sub>131.0672</sub> | <sub>+2.363%</sub> | <sub>92.758%</sub> |
| <sub>3</sub> | <sub>15.0</sub> | <sub>168.0600</sub> | <sub>174.4514</sub> | <sub>+3.659%</sub> | <sub>92.845%</sub> |

**Extended Horizon Profiling**

<p align = "center">
<img width="1389" height="515" alt="m2-1" src="https://github.com/user-attachments/assets/e7e920e1-b8e1-47f4-ac9f-fb52249545f4" />
</p>

Model 2 underperforms the persistence baseline at the 3 day horizon, yielding negative skill value for this horizon over all folds. 
The graph on the right shows skill score for the 3 day horizon for Fold 4 dipping below the red dotted 0 line. 

**Probabilistic Energy Score**

Applying the same probabilistic evaluation metric as in Model 1, we obtain the following:

| <sub>Fold</sub> | <sub>Forecast_Days</sub> | <sub>Mean_Energy_Score_Model</sub> | <sub>Mean_Energy_Score_Persistence</sub> | <sub>Skill_vs_Persistence_%</sub> |
| :---: | :---: | :---: | :---: | :---: |
| <sub>4</sub> | <sub>3.0</sub> | <sub>31.8626</sub> | <sub>37.5358</sub> | <sub>+15.1141%</sub> |
| <sub>4</sub> | <sub>10.0</sub> | <sub>85.2229</sub> | <sub>111.7391</sub> | <sub>+23.7304%</sub> |
| <sub>4</sub> | <sub>15.0</sub> | <sub>108.4731</sub> | <sub>143.7212</sub> | <sub>+24.5253%</sub> |

The results show that capturing seasonal dynamics indeed improves ensemble spread over our stationary baseline.

**Spatial Case Studies**

Finally, we generated a seasonal marine debris dispersion forecast using fold 4 seasonal matrices from a single origin cell at 28°N, 55°W and got the following results:

| |
| :---: |
| <img width="1550" height="637" alt="m2-2" src="https://github.com/user-attachments/assets/cb2725e4-db50-45c8-8fff-313a53da58a8" /> |
| <img width="1550" height="637" alt="m2-3" src="https://github.com/user-attachments/assets/4d9cdd4e-9615-450f-87f0-b8c8c56ae6c9" /> |
| <img width="1554" height="637" alt="m2-4" src="https://github.com/user-attachments/assets/f4c68279-c88c-48b9-846f-c4e273bc7e7c" /> |
| <img width="1550" height="637" alt="m2-5" src="https://github.com/user-attachments/assets/7b852e93-dd02-4a5c-bacc-bdfbb2663633" /> |

In Fold 4, no actual held-out drifter endpoints are captured in Q2, while Q1, Q3, and Q4 record only 1, 3, and 2 actual endpoints respectively. This highlights a key trade-off of Model 2: partitioning the dataset into four seasons reduces observation density within each quarter and excludes trajectories that cross seasonal boundaries, resulting in fewer observed validation endpoints in the dispersion plots.

## Model 3 (`Model_3.ipynb`)

### Multivariate Linear Regression with Bivariate Normal Dispersion 

For the third model, we took a very different approach. We built a continuous-space trajectory forecasting model predicting the total west-east ($\Delta x_{\text{lag1}}$) and south-north ($\Delta y_{\text{lag1}}$) displacements over specific forecast horizons using OLS.

**Feature selection & Model Evolution**

Initially, we had used the drifter's starting coordinates (`lat`, `lon`) as the only features of our model. It was a design choice made so that the model served as a simple baseline for our markov models. However, as physical drifters carry substantial short-term momentum, especially over short horizons, we experimented with adding one-step (6 hrs) lagged displacements representing the west-east and south-north distance traveled in the 6 hours immediately prior to forecast time to both regressions. With lag incorporated, Model 3 evolved from a simple baseline to a standalone model.<br>
Unlike prior memoryless grid-transition approaches, this model leverages short-term kinematics of the ocean to predict where marine debris end up.

**How the model works**

  - **5-fold cross validation:** For a rigorous analysis, a 5-fold cross validation with 80%/20% drifter-level split was made per fold (assigning ~780 unseen drifters to each test fold).<br>
  - **Forecast window data extraction:**  Using `prepare_frame` and `make_window_table`, we verified and extracted consecutive 6-hour observations to get continuous trajectory segments, computing true west-east and south-north displacements alongside 6-hour lagged displacements.<br>
  - **Horizon specific OLS and residual covariance estimation:** In `fit_linear` and `fit_cv`, we fitted separate bivariate Ordinary Least Squares (OLS) regressions directly for 3, 10 and 15 day horizons across all 5 folds (extended horizons up to 30 days on Fold 4), alongside 22 residual `covariance matrix ()` to capture directional spread and error correlation.<br>
  - **Point forecast evaluation & multi-horizon error curves:** In `evaluate_cv_forecasts`, predicted displacements are converted back to end coordinates (`end_position`) on held-out test drifters, measuring haversine MAE (`hav`) and percentage skill score against persistence baseline. We also generated a 5-fold CV error curve across 16 horizons from 6 hours (0.25 days) to 90 days. <br>
  - **Probabilistic Energy Score:** In `cloud_eval_fold` and `evaluate_best_fold_energy_score`, we modelled the OLS residuals as a bivariate normal distribution, transforming the deterministic regression into a probabilistic dispersion model capable of simulating spatial uncertainty clouds around predicted drift paths.<br>
On the best-performing fold (Fold 4), we draw 200 Monte Carlo error samples across 20,000 seasonally stratified unseen test windows over 3, 10, 15 day horizons evaluating resulting distribution with energy score, centroid error, cloud spread and central 50%/90% containment. We compared performance of the model with an intercept-only model and persistence baseline.<br>
  - **Case study dispersion forecasts:** In `forecast_garbage_patch_fate_linear`, we simulate 1,000 particles on Fold 4 over 3, 10, 15 day horizons onto the 0.1° × 0.1° spatial grid using `to_state`  across the same five high-impact marine zones.

**Results and Interpretation**

**Results of the Linear Model**

| | <sub>Horizon_Days</sub> | <sub>Markov_MAE_km</sub> | <sub>Persistence_MAE_km</sub> | <sub>Skill_vs_Persistence_%</sub> |
| :---: | :---: | :---: | :---: | :---: |
| <sub>1</sub> | <sub>3.0</sub> | <sub>38.3632</sub> | <sub>50.4702</sub> | <sub>+23.989%</sub> |
| <sub>2</sub> | <sub>10.0</sub> | <sub>113.7357</sub> | <sub>130.2284</sub> | <sub>+12.662%</sub> |
| <sub>3</sub> | <sub>15.0</sub> | <sub>154.3948</sub> | <sub>173.8517</sub> | <sub>+11.188%</sub> |

<p align = "center">
<img width="2048" height="760" alt="m3-1" src="https://github.com/user-attachments/assets/a39525e5-f2c5-491f-8499-0747945c70d4" />
</p>

| |
| :---: |
| <img width="2048" height="535" alt="m3-2" src="https://github.com/user-attachments/assets/76ca1672-f1d6-4867-abcf-629caf37387c" /> |
| <img width="2048" height="555" alt="m3-3" src="https://github.com/user-attachments/assets/a00990c7-0551-494a-a695-caa979cc5a59" /> |
| <img width="2048" height="544" alt="m3-4" src="https://github.com/user-attachments/assets/d46530d1-a26a-4670-ba74-ddcd13dbd008" /> |
| <img width="2048" height="548" alt="m3-5" src="https://github.com/user-attachments/assets/84a36259-cd9a-47df-9c81-a805693d8e51" /> |
| <img width="2048" height="536" alt="m3-6" src="https://github.com/user-attachments/assets/c07fc526-bc86-4053-bae5-4b19d8adcd78" /> |

<p align = "center">
<img width="2026" height="1174" alt="m3-7" src="https://github.com/user-attachments/assets/9b509425-a1bb-4e50-aa89-8dd74123c20d" />
</p>

**Execution**

To execute the model, open `Model_2.ipnyb` from the repository and run all cells sequentially. It automatically installs the required dependencies, loads the 6-hourly drifter dataset and reproduces all the above results and dispersion plots.

## 9. Discussion of Results

Comparing all three models against persistence highlights a clear tradeoff between data density, spatial grid structure and short-term momentum.

**Model 1 vs Model 2**

Overall, Model 1 consistently outperformed Model 2 across both MAE and Energy Score in terms of skill score.
When comparing Model 1 to the persistence baseline, MAE increases over time for both as expected, but the gap between Model 1 and persistence widens as the time-horizon increases - highlighting Model 1’s potential for short-term forecasting.<br>
The model does best when analysing the probabilistic skill, rather than a point prediction, demonstrating suitability for probabilistic forecasting over short-horizons.<br>
<br>
Despite prior research indicating that seasonality influences the movement of drifters, Model 2 consistently performed worse than Model 1 and yielded negative point-forecast skills scores. We hypothesized two primary reasons:
  - **Data Sparsity:** When splitting the data across four quarters, the amount of data used for training each Markov chain matrix was significantly smaller than the single Model 1 matrix, leaving several ocean regions with sparse or no data for training producing erroneous and noisy estimates. <br>
  - **Seasonal boundary:** Test drifters crossing seasonal boundaries within forecast horizon were excluded from evaluation, which negatively impacted validation.

**Model 3 vs Markov Models**

Model 3 achieved lower MAE and higher skill at 3 days than Model 1 because its 6-hour lagged displacements capture short-term momentum. However, an important thing to note is that, its skill steadily declined as horizon increased. It was hypothesised that this was observed as initial momentum faded and plain global linear regressions could not capture the bends around individual curved basin currents. Consequently, Model 1’s skill rose as local transitions accumulated and captured long-term variations.<br>
<br>
The time series lag in Model 3 gave it more information to work with when predicting drifter movement, however Model 1 and 2 were memoryless, meaning comparing the linear model as a baseline to our final products was not valid. Model 3 is therefore best treated as a short-horizon standalone model rather than a direct baseline the way we had intended it to be, leaving persistence to be our common benchmark.

## 10. Conclusion

Through our research, it is found that drifters are an appropriate proxy for marine debris as academics have previously used them to identify garbage patches in the ocean (van Sebille et al., 2012) (Shirah & Mitchell, 2015). 

Ocean cells do form geographically meaningful clusters based on characteristics measured by drifter observation, such as temperature and velocity. Though clusters reflected known North Atlantic ocean current circulations such as the Gulf Stream and North Equatorial current, these clusters were geographically large, meaning that they were not as useful for the purposes of precise short term forecasting.

Forecasting drifter movements saw modest success. Model 1 saw small improvements in skill score as forecast horizons increased, but even after 15 days, the MAE was only 7.1% better than persistence. This meant that the model was just slightly better than simply predicting that a drifter would not move at all. When evaluated using Energy Score, Model 1 was more promising, with a ~26% skill over persistence on Fold 4, reflecting the Markov Chain’s value as a probabilistic model that is able to produce forecast clouds that can account for the uncertainties of ocean currents.

In terms of skill score, Model 1 was better than Model 2 in both MAE and Energy Score, contrary to initial expectations that adjusting the matrix for each season could produce more accurate forecasts. Both however, reflect a pattern of the skill score growing with the time horizon, indicating that for further time horizons, Model 1 and Model 2 would be substantially better than persistence. 

As for Model 3, it was found that lagged displacements can include useful information for short-term forecasting, but that using this model as a baseline would be an unfair comparison for Models 1 and 2. 

## 11. Scope and Limitations

1. Since data about the ocean will be collected from drifters, not all cells are guaranteed to have drifter data, especially after filtering for incomplete data. It may be substituted with other data, such as meteorological data, but finding a proper format and combining it with the drifter data may be technically challenging.
2. Due to computation limitations, the six hourly dataset was used instead of a higher frequency. This study relies on this aggregated dataset to be a good approximation of ocean conditions at the measured time.
   <ol type="a">
     <li>Computation heavy when increasing the number of days to forecast / predict.</li>
   </ol>
   <ol type="b">
     <li>A 1-hour execution time for model 1 and 3-hours for model 2.</li>
   </ol>
3. This study relies on this aggregated dataset to be a good approximation of ocean conditions at the measured time.
4. A key assumption of this project is that drifters are a good proxy for plastic waste. Whilst drifters have been used as a proxy for plastic waste in prior research, they establish that not all plastic waste behaves the same. Nevertheless, they mention that drouged and undrouged drifters are useful for modelling different types of plastics (England et al, 2012).
5. Given the time constraint that the team had, we could not implement lag-based Markov matrix evaluation as it was too complex, given our current understanding.
6. The team had limited domain expertise with regards to oceanography. A bulk of our time was used researching past studies and figuring out further steps in our analysis.


## 12. Future Work
1. **Conduct research on proper implementation of seasonality:** Given that seasons affect ocean behavior, with enough time, we could refine our implementation of Model 2 to model seasonal behaviour more effectively.
2. **Investigate implementing a lag factor for the Markov chain models:** This would allow a fair comparison between the linear model and the Markov chain models, as well as potentially improving Markov chain model performance.


## 13. AI Usage Statement & Reflection

AI was used for a variety of tasks throughout this project, helping save time and quickly build knowledge of the field of oceanography. However, it also created new tasks, such as verifying that AI code worked correctly and that AI suggestions had backing from reputable sources. <br>

AI’s most important usage was creating the project’s code. The usage of AI meant that code was generally functional and flexible, reducing the time needed for producing code. However, code still needed to be verified to ensure it worked in the desired manner. The code was not always perfect and needed some adjustment. <br>

AI was also used as a starting point for researching the field of oceanography. It assisted in finding research papers and in explaining Markov Chain models so that the entire group had knowledge of the project's technical aspects. This was extremely useful for the group to build an understanding of oceanography. <br>

Though with that said, AI suggestions were particularly useful, helping provide the needed information to make important choices for this project. This included suggestions for the specification for Model 3, providing its rationale which was generally satisfactory. AI was also helpful in generating forecast clouds using a linear model, which relied on mathematics outside of what the group had learned thus far. The forecast cloud was generated successfully but the mathematics behind it was not fully understood. <br>

It also suggested a wide variety of metrics for evaluating probabilistic forecast models, from which we chose to present the Energy Score. It was particularly useful in explaining how these metrics were mathematically calculated, helping to make an informed decision about model evaluation choices. AI was also used in other minor tasks such as editing and spellcheck. <br>

Overall, AI was very useful in this project and was found to be very capable of the tasks given to it. But given that AI can still make mistakes, it was important to check its work and not to treat it as a definitive source of information, keeping final decision making power in the hands of the group. <br>

### References

1. Costello, C., Cao, L., Gelcich, S., Cisneros-Mata, M. Á., Free, C. M., Froehlich, H. E., Golden, C. D., Ishimura, G., Maier, J., Macadam-Somer, I., Mangin, T., Melnychuk, M. C., Miyahara, M., de Moor, C. L., Naylor, R., Nøstbakken, L., Ojea, E., O’Reilly, E., Parma, A. M., … Lubchenco, J. (2020). The future of food from the sea. Nature, 588(7836), 95–100. https://doi.org/10.1038/s41586-020-2616-y<br>
2. Furner, Haynes, Jones, Munday, Paige & Shuckburgh (2025). The Challenge of land in a Neural Network Ocean Model, Environmental Data Science https://www.cambridge.org/core/journals/environmental-data-science/article/challenge-of-land-in-a-neural-network-ocean-model/845CF0FEF5898072DA1262564D52B494<br>
3. Lebreton, L. (2018). Evidence that the great pacific garbage patch is rapidly accumulating plastic. Scientific Reports, 8(1). https://doi.org/10.1038/s41598-018-22939-w<br>
4. Lee, D.-K., & Maximenko, N. (2025). Surface drifters and Ocean Dynamics: A review of technological advancements and scientific contributions. Ocean Science Journal, 60(2). https://doi.org/10.1007/s12601-025-00217-x<br>
5. Maximenko, N., Hafner, J., & Niiler, P. (2012). Pathways of marine debris derived from trajectories of Lagrangian drifters. At-Sea Detection of Derelict Fishing Gear, 65(1), 51–62. https://doi.org/10.1016/j.marpolbul.2011.04.016<br>
6. McIlgorm, A., Raubenheimer, K., McIlgorm, D. E., & Nichols, R. (2022). The cost of marine litter damage to the global marine economy: Insights from the Asia-Pacific into prevention and the cost of inaction. Marine Pollution Bulletin, 174(113167), 113167. https://doi.org/10.1016/j.marpolbul.2021.113167<br>
7. NOAA. (2021, February 26). Why should we care about the ocean? NOAA. Noaa.Gov. https://oceanservice.noaa.gov/facts/why-care-about-ocean.html<br>
8. The Ocean Cleanup. (2025). The great pacific garbage patch. The Ocean Cleanup. https://theoceancleanup.com/great-pacific-garbage-patch/<br>
9. Reisser, J., Slat, B., Noble, K., du Plessis, K., Epp, M., Proietti, M., de Sonneville, J., Becker, T., & Pattiaratchi, C. (2015). The vertical distribution of buoyant plastics at sea: An observational study in the north atlantic gyre. Biogeosciences, 12(4), 1249–1256. https://doi.org/10.5194/bg-12-1249-2015<br>
10. Rodríguez-Méndez, V., Ser-Giacomi, E., Ramasco, J. J., López, C., Hernández-García, E. (2026). A Comparative Analysis of Clustering Algorithms for Characterizing Surface Ocean Variability in the Western Mediterranean [Campus Universitat de les Illes Balears]. https://arxiv.org/html/2605.26666v1#bib.bib20<br>
11. Shirah, G., & Mitchell, H. (2015, August 10). Garbage patch visualization experiment. NASA Scientific Visualization Studio. https://svs.gsfc.nasa.gov/4174<br>
12. van Sebille, E., England, M. H., & Froyland, G. (2012). Origin, dynamics and evolution of ocean garbage patches from observed surface drifters. Environmental Research Letters, 7(4), 044040. https://doi.org/10.1088/1748-9326/7/4/044040<br>
13. UNCTAD. (2025, April 23). Shipping data: UNCTAD releases new seaborne trade statistics. UN Trade and Development (UNCTAD). https://unctad.org/news/shipping-data-unctad-releases-new-seaborne-trade-statistics<br>
14. United Nations. (2022). Goal 14: Conserve and sustainably use the oceans, seas and marine resources. United Nations. United Nations Sustainable Development. https://www.un.org/sustainabledevelopment/oceans/<br>
15. World Wildlife Fund. (2019). Our seas: The vital role of coastal and high seas [Educational brochure/science overview]. https://www.wwf.org.uk/sites/default/files/2020-01/Our_Planet_ourseas.pdf<br>
16. World Wildlife Fund. (2025, June 27). Plastic in our oceans is killing marine mammals. Latest Blogs. Wwf.Org.Au. https://wwf.org.au/blogs/plastic-in-our-oceans-is-killing-marine-mammals



