# Project Proposal: Modelling Waste Movement and Ocean Behaviour in the North Atlantic

**Group Wombat**

**Members:** Ayantika Jana, Shreyas Siddhartha Pitre, Caleb Khor, Jason Kwok, Kyle Lawther

## Project Overview
One of the most prevalent environmental issues for our oceans is marine waste. Given the vast size of the ocean and its complex and interconnected system of currents, tracking and cleaning up waste in the oceans is often more difficult than it appears.

Locating ocean garbage patches is highly complex and deceptively difficult. While scientists know where the five major ocean gyres are (Mitchell & Shirah, 2014), finding the actual garbage inside them is not as simple as looking at a satellite photograph. Ocean behaviour is far from uniform: fast currents, swirling eddies and seasonal changes, all move water differently. Debris released close together can end up in very different places depending on the ocean behaviour it encounters. This inconsistency makes debris tracking unreliable with uniform assumptions, motivating approaches that utilize modelling regional ocean behaviour. 

For this study, the study area will be divided into cells. A transition matrix will be used to calculate the distribution of movements of drifters between cells. Then, through clustering the ocean cells based on current velocities, temperature and other features, ocean regions will be identified. In combination, a better understanding of the characteristics of each ocean region and a predictive model for where the debris ends up will optimize its tracking and cleaning in the oceans. 


## Research questions and objectives

|     | Questions |
| --- | --- |
| Question 1 | Are drifters a good proxy for ocean rubbish?  |
| Question 2 | Do ocean cells form clusters based on characteristics measured by drifters?  |
| Question 3 | Can we forecast which ocean clusters drifters end up in? | 

|     | Objectives |
| --- | --- |
| Objective 1 | Classify the ocean cells in the North Atlantic into distinct regions based on their features, providing local researchers, authorities and organisations a better understanding of the ocean |
| Objective 2 | Create visualisations for where plastic waste forecast based upon aforementioned regions to provide authorities and organisations with the best information on where cleanup is needed  |

## Background and Significance
**Significance**

The vast majority of the ocean's floating debris, including ghost nets, lines, crates, hard plastic bottles, and large debris, is made of low-density polymers. These stay concentrated in the top few meters of the water column and often get broken down into tiny microplastics by the forces of sun and waves, causing great harm to marine life due to confusion of garbage for food.
Garbage patches in the ocean are large and filled with microplastics that are hard to track and remove, and thus can create high costs in damage, especially to marine architecture, where the expected costs in marine damages is expected to reach $434 billion globally between 2020 and 2050 if plastic production continues to grow (McIlgorm, 2022).

**Past and Opportunities**

There are studies that focus on the accumulation of garbage and prove the location of several garbage patches across the Earth’s surface, including the Great Pacific Garbage Patch, which is the largest accumulation of plastic in the world. This includes research of drifters and their ability to track garbage accumulation by also analysing ocean behaviour through the GDP data (Lee et al., 2025).
Previous research into garbage accumulation mainly visualise the projection of garbage using current GDP data. We aim to create a final product that can predict where garbage will end up by extrapolating from the data, which is a prime opportunity for clear and certain paths to garbage patches for future clean up.


## Data/region and data description
**Dataset:** GDP 6-hour Drifter (clouddrift.datasets.gdp6h()) <br>
**Region:** North Atlantic Ocean from 10°N 80°W to 45°N 20°W <br>
**Time Period:** 1990-2022 <br>
**Key Variables:** Latitude, Longitude, Eastward Velocity, Northbound Velocity, Temperature <br>

|   Data Summary  |     |
| --- | --- |
|  Total observations (Complete Observations)   | 6,124,120 (5,719,745) |
| Number of Drifters | 3,899  |
| Number of Ocean Cells | 194,571 |
| Cell Size   | 0.1° x 0.1° (approximate 11 x 11 km) | 

We wanted to look at a significant region in regards to economic and political significance, thus the Atlantic Ocean region felt important enough to analyse with regards to importance to marine life, shipping routes, and the overall large size of the ocean. The product we wanted to make would require a large amount of data in order to predict where a drifter may go over a period of time, thus we decided on a long time period of around 30 years in order to make a well informed model that could work with other R. 

## Initial analysis and visualization

We conducted an initial analysis of the dataset as a whole, and specific to our region as well. Since we are working with a time series dataset, it was important to understand the distribution of data over time intervals.

**Velocity and Sea Surface Temperature** 
To identify ocean clusters, we analyzed the distribution of velocities and SST over our region, and found a resultant maximum net speed of 0.54 m/s, along with the SST ranging from 12.85°C to 28.55°C

