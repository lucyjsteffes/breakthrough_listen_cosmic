# breakthrough_listen_cosmic
This is the respository for all of my code while an intern at Breakthrough Listen at the Berkeley SETI Research Center. I've never made a repository before so it may take a little while for things to be as up and running as I would like. 

## Overview
This repository has all of the code for one of the projects that I am working on during the summer of 2023. This project was to create a data analysis pipeline to quickly analyze data from COSMIC (the Commensal Open-Source Multi-mode Interferometric Cluster), a new digital backend to conduct SETI using the Karl G. Jansky Very Large Array (VLA). This pipeline, called ARTISTIC (the Anomaly, RFI, and Technosignature Identification Search and Tabularization In COSMIC pipeline) inputs two files and returns a table of potentially interesting sources to examine the stamps files for. In future iterations of this pipeline, the goal would be to make this pipeline more compatible with the future upgrades of COSMIC. As COMIC begins to conduct more commensal observations with more beams, this pipeline will be edited to accomodate these changes. Additionally, my goal is to eventually have this pipeline be able to comb through previous COSMIC observations as a way of checking drift rates and the similarity of hits. 

## Packages
I used the following packages and versions throughout the entire pipeline:
- Pandas (1.3.5)
- Numpy (1.20.3)
- Matplotlib (3.2.1)
- Pickle (0.7.5)
- Seaborn (0.12.2)
- TQDM (4.64.0)
- Astropy (4.0.1.post1)
- CSV (0.14.3)

## Input Files
The first file that is needed to run this pipeline is a .json file of hits from COSMIC. This is created using [seticore](https://github.com/lacker/seticore/tree/master) and gives all of the hits that were flagged to potentially be interesting. The .json file that was used to design ARTISTIC was from 6 hours of commensal observations with the third epoch of VLASS (the Very Large Array Sky Survey) taken in early March, 2023. From this observation period, seitcore identified nearly 5.7 million hits, nearly all of which are very likely false positives. The goal of this pipeline is to identify criteria the define RFI (Radio Frequency Interference) to search for anomalies within the hits for follow-up observations and visual inspection using seticore and the .stamps files.

The second file is the frequency bins with high excess kurtosis in the time-averaged spectra. This portion of the ARTISTIC Pipeline was designed by Jared Sofair, and is accomplished using the [CRICKETS](https://github.com/jareds-laf/CRICKETS) package. The channels that are flagged with having a high excess kurtosis are very high in time-persistent RFI. Even if there were an interesting signal occurring at a frequency within one of these frequency bins, it would be completely drowned out by the much closer sources of RFI, such as satellites, WIFI, bluetooth, or other radio communication methods. It would also not be possible to differentiate between a potentially extraterrestrial technosignature and a more local source of RFI within these frequency bins. Due to these reasons, any hits within these bins are removed entirely.

## Order of ARTISTIC Pipeline
The ARTISTIC Pipeline is designed to go through a series of Jupyter Notebooks to yield a shortlist of potentially interesting hits to examine. I will eventually convert this to a more streamlined pipeline, at which point that will be noted in this README.md. In order to access all of the necessary steps in the intended order, the Jupyter Notebooks in this repository should be run in the following order:
- [Anomalies_Function.ipynb](https://github.com/lucyjsteffes/breakthrough_listen_cosmic/blob/main/Anomalies_Function.ipynb)
- [Beam_Splitting.ipynb](https://github.com/lucyjsteffes/breakthrough_listen_cosmic/blob/main/Beam_Splitting.ipynb)
- [Beam_Size_Analysis.ipynb](https://github.com/lucyjsteffes/breakthrough_listen_cosmic/blob/main/Beam_Size_Analysis.ipynb)
- [Comparing_Power_Levels.ipynb](https://github.com/lucyjsteffes/breakthrough_listen_cosmic/blob/main/Comparing_Power_Levels.ipynb)
- [Unique_Source_Analysis.ipynb](https://github.com/lucyjsteffes/breakthrough_listen_cosmic/blob/main/Unique_Source_Analysis.ipynb)

## Excluded Notebooks from Pipeline
There are several Jupyter Notebooks in this repository that are not particularly useful in the greater scheme of the ARTISTIC Pipeline. The following notebooks are used as practice and proof of concept for some of the ideas used in the main pipeline. These two notebooks are as follows:
- [Hits_Practice_new.ipynb](https://github.com/lucyjsteffes/breakthrough_listen_cosmic/blob/main/Hits_Practice_new.ipynb)
- [Frequency_and_Drift_Rates.ipynb](https://github.com/lucyjsteffes/breakthrough_listen_cosmic/blob/main/Frequency_and_Drift_Rates.ipynb)

The first of these notebooks was the first that I wrote for this project. The main purpose was to begin to examine the structure of the data file and determine the best first steps to take to search for anomalies within the data. While there are some interesting figures produced in this notebook to show the different beams within a field of view and the region of the sky that was observed, none of this takes us any closer to uncovering anomalies because there are simply too many hits to see anything interesting.

The second of these notebooks was primarily a proof of concept to be implemented later on in the pipeline. The idea here was to examine the hits that were observed twice during the 6 hours, due to the scanning nature of VLASS. While most of the hits in the .json file, were labeled as having zero drift, due to the low frequency resolution of COSMIC (~8 Hz resolution), these drift rates should be taken with a grain of salt and an eye of skepticism. Therefore, I took all of the hits at the first time stamp and calculated the hypothetical drift rates that would be needed for a hit at the first time stamp to be the same hit as one observed in the second time stamp. This also helped to better confirm non-drifting hits, as the frequency would be exactly the same at the two times. A mask was then applied to only include the pairs of hits with a drift rate less than +/- 100 Hz/s and a power difference of less than 20%.
