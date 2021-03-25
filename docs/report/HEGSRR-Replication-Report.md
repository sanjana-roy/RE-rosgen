---
layout: page
title: RE- Replication of Rosgen Stream Classification
---


**Replication of**
# A classification of natural rivers

Original study *by* Rosgen, D. L.
*in* *CATENA* 22 (3):169–199. https://linkinghub.elsevier.com/retrieve/pii/0341816294900019.

and Replication by: Kasprak, A., N. Hough-Snee, T. Beechie, N. Bouwes, G. Brierley, R. Camp, K. Fryirs, H. Imaki, M. Jensen, G. O’Brien, D. Rosgen, and J. Wheaton. 2016. The Blurred Line between Form and Process: A Comparison of Stream Channel Classification Frameworks ed. J. A. Jones. *PLOS ONE* 11 (3):e0150293. https://dx.plos.org/10.1371/journal.pone.0150293.

Replication Authors:
Sanjana Roy, Zach Hilgendorf, Joseph Holler, and Peter Kedron.

Replication Materials Available at: [github repository name](github repository link)

Created: `24 March 2021`
Revised: `25 March 2021`

## Introduction

This study attempts to use the Rosgen Stream Classification System (RCS), which is a method classifying streams and rivers based on their form and morphology at a particular moment in time, through replicating findings from the Kasprak et al. (2016) study of the Middle Fork John Day Basin (MFJD), a watershed of high conservation interest within the Columbia River Basin. The Rosgen classification attempts to “provide a consistent and reproducible frame of reference of communication for those working with river systems in a variety of professional disciplines” (Rosgen, 1994). It uses four hierarchical stages of classification under two ‘Levels’. Level 1 utilizes morphological ratios of rivers, such as entrenchment, width/depth, and sinuosity, from variables observed and calculated through site measurements, like bankfull width, bankfull depth, valley width, valley length, channel length, etc. Level 2 utilizes characteristics, such as the slope of the valley and channel material, to further determine classification. There has been an increase in the use of GIS in aiding to classify streams according to their aforementioned characteristics, however, its application has not been standardized. As RCS is “arguably the most commonly used stream classification system in North America and the world,” its replication through GIS modelling would be particularly helpful through applications in river maintenance, flood control, channel and riparian protection and restoration, impact assessment, etc. (Kasprak et al., 2016).

Therefore, this study attempts to create and practice a method of replicability of the Rosgen Classification System using high resolution terrain models to classify sections of streams and rivers, or “reaches.” We attempt to replicate the RCS analysis of Kasprak et al.’s (2016) study, which compared four different classification methods at the MFJD watershed scale.

![Image of Rosgen Classification](Rosgen/Images/Rosgenclass.png)
Figure 1. Level I and II of the Rosgen Classification System

## Data

# CHaMP Data
Kasprak et al. (2016) uses the Columbia Habitat Monitoring Program (CHaMP) data, collected as a result of aquatic-habitat monitoring in the watershed of the Columbia River Basin. This data contains information on reaches, of which details were collected during 2012 and 2013, at wadable, perennial streams selected through random sampling. Each reach includes information on channel bankfull width and depth, gradient, substrate, and sinuosity. Each sampled reach is twenty times as long as the bankfull channel width at each site (120-360 m in length).

We also utilised LiDAR data of the MFJD Watershed collected in 2008, as part of the Camp Creek LIDAR Project.

## Methods

