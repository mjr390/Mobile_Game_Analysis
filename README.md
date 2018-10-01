
The goal of this project was to use pandas to examine sales and demographic data of an inline gaming company.  The dataset, which is in the Resources folder, contains data about the customers of the company and the items purchased.  Included in this repo is this README contining a short analysis of the findings, the code used, and multiple data frames created from the data, and an ipynb file containg the code that can be run.

What the code does:

- Loads in the csv and converts it to a data frame

- Finds the total number of unique players, and makes a data frame of this information

- Finds the total number if unique items purchased, the average price, number of purchases, and total revenue of the dataset.  This info is converted into a readable data frame

- Creates a data frame breaking down the players by gender and another data frame showing sales info by gender

- Creates a data frame showing the player base by age, and another data frame with purchase statistics by age

- Creates a data frame showing the top 5 spenders

- Creates a data frame showing the most popular items and a data frame showing the most profitable items

Note: This project was originally part of a repo with multiple projects, it has been moved here to viewed on its own. Original location can be found here: https://github.com/mjr390/Pandas_In_Jupyter/tree/master/Heroes_of_Pymoli

# Heroes Of Pymoli Data Analysis
    1. While the vast majority of players are male, their average purchase price per item ($3.02), is lower than average purchase price of all players ($3.05).
    2. The most popular item ("Oathbreaker, Last Hope of the Breaking Storm") is also the most profitable. The second ("Nirvana") and third ("Fiery Glass Crusader") most profitable items are also in the top 4 most popular items.
    3. Lisosia93 has spent the most money on items ($18.96). Followed by Idastidru52 at ($15.45) and Chamjask73 at($13.83).


```python
import pandas as pd
import numpy as np
```


```python
file_to_load = "Resources/purchase_data.csv"
df = pd.read_csv(file_to_load)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



# Player Count


```python
#Calcualte the total number of players
#Use len() on the unque values in "SN" to find the number of unique players, put that value into a dataframe and display it
totPlayers = len(df["SN"].unique())
totPlayersVar = [{"Total Players":totPlayers}]
totPlayersDF = pd.DataFrame(totPlayersVar)
totPlayersDF
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Total)


```python
#Find the total number of of Unique Items, Number of Purchases, Total Revenue, and the Average Purchase Price
#use len() on the unique values in "Item Name" and set that value to a variable
uniItems = len(df["Item Name"].unique())

#use .mean() on the "Price" column to find the average cost per item and set to a varibale
#use round() to round the number to 2 decimal places beacuse the value is a float
#and then create a new variable for the value as a string
avgPrice = df["Price"].mean()
avgPrice = round(avgPrice,2)
avgPriceDis = ("$" + str(avgPrice))
#use .sum() on "Price" column to find the sum of all it's values, use round() bacuse it is a float
#and create a new variable with the value as a string to display
totRev = df["Price"].sum()
totRevDis = ("$" + str(totRev))
totNumOfPur = df["Item ID"].count()
#Create a DataFrame to display the results and order them
Purchasing_Analysis = pd.DataFrame([{"Number of Unique Items":uniItems, "Average Price": avgPriceDis, "Number of Purchases": totNumOfPur
                                   , "Total Revenue":totRevDis}])
Purchasing_Analysis_Ordered = Purchasing_Analysis[["Number of Unique Items", "Average Price", "Number of Purchases", "Total Revenue"]]
Purchasing_Analysis_Ordered
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>$3.05</td>
      <td>780</td>
      <td>$2379.77</td>
    </tr>
  </tbody>
</table>
</div>



# Gender Demographics


```python
# Find the Percentage and Count of Male Players, Percentage and Count of Female Players, and Percentage and Count of Other / Non-Disclosed
#create variables for the total count of each gender to use to find the % they are of the total player base
malePlayerCount = len(df.loc[df["Gender"] == "Male"])
femalePlayerCount = len(df.loc[df["Gender"] == "Female"])
otherPlayerCount = len(df.loc[df["Gender"] == "Other / Non-Disclosed"])
#Use the variables from the lasst step to create variables for each gender's % of the total
malePlayPer = round(malePlayerCount/totPlayers*100,2)
fePlayPer = round(femalePlayerCount/totPlayers*100,2)
othPlayPer = round(otherPlayerCount/totPlayers*100,2)

