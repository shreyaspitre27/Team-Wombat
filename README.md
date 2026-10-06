# Project Proposal: Modelling Waste Movement in the North Atlantic 

**Group:** Group Wombat

**Members:** Ayantika Jana, Shreyas Siddhartha Pitre, Caleb Khor, Jason Kwok, Kyle Lawther

## Project Overview
One of the most prevalent environmental issues for our oceans is plastic waste. Given the vast size of the ocean and its complex and interconnected system of currents, tracking and cleaning up plastic waste in the oceans is often more difficult than it seems.

Locating ocean garbage patches is highly complex and deceptively difficult. While scientists know where the five major ocean gyres are (Mitchell & Shirah, 2014), finding the actual garbage inside them is not as simple as looking at a satellite photograph. Ocean behaviour is far from uniform: fast currents, swirling eddies and seasonal changes, all move water differently. Debris released close together can end up in very different places depending on which of these regions it enters. This inconsistency makes debris tracking unreliable with uniform assumptions, motivating approaches that utilize modelling regional ocean behaviour. 

Through the use of drifter data, this study aims to classify the ocean into regions, based on currents, temperature and other features. Once these regions are identified, drifter movements will be used to model marine debris movement through these ocean regions. In combination, a better understanding of the features of each ocean region and a predictive model for where the debris moves will optimize its tracking and cleaning in the oceans.

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

## Data/region and data description
**Dataset:** GDP 6-hour Drifter (clouddrift.datasets.gdp6h())
**Region:** North Atlantic Ocean from 10°N 80°W to 45°N 20°W
**Time Period:** 1990-2022
**Key Variables:** Latitude, Longitude, Eastward Velocity, Northbound Velocity, Temperature

|   Data Summary  |     |
| --- | --- |
|  Total observations (Complete Observations)   | 6,124,120 (5,719,745) |
| Number of Drifters | 3,899  |
| Number of Ocean Cells | 194,571 |
| Cell Size   | 0.1° x 0.1° (approximate 11 x 11 km) | 

## Why that problem is important/significant
The vast majority of the ocean's floating debris, including ghost nets, lines, crates, hard plastic bottles, and large debris, is made of low-density polymers. These stay concentrated in the top few meters of the water column and often get broken down into tiny microplastics by the forces of sun and waves.

**Harm to Marine Life:** Entanglement and physical injury to surface-dwelling marine megafauna occur overwhelmingly in this top layer. Animals like fish, sea turtles, and seabirds mistake the tiny plastic pieces for food or become trapped in abandoned fishing nets

**Food Chain Contamination:** Toxins from degraded plastics enter small organisms, moving up the food chain through a process called biomagnification

**Hard to detect and clean:** Because the debris spans vast, remote areas and mostly consists of microscopic particles suspended deep in the water column, it is very difficult and expensive to track and remove. Submerged debris at this shallow depth is a severe hazard to human activity. 

**High Cost in Damage:** Several sectors are affected and this contributes to significantly high cost of damage. The APEC estimate of damage from marine debris to fisheries, aquaculture, marine transport, shipbuilding and marine tourism industries is US$11.2 billion as of 2015 and will reach US$216 billion in 2050 (APEC, 2023).


## Intro/background and existing studies/solutions


## Proposed method


## Initial analysis and visualization


## Timeline and plan
|   Weeks | Phase | Output |
| --- | --- | --- |
|  1-2   | Crafting Research Questions / Project Planning / Understanding Dataset / Researching Existing Projects | Research question to work on  |
| 3-4 | Data Manipulation / Initial Visualisations / Ocean Cell Classification / Proposal & Poster Development / Refining Project Scope & Objectives / Researching Existing Projects | Project Proposal including research questions, visualisation etc. |
| 5-6 | Further improve ocean cell classification through further feature engineering / Begin research, understanding and developing Markov Chain for forecasting| Project Poster | 
| 7-8  | Finalise ocean regions  | Final algorithm used to classify ocean cells |
| 9-10  | Testing algorithm on various regions / Evaluate efficiency / Presentation of results | Final models for plastic waste forecasting / Project Presentation |
| 11-12 | Finalize Research into a report | Final Report | 
## Scope and limitation
1. Since data about the ocean will be collected from drifters, not all cells are guaranteed to have drifter data, especially after filtering for incomplete data. It may be substituted with other data, such as meteorological data, but finding a proper format and combining it with the drifter data may be technically challenging.
2. Due to computation limitations, the six hourly dataset was used instead of a higher frequency. This study relies on this aggregated dataset to be a good approximation of ocean conditions at the measured time.
3. A key assumption of this project and its usefulness is that drifters are a good proxy for plastic waste. Whilst drifters have been used as a proxy for plastic waste in previous studies, they establish that not all plastic waste behaves the same and that drouged and undrouged drifters are more useful for modelling different types of plastics (England et al, 2012). 

## References
1. Lee, D.-K., & Maximenko, N. (2025). Surface drifters and Ocean Dynamics: A review of technological advancements and scientific contributions. Ocean Science Journal, 60(2). https://doi.org/10.1007/s12601-025-00217-x
2. Nikolai, M., Hafner, J., & Niiler, P. (2012). Pathways of marine debris derived from trajectories of Lagrangian drifters. At-Sea Detection of Derelict Fishing Gear, 65(1), 51–62. https://doi.org/10.1016/j.marpolbul.2011.04.016
3. Shirah, G., & Mitchell, H. (2015, August 10). Garbage patch visualization experiment. NASA Scientific Visualization Studio. https://svs.gsfc.nasa.gov/4174
4. van Sebille, E., England, M. H., & Froyland, G. (2012). Origin, dynamics and evolution of ocean garbage patches from observed surface drifters. Environmental Research Letters, 7(4), 044040. https://doi.org/10.1088/1748-9326/7/4/044040