# Kasprak et al. (2016) Analysis
Kasprak et al. (2016) classified 33 CHaMP reaches in the MFJD Basin using Levels I and II of the RCS.
The study used DEMs of grid resolutions 10m and 0.1m, aerial imagery, and ground-based assessments to understand stream morphological characteristics in order to fulfil the Level I classification. Processing was done using the [River Bathymetry Toolkit (RBT)](https://essa.com/explore-essa/tools/river-bathymetry-toolkit-rbt/) and the [CHaMP Topo Toolbar](http://champtools.northarrowresearch.com/), both used with ESRI ArcGIS software. In order to further classify streams at Level II, Kasprak et al. (2016) then used river bed material size identified by the CHaMP survey from the stream reaches.


# Class Analysis
As a class, we were randomly assigned 17 CHaMP points to classify through replication of the Kasprak et al.(2016) methods. I was assigned the Granite Boulder Creek stream (loc_id = 10) to analyse.

![Image of watershed and points](Rosgen/Images/aoi.jpg)

We used GRASS GIS (7.8.5 for MacOS) for the processing of the two layers of data, the CHaMP points and the MFJD Watershed tif file. [A model](https://github.com/sanjana-roy/RE-rosgen/blob/main/procedure/code/visualize.gxm) was used to create buffer zones around the CHaMP survey points, as Rosgen (1994) suggests analyzing a distance of 20 channel widths, applied in the distance settings. The model also uses the LiDAR MFJD image to create a Digital Elevation Model (DEM) with colors and hillshade.

![Image of Model1](Rosgen/Images/visualize_model.png)
![Image of Map Study Site Elevation](Rosgen/Images/map_elevation.png)
![Image of Map Study Site Slope](Rosgen/Images/map_slope2.png)

The stream banks and valley edges were manually digitized with respect to the buffer at a scale of 1:1500. This digitization was done three times for both the banks and valley edges. [A second model](https://github.com/sanjana-roy/RE-rosgen/blob/main/procedure/code/center_line_length_no_clip.gxm) was then used to find the averages of each set of lines as well as the “average of the average,” providing us with a final banks line and valley line.

![Image of Model2](Rosgen/Images/center_line_length_model.png)
![Image of Map Study Site Banks](Rosgen/Images/map_banks.png)
![Image of Map Study Site Valley](Rosgen/Images/map_valley.png)


The longitudinal and cross-sectional profiles of the reach were then extracted using the averaged banks and valley lines. Each profile consisted of a set of points spaced 1 m apart. This data was then exported and visualized in graphs in RStudio (v 1.4.1103 for MacOS) using [this code](https://github.com/sanjana-roy/RE-rosgen/blob/main/procedure/code/2-ProfileViewer.Rmd). Analysis using the R code allows us to determine the Slope of the stream as well as the Valley width (Table 1).

![Image of Cross-Section](Rosgen/Images/figures/CrossSecProf.png)
![Image of Long Prof](Rosgen/Images/figures/LongProf.png)
![Image of LongProf Slope](Rosgen/Images/figures/SlopePer.png)
![Image of Cross-Sec Zoom](Rosgen/Images/figures/ZoomBfDepth.png)


# Differences in Method
1. The computational environments that were used in these two studies were different, possibly introducing many uncertainties in how the analysis was carried out. Kasprak et al. (2016) used RBT and the CHaMP Topo Toolbar with ESRI ArcGIS to process and analyze data, while this study used a combination of GRASS GIS and RStudio.
2. Although we are not aware of whether Kasprak et al. (2016) used LiDAR in their analysis, the DEM files were of a resolution of 0.1m, allowing a finer digitization of stream and valley edges. DEM resolution in this study was 1m.
3. Finally, Kasprak et al. (2016) were able to conduct field observations, which would have largely influenced the accuracy of their digitazation as well as general understanding of the landscape.


# Unplanned Deviations from the Protocol
1.
> Use of no_clip
> MacOS downloading XCode and something else
> Difference in calculating slope in R


## Results

Table 1. Site Measurements
| Variable | Value | Source |
| :-: | :-: | :-: |
| Bankfull Width | 6.1004 | CHaMP data BfWdth_Avg |
| Bankfull Depth Maximum | 1.4275 | CHaMP data DpthBf_Max |
| Bankfull Depth Mean | 0.3212 | CHaMP data DpthBf_Avg |
| Valley Width | 60(m) | Terrain Cross-Section |
| Valley Depth | 2.855 | Bankfull Depth * 2|
| Stream/River Length | 154.46(m) | Mean Stream Centerline from GRASS|
| Valley Length | 167.83(m) | Mean Valley Centerline from GRASS|
| Median Channel Material Particle Diameter | 152 | CHaMP data SubD50 |

Table 2. Rosgen Level I Classification
| Criteria | Value | Formula |
| :-: | :-: |
| Entrenchment Ratio | 9.835 | (Valley Width at Bankfull Depth * 2) / Bankfull Width |
| Width / Depth Ratio | 18.99 | Bankfull Width / Bankfull Depth Mean|
| Sinuosity | 0.920 | Stream Length / Valley Length |
| Level I Stream Type | Either E or C |

Table 3. Rosgen Level II Classification
| Criteria | Value |
| :-: | :-: |
| Slope | 0.086 |
| Channel Material | Gravel |
| Level II Stream Type | Unclear |

## Discussion

## Conclusion

## References




## Original Study Information

Description: Present a short narrative that summarizes key information about the original study. Include information about all of the following
1.	Provide a written description of the study location and extent. Whenever possible, provide specific geographic coordinates bounding the study extent or a spatial reference file.
2.	Identify and describe the spatial support (spatial resolution, unit of analysis) of the original analysis was conducted
3.	What type of sample/data did the original study use?
4.	Are the data and code used in the original analysis available/used in this replication?

## Analytical Plan

Describe all elements of the analytical plan of the original study that are relevant to the research questions and hypotheses being re-examined by the replication. Include information for each of the following sub-sections as appropriate.

### Sampling Plan and Data Description

Include a reference map of the stream reach point you will analyze.

Describe the data used in the original study. If sampling was used, provide details about the sampling design and how it was implemented.
1. Describe how sampled data relevant to the hypotheses being re-examined was collected by the original authors.
   -	For human subjects research, include the population from which subjects were sampled, location of sampling, recruitment details, payments for participation, eligibility criteria (e.g. inclusion and exclusion rules), and sampling timeline.
   -	For research that did not involve human subjects, include information about sample collection, duration of data gathering efforts, source or location of samples
   -	For studies in which sample location is obfuscated, explain the motivation for the obfuscation and identify the type of geographic masking technique that was used.  
2. Describe the spatial sampling design used during data collection
   -	Identify the design of the spatial sample (e.g., stratified random sample)
   -	Identify the size of the sample, and how many observations will be collected in different geographic strata or levels if using a stratified, clustered, or multilevel design.
   -	If a termination rule was used, identify the relevant criteria, original authors’ motivation, and how the rule was implemented.
3. Describe any secondary dataset(s), or sub-set(s) of those datasets, used in the original study.
   -	Explain how the data was acquired by the original authors including – source (with DOI if possible), data of access
   -	If selected datasets or sub-sets cover only portions of the overall study area or study period, clearly identify which datasets are associated with which locations and times.
   -	Explain how the data was acquired by the original authors including – source, data of access
4. Describe if/how the original study excluded or adjusted the initial dataset
   -	Identify any data that was excluded from the original analysis report –reason for exclusion, exclusion criteria, sample size before and after exclusion, location of excluded data (e.g., is exclusion likely to reduce/eliminate coverage in a particular sub-region)
   -	Explain how the original authors addressed missing data and details about any interpolation procedures used by the authors.
   -	Describe any sample weighting that was used in the original study. Separately identify any spatial component used in the weighting scheme.

### Variables

Describe the variables used in the original study to address the research questions and hypotheses that are the focus of the replication.

1. Identify any experimentally manipulated variables and include details about how these variables were manipulated during the original study.
2. Identify any measured variables examined in the original study
   -	Identify both the response(s) and predictor variable(s) associated with each hypothesis
   -	Describe any variable transformations (e.g., log-scaled, categorical)
   -	Describe any spatial aggregation/disaggregation that was applied to any variables
3. Describe any adjustments made to the variables to account for
   -	first-order spatial effects (sub-regional differences in means)
   -	second-order spatial effects (spatial dependencies)
   -	spatial anisotropies (directional trends)

### Analytical Specification

Describe the exact analytical specification that was used to test each hypothesis
1. For computational studies include information about the hardware and software environments of both the original study
2. Identify the coordinate system(s) and projection(s) used during the original analysis
3. Specify if/how edge effects were addressed. Provide details regarding the extent of any buffer or guard areas used.
4. Describe the type of model, the specification of that model, distributional assumptions of the model, and any post-hoc analyses used to test each hypothesis. Key aspects of some common geographical analyses include:
   - If a spatial weighting scheme was used, provide a functional description of that scheme
   - If a spatial model was used, provide detailed description of that model
   - If a classifier was used, provide details about the selection of training data, validation data, and if any independent test data
   - If a spatial multi-level model was used, identify the spatial scale of each level, the variable included at each level, and the levels any spatial structures or cross-scale structure are estimated at.
Inference Criteria, Results, and Robustness: For each separate hypothesis, provide a description of the results of the original study and the relevant inference criteria and robustness checks
1. Describe the specific criteria (e.g., p-values, effect size, model fit) and thresholds that were used to make inferences.
   -	Identify any adjustments made for multiple testing (e.g., Bonferroni, Sidak) and how they were implemented.
2. Describe the result associated with each hypothesis.
   -	Identify the size and direction of the effect, measure of variance of the effect, statistical assessments
3. Describe any robustness checks that were completed to assess the strength and reliability of inferences for each hypothesis. Identify any spatial components varied during robustness checks.

## Materials and Procedure

Describe how the replication study will be implemented and identify any materials and procedures used to complete the replication.
1.	For computational studies include information about the hardware and software environments of both the original study and the replication attempt.

Protocol: Explain how the analysis of the replication will proceed and identify if the analysis plan will match the original study. For many replications this section may be quite short if the procedures used in the original analyses are followed closely. In those cases, this section can simply explain how key elements will be followed.

Differences from the Original Study: Identify any ways in which the replication is planned to depart from the original study -- a) location, b) sampling, c) data, d) measures/variable construction, d) analytical techniques.
1.	Provide the motivation for each change that is made to the original study.
2.	State how the differences identified above may influence the expected size/direction of the effect of the original study
3.	List any testable hypotheses associated with each change. If a hypothesis is directional, state the direction
4.	Outline any initial analyses that were taken to assess whether the differences identified above will influence the outcome of the replication attempt.