In the velocity heat map on the left, the Gulf Stream stands out immediately off the North American coast. The Caribbean also has some faster moving waters. Whilst the central North Atlantic seems quiet, there are streaks of gradually moving currents throughout.
As expected, sea surface temperature generally cools towards higher latitudes. Notable features include the Gulf Steam, which is warmer than its surrounding regions,and the sudden transition to cool waters, represented by dark blue, near New England and Atlantic Canada.The Caribbean is also warmer than other areas at the same latitudes.

**Ocean Clustering**

After running GMM clustering on sea surface temperature and ocean velocity, we identified five clusters having noisy boundaries, along with their profiles. Well known features like the Gulf Stream and the North Atlantic Drift easily stand out.



## Proposed Method
|   |   |
| --- | --- |
| Data Cleaning | Filtering drifter data in relation to our R. Creating a new dataframe that includes only the variables that we are using, and analyzing the data. Dividing the ocean into grids for visual analysis and a basis for future drifter modelling |
| Analysis/Model | Lagrangian/Eulerian models using the Markov Chain as a probabilistic model, to model drifter transitions and forecast its location |
| Evaluation | Markov Property Test / Goodness of fit (RMSE) |
| Final Product | A probabilistic model that allows users to input for any region of interest to determine the probability of where drifters would end up as a proxy to where garbage ends up, along with the cluster it ends up to ease clean up operations |


## Expected Final Results 

Using drifters as a proxy for marine debris, our research aims to predict the location where marine debris would end up at a given time through drifter movements. Along with this, since clean up methods differ based on ocean behaviour, we aim to classify the ocean into clusters based on physical characteristics, and subsequently predict which clusters the debris would end up to indicate the behaviour in those specific clusters which would also help determine the most safe and efficient way for cleaning operations.


## Scope and limitation

1. Since data about the ocean will be collected from drifters, not all cells are guaranteed to have drifter data, especially after filtering for incomplete data. It may be substituted with other data, such as meteorological data, but finding a proper format and combining it with the drifter data may be technically challenging.
2. Due to computation limitations, the six hourly dataset was used instead of a higher frequency. This study relies on this aggregated dataset to be a good approximation of ocean conditions at the measured time.
3. A key assumption of this project and its usefulness is that drifters are a good proxy for plastic waste. Whilst drifters have been used as a proxy for plastic waste in previous studies, they establish that not all plastic waste behaves the same and that drouged and undrouged drifters are more useful for modelling different types of plastics (England et al, 2012). 

## Timeline and plan
|   Weeks | Phase | Output |
| --- | --- | --- |
|  1-2   | Crafting Research Questions / Project Planning / Understanding Dataset / Researching Existing Projects | Research question to work on  |
| 3-4 | Data Manipulation / Initial Visualisations / Proposal & Poster Development / Refining Project Scope & Objectives / Researching Existing Projects | Project Proposal including research questions, visualisation etc. |
| 5-6 | Further improve ocean classification through further feature engineering / Begin research, understanding and developing model for forecasting | Project Poster | 
| 7-8  | Finalise region grids / implementing Lagrangian/Eulerian models using the Markov Chain  | Final algorithm used to classify ocean cells |
| 9-10  | Testing algorithm on various regions / Evaluate efficiency / Presentation of results | Final models for plastic waste forecasting / Project Presentation |
| 11-12 | Finalize Research into a report | Final Report | 

## References

1. Lee, D.-K., & Maximenko, N. (2025). Surface drifters and Ocean Dynamics: A review of technological advancements and scientific contributions. Ocean Science Journal, 60(2). https://doi.org/10.1007/s12601-025-00217-x
2. McIlgorm, A., Raubenheimer, K., McIlgorm, D. E., Nichols, R. (2022). The cost of marine litter damage to the global marine economy. International Knowledge Hub Against Plastic Pollution. https://ikhapp.org/stories-and-research-brief/the-cost-of-marine-litter-damage-to-the-global-marine-economy/
3. Nikolai, M., Hafner, J., & Niiler, P. (2012). Pathways of marine debris derived from trajectories of Lagrangian drifters. At-Sea Detection of Derelict Fishing Gear, 65(1), 51–62. https://doi.org/10.1016/j.marpolbul.2011.04.016
4. Shirah, G., & Mitchell, H. (2015, August 10). Garbage patch visualization experiment. NASA Scientific Visualization Studio. https://svs.gsfc.nasa.gov/4174
5. van Sebille, E., England, M. H., & Froyland, G. (2012). Origin, dynamics and evolution of ocean garbage patches from observed surface drifters. Environmental Research Letters, 7(4), 044040. https://doi.org/10.1088/1748-9326/7/4/044040

