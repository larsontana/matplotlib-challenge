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

mouse_data = pd.read_csv("data/mouse_metadata.csv")
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

# BAR AND PIE CHARTS ------------------------

drug_data = pd.DataFrame(combined_df.groupby(["Drug Regimen"]).count()).reset_index()
drug_data[["Drug Regimen","Mouse ID"]]
drug_df.set_index("Drug Regimen")

# Set the DataFrame index using existing columns. So essentially the numerical representation of an element in the list. 

# Creating bar plot. 

drug_df.plot(kind="bar",figsize =(10,3))

plt.title("Drug Treatment Count")
plt.show()
plt.tight.layout()

# STEP 6: Generate a bar plot using pyplot. 

drug_list = summary_df.index.tolist()
drug_list

# Display all of the drugs. 

drug_count = combined_df.groupby(["Drug Regimen"])["Age Months"].count().tolist()
drug_count

# Set up x axis
x_axis = np.arange(len(drug_count))

x_axis = drug_list

# Customize plot
plt.figure(figsize=(11,4))
plt.title("Drug Treatment Count")
plt.xlabel("Drug Regimen")
plt.ylabel("Count")
plt.bar(x_axis, drug_count, color='b', alpha=0.5, align="center")

plt.clf()
# Clears the figure
plt.cla()
# Clears the current axis
plt.close

# Step 8: Generate the pie plot using pandas

gender_df = pd.DataFrame(combined_df.groupby(["Sex"]).count()).reset.index()
gender_df.head
# Head function returns the first n rows.

# Customize plot.

plt.figure(figsize=(12,6))
ax1 = plt.subplot(121, aspect="equal")
gender_df.plot(kind="pie", y = "Mouse ID", ax=ax1, autopct='%1.1f%%',
              startangle=190, shadow=True, labels=gender_df["Sex"], legend = False, fontsize=14)

plt.title("Male and Female Mice Percentage")
plt.xlabel("")
plt.ylabel("")

plt.clf()
plt.cla()
plt.close()

# Step 9: Generate a pie plot using pyplot 

gender_count = (combined_df.groupby(["Sex"])["Age_months"].count()).tolist()
gender_count

# This counts the number of mails and femails grouped by female and male and counts them by age 

# Adding details to pie chart

labels = ["Females", "Males"]
colors = ["pink", "blue"]
explode = (0.1, 0)

plt.pie(gender_count, explode=explode, labels=labels, colors=colors, autopct="%1.1f%%", shadow=True, startangle=160)
plt.axis("equal")

plt.clf()
plt.cla()
plt.close()

# -------- QUARTILES, IQR, OUTLIERS -------

# Calculate the final tumor volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Calculate the quartiles and IQR and quantitatively determine if there are any potential outliers across all four treatment regimens.

combined_df.head() 

# sort FG intocolumns

sorted_df = combined_df.sort_values(["Drug Regimen", "Mouse ID", "Timepoint"], ascending=True)
last_df = sorted_df.loc[sorted_df["Timepoint"] == 45]
last_df.head().reset_index()

# data for just capomulin
capo_df = last_df[last_df["Drug Regimen"].isin(["Capomulin"])]

# Make tumor volume a DF object

capo_obj = capo_df.sort_values(["Tumor Volume (mm3)"], ascending=True).reset_index()
capo_obj = capo_obj["Tumor Volume (mm3)"]
capo_obj

# Find quartiles in the DF using pandas. 

quartiles = capo_obj.quantile([.25,.5,.75])
lowerq = quartiles[0.25]
upperq = quartiles[0.75]
iqr = upperq - lowerq

print(f"The lower quartile of temperatures is: {lowerq}")
print(f"The upper quartile of temperatures is: {upperq}")
print(f"The interquartile range of temperatures is: {iqr}")
print(f"The median of temperatures is: {quartiles[0.5]}")

lower_bound = lowerq - (1.5*iqr)
upper_bound = upperq + (1.5*iqr)
print(f"Values below {lower_bound} could be outliers.")
print(f"Values above {upper_bound} could be outliers.")
capo_df.head().reset_index() 

# Step 10: Box plot using matplotlib

fig1, ax1 = plt.subplots()
ax1.set_title("Final Tumor Volume in Capomulin Regimen")
ax1.set_ylabel("Final Tumor Volume (mm3)")
ax1.boxplot(capo_obj)
plt.show()

# Repeat for all of the drugs. 

ram_df = last_df[last_df["Drug Regimen"].isin(["Ramicane"])]
ram_df.head().reset_index() 

# Make Tumor Volume a DF object

ram_obj = ram_df.sort_values(["Tumor Volume (mm3)"], ascending=True).reset_index()

# IQR calcs

quartiles = ram_obj.quantile([.25,.5,.75])
lowerq = quartiles[0.25]
upperq = quartiles[0.75]
iqr = upperq - lowerq

print(f"The lower quartile of temperatures is: {lowerq}")
print(f"The upper quartile of temperatures is: {upperq}")
print(f"The interquartile range of temperatures is: {iqr}")
print(f"The median of temperatures is: {quartiles[0.5]}")

lower_bound = lowerq - (1.5*iqr)
upper_bound = upperq + (1.5*iqr)
print(f"Values below {lower_bound} could be outliers.")
print(f"Values above {upper_bound} could be outliers.")
ram_obj = ram_obj["Tumor Volume (mm3)"]
ram_obj

fig1, ax1 = plt.subplots()
ax1.set_title("Final Tumor Volume in Ramicane Regimen")
ax1.set_ylabel("Final Tumor Volume (mm3)")
ax1.boxplot(ram_obj)
plt.show()