Assessment Criteria: Identify the criteria that will define whether the replication attempt was successful (e.g., matched statistical significance, direction of effect, similar magnitude of effect)
- Reproducible documentation of methods, where documentation includes:
- Annotated flowchart of final parameter values (use last page of RSC_EPA_2005 PDF)

## Replication Results

For each hypothesis examined, present separately the results of the replication attempt.
1.	Briefly describe how the replication protocol outlined above was implemented reporting key information (e.g., sample size).
2.	State whether the original hypothesis was or was not supported by the replication
   - Provide key statistics produced by the replication.
   - Provide key measures (e.g., matching effect direction/size, significance) used to make the decision.
   - Highlight any contradictory results with a brief explanation
3.	State whether any hypothesis linked to a planned deviation from the original study was supported. Provide key statistics and related reasoning.

Figures to Include:
- map of the study site shaded elevation
- map of the study site slope
- Map of the study site stream/river centerlines and final mean centerline
- Map of the study site valley centerlines and final mean centerline
- Longitudinal profile graph with elevation and slope
- Cross-sectional profile graph

Tables to Include:

Table 1. Site Measurements
| Variable | Value | Source |
| :-: | :-: | :-: |
| Bankfull Width | | |
| Bankfull Depth | | |
| Valley Width | | |
| Valley Depth | | |
| Stream/River Length | | |
| Valley Length | | |
| Median Channel Material Particle Diameter | | |

