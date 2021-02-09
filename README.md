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


                                  