#use value_counts() to find how many of each gender there are and set to a variable
GenderCounts = df["Gender"].value_counts()
#create a DataFrame for the found values and labels
GenderCounts_df = pd.DataFrame(GenderCounts)
#Add in a new column with the % values found earlier and create a new DataFrame with the columns in a different order for display
GenderCounts_df["Percentage of Players"]=[malePlayPer, fePlayPer, othPlayPer]
GenderCounts_df_ordered = GenderCounts_df[["Percentage of Players", "Gender"]]

GenderCounts_df_ordered
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>113.19</td>
      <td>652</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>19.62</td>
      <td>113</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>2.60</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Gender)


```python
# Find the purchase count, Average Purchase Price, Total Purchase Value, and Normalized Totals by gender

#Run basic calculations to find the needed values
mPurCount = len(df.loc[df["Gender"] == "Male"])
fPurCount = len(df.loc[df["Gender"] == "Female"])
oPurCount = len(df.loc[df["Gender"] == "Other / Non-Disclosed"])

#For each gender's average price, locate the values for each gender and take the mean
#use round() to reduce each to 2 decimal places. create a new variavle to display the value in a DataFrame formatted as a string
mAvgPrice = df["Price"].loc[df["Gender"] == "Male"].mean()
mAvgPrice = round(mAvgPrice,2)
mAvgPrice_display = ("$" + str(mAvgPrice))

fAvgPrice = df["Price"].loc[df["Gender"] == "Female"].mean()
#The Female average ends in a '0' so a different method of formatting must be used
fAvgPrice = "%.2f" % round(fAvgPrice, 2)
fAvgPrice_diaplay = ("$" + str(fAvgPrice))

oAvgPrice = df["Price"].loc[df["Gender"] == "Other / Non-Disclosed"].mean()
oAvgPrice = round(oAvgPrice,2)
oAvgPrice_display = ("$" + str(oAvgPrice))

#Use sum() instead of mean() to find the total Purchase value for each gender and assign to a variable
#Create a new variable to use in the DataFrame
mTotPrice = df["Price"].loc[df["Gender"] == "Male"].sum()
mTotPrice_display = ("$" + str(mTotPrice))

fTotPrice = df["Price"].loc[df["Gender"] == "Female"].sum()
fTotPrice_display = ("$" + str(fTotPrice))

oTotPrice = df["Price"].loc[df["Gender"] == "Other / Non-Disclosed"].sum()
oTotPrice_display = ("$" + str(oTotPrice))

#Find the Normalized totals for each gender by dividing the total price variable by the purchase count
#Round each to 2 decimal places and then create a new variable to display in the DataFrame
mNorTot = mTotPrice/mPurCount
mNorTot = round(mNorTot,2)
mNorTot_display = ("$" + str(mNorTot))

fNorTot = fTotPrice/fPurCount

fNorTot = "%.2f" % round(fNorTot, 2)
fNorTot_display = ("$" + str(fNorTot))

oNorTot = oTotPrice/oPurCount
oNorTot = round(oNorTot,2)
oNorTot_display = ("$" + str(oNorTot))

#Create the DataFrame for the values
PA_Gender_df = pd.DataFrame({
    "Gender" : ["Male", "Female", "Other / Non-Disclosed"],
    "Purchase Count" : [mPurCount, fPurCount, oPurCount],
    "Average Purchase Price" : [mAvgPrice_display, fAvgPrice_diaplay, oAvgPrice_display],
    "Total Purchase Value" : [mTotPrice_display, fTotPrice_display, oTotPrice_display],
    "Normalized Totals" : [mNorTot_display, fNorTot_display, oNorTot_display]
})
#Reorder the DataFrame, Set the index column to the genders, set the index to appear in alphabetical order and display the DataFrame
PA_Gender_df = PA_Gender_df[["Gender", "Purchase Count", "Average Purchase Price", "Total Purchase Value", "Normalized Totals"]]
PA_Gender_df = PA_Gender_df.set_index("Gender")
PA_Gender_df = PA_Gender_df.sort_index(ascending=True)
PA_Gender_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>113</td>
      <td>$3.20</td>
      <td>$361.94</td>
      <td>$3.20</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>$3.02</td>
      <td>$1967.64</td>
      <td>$3.02</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>15</td>
      <td>$3.35</td>
      <td>$50.19</td>
      <td>$3.35</td>
    </tr>
  </tbody>
</table>
</div>



# Age Demographics


```python
#create bins and corresponding labels
age_bins = [0, 9.90, 14.90, 19.90, 24.90, 29.90, 34.90, 39.90, 99999]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]