Table 2. Rosgen Level I Classification
| Criteria | Value |
| :-: | :-: |
| Entrenchment Ratio | -- |
| Width / Depth Ratio | -- |
| Sinuosity | -- |
| Level I Stream Type | -- |

Table 3. Rosgen Level II Classification
| Criteria | Value |
| :-: | :-: |
| Slope | -- |
| Channel Material | -- |
| Level II Stream Type | -- |


## Unplanned Deviations from the Protocol

Identify and describe any unplanned deviations from the original replication protocol the occurred during the course of the replication. Explain the rationale behind any deviations. Finally, provide the details and results of any sensitivity analyses conducted to assess whether these deviations may have impacted the results of the replication.

## Discussion

Provide a summary and interpretation of the key findings of the replication *vis-a-vis* the original study results. If the attempt was a failure, discuss possible causes of the failure. These may include:
- Practical Causes – related to lack of data, code, details in the original analysis
- Informative Causes – related to absence of effect, change in population, or location.

Discuss an interpretation of your results.
- Were the Level I and Level II results internally and logically consistent? That is, did all the parameters for the identified stream type conform to expectations outlined in Rosgen?
- Were your results consistent with previous evaluations of the same stream reach reported by Kasperak et al?

Discuss a response to the following prompt: Quantifying uncertainty in geomorphic systems and in GIScience is of paramount importance, not only for creating error bars on a graph, but for realistically communicating the reliability and legitimacy of an output dataset. Error bars do not (necessarily) reflect on the researcher. They stem from collection constraints, processing constraints, subjective decision making, and many, many more sources. Given what you have learned in this module, discuss at least three sources of error and uncertainty and how they could impact the classification of your stream. Where does uncertainty stem from? Why is uncertainty a problem? What could be done (or has been done) to fix or reduce uncertainty? In a perfect world, how could this uncertainty be removed?

