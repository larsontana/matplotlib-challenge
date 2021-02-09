# matplotlib-challenge

# STEP 1: First setup dependencies and and libraries. 

# Import libraries. 
import pandas as pd
# Pandas is a common library that is used for data analysis and manipulation. 
import numpy as np
# Numpy is a common library used for working with arrays. Arrays being an object that stores multiple items of the same type. 
import matplotlib.pyplot as plt 
# Matplotlib.pyplot is used for data visualization. 
import scipy.stats as sp
# Scipy.stats is used for basic statistical analysis. 
import matplotlib.axes as ax
# matplotlib.axes is used for more visualization. 
from scipy.stats import linregress
# Need this for the linear regression question. 

# STEP 2: Load in files using Pandas. 

mouse_data = pd.read_csv("data/mouse_metadata.csv"
study_results = pd.read_csv("data/study_results.csv")

# STEP 3: Merge together the two data files because the drug regimen needs to be associated with the tumor volume. 
combined_df = pd.merge (mouse_data, study_results, on="Mouse ID")
# The merging function goes pd.merge(file1, file2,on="column name")

# STEP 4: Group by drug regimen, mouse ID, sex, drug regimen and sex, drug regimen and mouse ID. 

drug_group = df.groupby(["Drug Regimen"])
ID_group = df.groupby(["Mouse ID"])
sex_group = df.groupby(["Sex"])
drugsex_group = df.groupby(["Drug Regimen","Sex"])
drugID_group = df.groupby(["Drug Regimen","Mouse ID"])

# STEP 5: Plot the tumor size. 

tumor_summary = pd.DataFrame({
  "Tumor Mean":drug_group['Tumor Volume (mm3)'].mean(),
  "Tumor Median":drug_group['Tumor Volume (mm3)'].median(),
  "Tumor Variance":drug_group['Tumor Volume (mm3)'].var(),
  "Tumor Std Dev":drug_group['Tumor Volume (mm3)'].std(),
  "Tumor SEM":drug_group['Tumor Volume (mm3)'].sem(),
  })
 tumor_summary
 
 # This will display the stats of the tumor summary. 

# STEP 6: Generate a plot using pyplot. 

plt.figure(figsize=(10,6))
drug_count = drug_group['Mouse ID'].count()
# This line is saying count the number of mice that have this drug in them and it's using the drug group that has grouped the drugs already. 
drug_count.plot(kind="bar", label='Observation Count')
# This line plots the bar graph as the count.
plt.ylim(125,250)
plt.ylabel("Number of Observations")
# Y axis. 
plt.title("Number of Observations for Each Drug Regimen")
# Title. 
plt.legend()
# Legend (obeservation count)
plt.show()
# Show graph. 

# STEP 7: Generate a plot using pandas.

# STEP 8: Generate a pie plot for male and female.    

count if male
count if female
set up pie graph labels and what not