#create a data frame off of the "Age" column in the data set
new_age_df = pd.DataFrame(df["Age"])

#create a new row with the ages grouped using .cut and the bins and labels
new_age_df["Age Group"] = pd.cut(new_age_df["Age"], age_bins, labels=group_names)

#group the data frame by "Age Group"
new_age_df = new_age_df.groupby("Age Group")

#find how many times an entry appears in a bucket
new_age_df.count()

#turn the found count into a data frame
new_age_df = pd.DataFrame(new_age_df.count())

#rename the columns
new_age_df = new_age_df.rename(columns={"Age":"Total Count"})

#add a new column for the "Percent of PLayers" by dividing the count in each bucket by the total number of players and multiply by 100
#round the result to 2 decimal places
new_age_df["Percent of Players"] = round(new_age_df["Total Count"]/totPlayers*100, 2)

#rearrange the columns
new_age_df = new_age_df[["Percent of Players", "Total Count"]]

#delete the index title
del new_age_df.index.name

#display the results
new_age_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percent of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>3.99</td>
      <td>23</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4.86</td>
      <td>28</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>23.61</td>
      <td>136</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>63.37</td>
      <td>365</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>17.53</td>
      <td>101</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>12.67</td>
      <td>73</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>7.12</td>
      <td>41</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>2.26</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Age)


```python
#create a new variable holding the "Age" and "Price" columns from the data set
paAge_df = df[["Age", "Price"]]
paAge_df.head()


#create bins and corresponding labels
age_bins = [0, 9.90, 14.90, 19.90, 24.90, 29.90, 34.90, 39.90, 99999]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

#add age groups to the data frame useing .cut on the "Age" column and the age_groups and group_names
paAge_df["Age Groups"] = pd.cut(paAge_df["Age"], age_bins, labels=group_names)

#groupby the new column and save to a variable to use later to find the total count of each bin
grouped_paAge = paAge_df.groupby(["Age Groups"])

#use .count() on the created variable to find how many values are in each bin
#save to a variable as a data frame to create a row to be used later
findPurCount = pd.DataFrame(grouped_paAge.count())

#group the data frame by the new column
paAge_df = paAge_df.groupby("Age Groups")

#take the sum of each bin and save to a data frame
paAge_df.sum()
paAge_df2 = pd.DataFrame(paAge_df.sum())

#add a column to the data frame which is the column from the data frame that .count() was used on
paAge_df2["Purchase Count"] = findPurCount["Age"]

#remove the unneeded columns
paAge_df2 = paAge_df2[["Price", "Purchase Count"]]

#rename columns
paAge_df2 = paAge_df2.rename(columns={"Price":"Total Purchase Value"})

#add columns to the data frame for "Average Purchase Price" and "Normalized Totals" doing the calcs for each
paAge_df2["Average Purchase Price"] = round(paAge_df2["Total Purchase Value"]/paAge_df2["Purchase Count"],2)
paAge_df2["Normalized Totals"] = round(paAge_df2["Total Purchase Value"]/paAge_df2["Purchase Count"],2)

#reorganize the columns to make more sense
paAge_df2 = paAge_df2[["Purchase Count", "Average Purchase Price", "Total Purchase Value", "Normalized Totals"]]

#check the data types of the columns for formatting
paAge_df2.dtypes

#Changethe format on the columns that are floats to represent money
pd.options.display.float_format = '${:,.2f}'.format

#Delete the index name
del paAge_df2.index.name

#display the data frame
paAge_df2
```

    C:\Users\Mike\Anaconda3\envs\PythonData\lib\site-packages\ipykernel_launcher.py:11: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      # This is added back by InteractiveShellApp.init_path()





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$3.35</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
      <td>$82.78</td>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$412.89</td>
      <td>$3.04</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$1,114.06</td>
      <td>$3.05</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$293.00</td>
      <td>$2.90</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$214.00</td>
      <td>$2.93</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$147.67</td>
      <td>$3.60</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$38.24</td>
      <td>$2.94</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
#use vlaue counts on the "SN" column to find how many items each player bought and save to a variable
purCount = df["SN"].value_counts()
purCount.head()

#use groupby to seperate the data into fields by SN
findTotPurValue = df.groupby(["SN"])
findTotPurValue.count().head()

