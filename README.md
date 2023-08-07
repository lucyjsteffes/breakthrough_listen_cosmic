# breakthrough_listen_cosmic
This is the respository for all of my code while an intern at Breakthrough Listen at the Berkeley SETI Research Center. I've never made a repository before so it may take a little while for things to be as up and running as I would like. 

This repository has all of the code for one of the projects that I am working on during the summer of 2023. This project was to create a data analysis pipeline to quickly analyze data from COSMIC (the Commensal Open-Source Multi-mode Interferometric Cluster), a new digital backend to conduct SETI using the Karl G. Jansky Very Large Array (VLA). This pipeline, called ARTISTIC (the Anomaly, RFI, and Technosignature Identification Search and Tabularization In COSMIC pipeline) inputs two files and returns a table of potentially interesting sources to examine the stamps files for. In future iterations of this pipeline, the goal would be to make this pipeline more compatible with the future upgrades of COSMIC. As COMIC begins to conduct more commensal observations with more beams, this pipeline will be edited to accomodate these changes. Additionally, my goal is to eventually have this pipeline be able to comb through previous COSMIC observations as a way of checking drift rates and the similarity of hits. 

# Packages
I used the following packages and versions throughout the entire pipeline:
- Pandas (1.3.5)
- Numpy (1.20.3)
- Matplotlib (3.2.1)
- Pickle (0.7.5)
- Seaborn (0.12.2)
- TQDM (4.64.0)
- Astropy (4.0.1.post1)
- CSV (0.14.3)