# Repeat for Ibunifol

infu_df = last_df[last_df["Drug Regimen"].isin(["Infubinol"])]
infu_df.head().reset_index()

# Make "Tumor Volume" a dataframe object. 

infu_obj = infu_df.sort_values(["Tumor Volume (mm3)"], ascending=True).reset_index()
infu_obj = infu_obj["Tumor Volume (mm3)"]
infu_obj

# Find IQR.

quartiles = infu_obj.quantile([.25,.5,.75])
lowerq = quartiles[0.25]
upperq = quartiles[0.75]
iqr = upperq - lowerq

print(f"The lower quartile of temperatures is: {lowerq}")
print(f"The upper quartile of temperatures is: {upperq}")
print(f"The interquartile range of temperatures is: {iqr}")
print(f"The median of temperatures is: {quartiles[0.5]}")

lower_bound = lowerq - (1.5*iqr)
upper_bound = upperq + (1.5*iqr)
print(f"Values below {lower_bound} could be outliers.")
print(f"Values above {upper_bound} could be outliers.")

# Box plot. 

fig1, ax1 = plt.subplots()
ax1.set_title("Final Tumor Volume in Infubinol Regimen")
ax1.set_ylabel("Final Tumor Volume (mm3)")
ax1.boxplot(infu_obj)
plt.show()

# Repeat for Ceftamin, reset index. 

ceft_df = last_df[last_df["Drug Regimen"].isin(["Ceftamin"])]
ceft_df.head().reset_index()

# Make column "Tumor Volume" a dataframe object

ceft_obj = ceft_df.sort_values(["Tumor Volume (mm3)"], ascending=True).reset_index()
ceft_obj = ceft_obj["Tumor Volume (mm3)"]

# Find IQR data. 

quartiles = ceft_obj.quantile([.25,.5,.75])
lowerq = quartiles[0.25]
upperq = quartiles[0.75]
iqr = upperq - lowerq

print(f"The lower quartile of temperatures is: {lowerq}")
print(f"The upper quartile of temperatures is: {upperq}")
print(f"The interquartile range of temperatures is: {iqr}")
print(f"The median of temperatures is: {quartiles[0.5]}")

lower_bound = lowerq - (1.5*iqr)
upper_bound = upperq + (1.5*iqr)
print(f"Values below {lower_bound} could be outliers.")
print(f"Values above {upper_bound} could be outliers.")
ceft_obj

fig1, ax1 = plt.subplots()
ax1.set_title("Final Tumor Volume in Ceftamin Regimen")
ax1.set_ylabel("Final Tumor Volume (mm3)")
ax1.boxplot(ceft_obj)
plt.show()

# Select a mouse that was treated with Capomulin and generate a line plot of tumor volume vs. time point for that mouse.

capomulin_df = combined_df.loc[combined_df["Drug Regimen"] == "Capomulin"]
capomulin_df = capomulin_df.reset_index()
capomulin_df.head()

# Grab data from one mouse
capo_mouse = capomulin_df.loc[capomulin_df["Mouse ID"] == "s185"]
capo_mouse

# Arrange data into two columns
capo_mouse = capo_mouse.loc[:, ["Timepoint", "Tumor Volume (mm3)"]]
# Now reset the index and generate a line plot showing the tumor volume for mice treated with Capomulin
capo_mouse = capo_mouse.reset_index(drop=True)
capo_mouse.set_index("Timepoint").plot(figsize=(10,8), linewidth=2.5, color="red")

# Generate a scatter plot of mouse weight versus average tumor volume for the Capomulin regimen
capomulin_df.head()

# Arrange data into 3 columns
weight_df = capomulin_df.loc[:, ["Mouse ID", "Weight (g)", "Tumor Volume (mm3)"]]
weight_df.head()

# Get the average tumor volume for each mouse under the use of Capomulin
avg_capo = pd.DataFrame(weight_df.groupby(["Mouse ID", "Weight (g)"])["Tumor Volume (mm3)"].mean()).reset_index()
avg_capo.head()

# Rename "Tumor Volume (mm3)" column to "Average Volume"
avg_capo = avg_capo.rename(columns={"Tumor Volume (mm3)": "Average Volume"})
avg_capo.head()

# Create the scatter plot of mouse wight compared to the average tumor volume for Capomulin

avg_capo.plot(kind="scatter", x="Weight (g)", y="Average Volume", grid=True, figsize=(4,4), title="Weight vs. Average Tumor Volume")
plt.show()

plt.clf()
plt.cla()
plt.close()

# Calculate the correlation coefficient and linear regression model for mouse weight and average tumor volume for the Capomulin regimen
mouse_weight = avg_capo.iloc[:,0]
avg_tumor_volume = avg_capo.iloc[:,1]
# Compute the Pearson correlation coefficient between "Mouse Weight" and "Average Tumor Volume"
correlation = st.pearsonr(mouse_weight,avg_tumor_volume)
print(f"The correlation between both factors is {round(correlation[0],2)}")

# import linregress
from scipy.stats import linregress

# Add the lineear regression equation and line to the scatter plot
x_values = avg_capo["Weight (g)"]
y_values = avg_capo["Average Volume"]
(slope, intercept, rvalue, pvalue, stderr) = linregress(x_values, y_values)
regress_values = x_values * slope + intercept
line_eq = "y = " + str(round(slope,2)) + "x + " + str(round(intercept,2))
plt.scatter(x_values, y_values)
plt.plot(x_values,regress_values,"r-")
plt.annotate(line_eq,(6,10),fontsize=15,color="red")
plt.xlabel("Mouse Weight")
plt.ylabel("Average Tumor Volume")
plt.show()