## Conclusion

Restate the key findings and discuss their broader societal implications or contributions to theory.
Do the research findings suggest a need for any future research?

## References

Include any referenced studies or materials in the [AAG Style of author-date referencing](https://www.tandf.co.uk//journals/authors/style/reference/tf_USChicagoB.pdf).

####  Report Template References & License

This template was developed by Peter Kedron and Joseph Holler with funding support from HEGS-2049837. This template is an adaptation of the ReScience Article Template Developed by N.P Rougier, released under a GPL version 3 license and available here: https://github.com/ReScience/template. Copyright © Nicolas Rougier and coauthors. It also draws inspiration from the pre-registration protocol of the Open Science Framework and the replication studies of Camerer et al. (2016, 2018). See https://osf.io/pfdyw/ and https://osf.io/bzm54/

Camerer, C. F., A. Dreber, E. Forsell, T.-H. Ho, J. Huber, M. Johannesson, M. Kirchler, J. Almenberg, A. Altmejd, T. Chan, E. Heikensten, F. Holzmeister, T. Imai, S. Isaksson, G. Nave, T. Pfeiffer, M. Razen, and H. Wu. 2016. Evaluating replicability of laboratory experiments in economics. Science 351 (6280):1433–1436. https://www.sciencemag.org/lookup/doi/10.1126/science.aaf0918.

Camerer, C. F., A. Dreber, F. Holzmeister, T.-H. Ho, J. Huber, M. Johannesson, M. Kirchler, G. Nave, B. A. Nosek, T. Pfeiffer, A. Altmejd, N. Buttrick, T. Chan, Y. Chen, E. Forsell, A. Gampa, E. Heikensten, L. Hummer, T. Imai, S. Isaksson, D. Manfredi, J. Rose, E.-J. Wagenmakers, and H. Wu. 2018. Evaluating the replicability of social science experiments in Nature and Science between 2010 and 2015. Nature Human Behaviour 2 (9):637–644. http://www.nature.com/articles/s41562-018-0399-z.
