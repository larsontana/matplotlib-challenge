# matplotlib-challenge
# First setup dependencies and and libraries. 

# Import libraries. 
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt 

# Load in files. 
file_to_load = "Resources/study.results.csv"
study_results = pd.read_csv(file_to_load)

# Matplotlib is another library that is essentially used for visualizing data. 
# First, clean data in Excel. 

# TASK ONE: Generate a summary statistics table consisting of the mean, median, variance, standard deviation, and SEM of the tumor volume for each drug regimen.

# STEP ONE: Find the mean, median, variance, standard deviation, and SEM of the tumor volume for each regimen. This will be taken from the study results data.

mean_tumor_volume = study_results:["Tumor Volume (mm3)"].mean()
median_tumor_volume = study_results:["Tumor Volume (mm3)"].median()
std_tumor_volume = study_results:["Tumor Volume (mm3)"].std()
# SEM is the STD /sqrt of sample size
sample_size_tumor = study_results:["Tumor Volume (mm3)"].count()
SEM_tumor_volume = std_tumor_volume / sample_size_tumor 

# STEP TWO: Make data frame of the above data. 

tumor_size_summary = pd.DataFrame({"Mean":[mean_tumor_volume], "Median":[median_tumor_volume], "Standard Deviation":[std_tumor_volume], "SEM":[SEM_tumor_volume]})

# STEP THREE: Format with two decimal places. 

tumor_size_summary.style.format({"Mean":"{:,.2f}",
                                  "Median":"${:,.2f}",
                                  "Standard Deviation":"${:,.2f}",
                                  "SEM":"${:,.2f}"})
                                  
                                  