#find the sum of price for each SN and save to a variable
totSpendPerValue = findTotPurValue["Price"].sum()

totSpendPerValue.head(10)

#create a new DataFrame with the new variables
Top_Spenders = pd.DataFrame({
    "Purchase Count":purCount,
    "Total Purchase Value": totSpendPerValue
})
Top_Spenders.head(10)

#Add ac column for average price by dividing the values in "Total Purchase Value" by those in "Purchase Count"
#round the findings to 2 decimal places
Top_Spenders["Average Purchase Price"] = round((Top_Spenders["Total Purchase Value"]/Top_Spenders["Purchase Count"]),2)
Top_Spenders.head(10)

#format the columns with floats data into currency format
pd.options.display.float_format = '${:,.2f}'.format
Top_Spenders.head(10)

#Name the index in the DataFrame
Top_Spenders.index.name = "SN"
Top_Spenders.head(10)

#Sort the DataFrame by highest "Total Purchase Value" on top
Top_Spenders_Sorted = Top_Spenders.sort_values("Total Purchase Value", ascending=False)
Top_Spenders_Sorted.head()

#Rearrange the columns
Top_Spenders_Sorted = Top_Spenders_Sorted[["Purchase Count", "Average Purchase Price", "Total Purchase Value"]]

#display the finished data frame
Top_Spenders_Sorted.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
#create a new data frame by taking the "Item Id", "Item Name", and ""Price columns from the main data frame
popItems_df = df[["Item ID", "Item Name", "Price"]]
popItems_df.head()

#find how many of each Item ID exists and set to a variable
itemPurCount = df["Item ID"].value_counts()
itemPurCount.head()

#use the last variable to create a new dataframe
itemNumPurchases = pd.DataFrame(itemPurCount)
#Change the column names
itemNumPurchases = itemNumPurchases.rename(columns={"Item ID": "Purchase Count"})
#name the index
itemNumPurchases.index.name = "Item ID"
itemNumPurchases.head()

#group the data frame popItems by "Item ID" and "Index"
grouped_Items = popItems_df.groupby(["Item ID", "Item Name"])
#create a data frame for grouped_Items with the sum of it's "Price" column
grouped_Items_df = pd.DataFrame(grouped_Items["Price"].sum())
grouped_Items_df.head()

#merge the grouped_Items_df with the itemNumPurchases by their indexes
mergedPopItems = pd.merge(grouped_Items_df, itemNumPurchases, left_index=True, right_index=True)
mergedPopItems.head()

#create a new variable holding the "Price" and correct purchase count columns from the merged data frame
correctMergedPopItems = mergedPopItems[["Price", "Purchase Count"]]
correctMergedPopItems.head()

#create a new varable with the value of the last data frame, but change the column titles
correctMergedPopItTitles = correctMergedPopItems.rename(columns = {"Price":"Total Purchase Value", "Purchase Count_y":"Purchase Count"})
correctMergedPopItTitles

#add a new column called "Item Price" to shw the price of each colum by dividing the item's total count
correctMergedPopItTitles["Item Price"] = (correctMergedPopItTitles["Total Purchase Value"]/correctMergedPopItTitles["Purchase Count"])
correctMergedPopItTitles.head()

#sort by the "Purchase Count" column and display in decending order, set to a new variable
mergedPopIt_sorted = correctMergedPopItTitles.sort_values("Purchase Count", ascending=False)
mergedPopIt_sorted.head()

#reorder the columns
mergedPopIt_sorted = mergedPopIt_sorted[["Purchase Count", "Item Price", "Total Purchase Value"]]
mergedPopIt_sorted.head()

#Change the columns displaying money to a currency format by changing the format of all columns that are floats
pd.options.display.float_format = '${:,.2f}'.format
mergedPopIt_sorted.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>19</th>
      <th>Pursuit, Cudgel of Necromancy</th>
      <td>8</td>
      <td>$1.02</td>
      <td>$8.16</td>
    </tr>
  </tbody>
</table>
</div>



# Most Profitable Items


```python
#sort the most popular items data frame by the "Total Purchase Value" and show in decending order to find the most profitable item
#set to a new variable and display the variable
highProfItems = mergedPopIt_sorted.sort_values("Total Purchase Value", ascending=False)
highProfItems.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>8</td>
      <td>$4.88</td>
      <td>$39.04</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>
