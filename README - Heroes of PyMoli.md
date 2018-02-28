

```python
#                     ****OBSERVABLE TRENDS****


#1.  First we can say something very generak about the video-gaming industry:  It
# is quiet profiable based on the sole fact that users are willing to purchase
# "virtual" items during game-play.  IE, players are willing to spend money not JUST ON
# purchasing a game, but WHILE in a game.  This is a rather new trend that can
# quiet obersvably produce not just fixed revenues "up-front", but a range of 
# revenue-streams throughout the life of a game.   This is a very new concept
# in gaming, compared to console-based gaming of the 80's, 90's, and early 00's.


#2.  More men are playing games than women.  This data set shows that over 80% of 
# the observed particants are male.  This is an overwhelming skew that most likely
# would be seen in other data sets (as well as this one).


#3.   The 15-29 age range is responisble for the bulk of the revenue, in terms of
# in-game purchases.  With most of that falling in the 20-24 age range.  This seems to be
# the "target-market", should a company be asked to focus upon.  

#4.   So to conclude, we can say that males between the ages of 15-29 (predomintly
# in the 20-24 "bin") are the biggest spending-group in modern gaming.   


```


```python
# For Heroes of PyMoli!:
# First we add the modules/dependencies

import pandas as pd
import numpy as np


```


```python
# Import the data files/path / create the path:

file = os.path.join('Instructions/HeroesOfPymoli', 'purchase_data.json')

# name our Purchase data file "pur_data" & instruct the json file to be read:

pur_data = pd.read_json(file)

# view the data to see the columns/ entries & how they appear:

pur_data.head()

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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#   FINAL REPORT for data set 1...................................

#                    ****PLAYER COUNT****

# Calculate the number of players based on the individual screen names ("SN" column)
player_count = len(pur_data['SN'].unique())


```


```python
#Create the DataFrame for the players (count):  Dataframe will be players_df:

players_df = pd.DataFrame([{'Total Players': player_count}])


#Hides the "0-Index" column (as not needed).  Only need to see the total players. 
players_df.set_index('Total Players', inplace = True)


#Creates/prints the dataframe below.   Total players are 573 in purchase data set1.
players_df



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
    </tr>
    <tr>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>573</th>
    </tr>
  </tbody>
</table>
</div>




```python
#                   ****PURCHASING ANALYSIS (TOTALS)****





# Number of Unique Items & Average Purchase price: (Printing as a complete list of the item's ID and number of times purchased
# or occurances).  There are 183 items in dataset 1.

pur_data['Item ID'].value_counts()



# However we want to reduce the dataset to show only the total purchases for each unique item's ID:
unique_items = pd.DataFrame(pur_data['Item ID'].unique())
len(unique_items)


#Now we create a df but only keeping last occurance of Item ID
no_dup_items = pur_data.drop_duplicates(['Item ID'], keep = 'last')




#Total Number of Purchases & Total Revenue:


#Now we count the items by unique ID (total-unique)
total_unique = len(no_dup_items)


#finds the number of total purchases by counting occurances of price
total_pur = pur_data['Price'].count()


#calculates total revenue for table by summing occurance of price and below calc
total_rev = round(pur_data['Price'].sum(),2)

#calculates total_rev
avg_price = round(total_rev/total_pur, 2)
 
#creates Purchase Analysis DataFrame
pur_analysis = pd.DataFrame([{
    
    "Number of Unique Items": total_unique,
    'Average Purchase Price': avg_price,
    'Total Purchases': total_pur,
    'Total Revenue': total_rev
}])
 
#format Purchases Analysis Table
pur_analysis.style.format({'Average Purchase Price': '${:.2f}', 'Total Revenue': '${:,.2f}'})
```




<style  type="text/css" >
</style>  
<table id="T_580c073e_1c1c_11e8_861f_b0359f01b07a" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Number of Unique Items</th> 
        <th class="col_heading level0 col2" >Total Purchases</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_580c073e_1c1c_11e8_861f_b0359f01b07alevel0_row0" class="row_heading level0 row0" >0</th> 
        <td id="T_580c073e_1c1c_11e8_861f_b0359f01b07arow0_col0" class="data row0 col0" >$2.93</td> 
        <td id="T_580c073e_1c1c_11e8_861f_b0359f01b07arow0_col1" class="data row0 col1" >183</td> 
        <td id="T_580c073e_1c1c_11e8_861f_b0359f01b07arow0_col2" class="data row0 col2" >780</td> 
        <td id="T_580c073e_1c1c_11e8_861f_b0359f01b07arow0_col3" class="data row0 col3" >$2,286.33</td> 
    </tr></tbody> 
</table> 




```python
#                    ****GENDER DEMOGRAPHICS****





# Finding the Percentage and Count of Male Players 
# Finding the Percentage and Count of Female Players
# Percentage and Count of Other / Non-Disclosed


# First we filter down unique players by SN (keeping only 1 entry per player, so there are no duplicates):
no_dup_players = pur_data.drop_duplicates(['SN'], keep ='last')

#  From the "no_dup_players" df above, we count the gender values:
gender_counts = no_dup_players['Gender'].value_counts().reset_index()


# Now we add a column for % of players using player_count from our table created (in input box 4, near the begining)
# and from the gender_counts column above:

gender_counts['% of Players'] = gender_counts['Gender']/player_count * 100

# Now renames columns to desired values needed:
gender_counts.rename(columns = {'index': 'Gender', 'Gender': '# of Players'}, inplace = True)

# Set the first (0) index as "Gender".
gender_counts.set_index(['Gender'], inplace = True)



#formats table
gender_counts.style.format({"% of Players": "{:.1f}%"})




```




<style  type="text/css" >
</style>  
<table id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07a" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" ># of Players</th> 
        <th class="col_heading level0 col1" >% of Players</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07alevel0_row0" class="row_heading level0 row0" >Male</th> 
        <td id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07arow0_col0" class="data row0 col0" >465</td> 
        <td id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07arow0_col1" class="data row0 col1" >81.2%</td> 
    </tr>    <tr> 
        <th id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07alevel0_row1" class="row_heading level0 row1" >Female</th> 
        <td id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07arow1_col0" class="data row1 col0" >100</td> 
        <td id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07arow1_col1" class="data row1 col1" >17.5%</td> 
    </tr>    <tr> 
        <th id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07alevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07arow2_col0" class="data row2 col0" >8</td> 
        <td id="T_58613e06_1c1c_11e8_a1cc_b0359f01b07arow2_col1" class="data row2 col1" >1.4%</td> 
    </tr></tbody> 
</table> 




```python
#                    ****Purchasing Analysis (by Gender)****






# Breaking down the following by gender:
   #Purchase Count
   #Average Purchase Price
   #Total Purchase Value
   #Normalized Totals


# Our purchase count by gender dataframe:
pur_count_by_gen = pd.DataFrame(pur_data.groupby('Gender')['Gender'].count())




#  **Calculating the Total Purchase Values:

#  Our Total purchase price by gender dataframe:
total_pur_by_gen = pd.DataFrame(pur_data.groupby('Gender')['Price'].sum())

#  Merges the two data frames from above,  so we can calc the average puch price:
pur_analysis_gen = pd.merge(pur_count_by_gen, total_pur_by_gen, left_index = True, right_index = True)

# Renames our columns:
pur_analysis_gen.rename(columns = {'Gender': '# of Purchases', 'Price':'Total Purchase Value'}, inplace=True)




#  **Calculating the Average Purchase Prices:

# Now we add a column for average purchase price, by gender -- by dividing total purchase value by gender by # of purchases by gender
pur_analysis_gen['Average Purchase Price'] = pur_analysis_gen['Total Purchase Value']/pur_analysis_gen['# of Purchases']

# Now merge our gender counts from the above table, and exclude any dup SNs) into current df. 
pur_analysis_gen = pur_analysis_gen.merge(gender_counts, left_index = True, right_index = True)





#  **Finding the Normalized Totals:  The "Normalized Totals" take into account the proportion of a 
# ...given demographic.  
# First, we calculate and add normalized total column by dividing total purchase value by unique # of players by gender
#(As stated above, we need to take into accoun the proportion....)
pur_analysis_gen['Normalized Totals'] = pur_analysis_gen['Total Purchase Value']/pur_analysis_gen['# of Players']
pur_analysis_gen

# Next we deletes columns not needed for table. The # of Players was used for normalized totals above, while % of players came from gender count table above.)
del pur_analysis_gen['% of Players']
del pur_analysis_gen['# of Players']

# Last we format our table:
pur_analysis_gen.style.format({'Total Purchase Value': '${:.2f}', 'Average Purchase Price': '${:.2f}', 'Normalized Totals': '${:.2f}'})


```




<style  type="text/css" >
</style>  
<table id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07a" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" ># of Purchases</th> 
        <th class="col_heading level0 col1" >Total Purchase Value</th> 
        <th class="col_heading level0 col2" >Average Purchase Price</th> 
        <th class="col_heading level0 col3" >Normalized Totals</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07alevel0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow0_col0" class="data row0 col0" >136</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow0_col1" class="data row0 col1" >$382.91</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow0_col2" class="data row0 col2" >$2.82</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow0_col3" class="data row0 col3" >$3.83</td> 
    </tr>    <tr> 
        <th id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07alevel0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow1_col0" class="data row1 col0" >633</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow1_col1" class="data row1 col1" >$1867.68</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow1_col2" class="data row1 col2" >$2.95</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow1_col3" class="data row1 col3" >$4.02</td> 
    </tr>    <tr> 
        <th id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07alevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow2_col0" class="data row2 col0" >11</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow2_col1" class="data row2 col1" >$35.74</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow2_col2" class="data row2 col2" >$3.25</td> 
        <td id="T_58a94d92_1c1c_11e8_a93d_b0359f01b07arow2_col3" class="data row2 col3" >$4.47</td> 
    </tr></tbody> 
</table> 




```python
#                    ****Age Demographics (by Gender)****






# In this section we are given bins that are broken down into 4 years each (per bin)
# (0 to 10,  10-14,  15-19.  etc.)



# Purchase Count

# Creating columns for each age bin which are subject to the age range (of those in the purchasing data sets):
#  We start from ages less than 10, then 10-14, and every 4 year bins with a max of greater than 40:

pur_data.loc[(pur_data['Age'] < 10), 'age_bin'] = "< 10"
pur_data.loc[(pur_data['Age'] >= 10) & (pur_data['Age'] <= 14), 'age_bin'] = "10 - 14"
pur_data.loc[(pur_data['Age'] >= 15) & (pur_data['Age'] <= 19), 'age_bin'] = "15 - 19"
pur_data.loc[(pur_data['Age'] >= 20) & (pur_data['Age'] <= 24), 'age_bin'] = "20 - 24"
pur_data.loc[(pur_data['Age'] >= 25) & (pur_data['Age'] <= 29), 'age_bin'] = "25 - 29"
pur_data.loc[(pur_data['Age'] >= 30) & (pur_data['Age'] <= 34), 'age_bin'] = "30 - 34"
pur_data.loc[(pur_data['Age'] >= 35) & (pur_data['Age'] <= 39), 'age_bin'] = "35 - 39"
pur_data.loc[(pur_data['Age'] >= 40), 'age_bin'] = "> 40"



#  Now we count the purchases by/per age bin using the screen names:
pur_count_age = pd.DataFrame(pur_data.groupby('age_bin')['SN'].count())



# ***Average Purchase Price:
#finds avg price of purchases by age bin
avg_price_age = pd.DataFrame(pur_data.groupby('age_bin')['Price'].mean())


# **Total Purchase Valye by age bin:
tot_pur_age = pd.DataFrame(pur_data.groupby('age_bin')['Price'].sum())

# Remove duplicates of screen names & keep last (as done above) and counts the number of players by age bin.
no_dup_age = pd.DataFrame(pur_data.drop_duplicates('SN', keep = 'last').groupby('age_bin')['SN'].count())

# Merge the above info into our new data frame:
merge_age = pd.merge(pur_count_age, avg_price_age, left_index = True, right_index = True).merge(tot_pur_age, left_index = True, right_index = True).merge(no_dup_age, left_index = True, right_index = True)

# Now we rename the columns of our newly merged data frame, for the values we wish to find:
merge_age.rename(columns = {"SN_x": "# of Purchases", "Price_x": "Average Purchase Price", "Price_y": "Total Purchase Value", "SN_y": "# of Purchasers"}, inplace = True)


# As previous, we want the "Normalized Totals" -- IE, taking into account demogrpahics / different proportions.
merge_age['Normalized Totals'] = merge_age['Total Purchase Value']/merge_age['# of Purchasers']


# formats
merge_age.style.format({'Average Purchase Price': '${:.2f}', 'Total Purchase Value': '${:.2f}', 'Normalized Totals': '${:.2f}'})


```




<style  type="text/css" >
</style>  
<table id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07a" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" ># of Purchases</th> 
        <th class="col_heading level0 col1" >Average Purchase Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
        <th class="col_heading level0 col3" ># of Purchasers</th> 
        <th class="col_heading level0 col4" >Normalized Totals</th> 
    </tr>    <tr> 
        <th class="index_name level0" >age_bin</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row0" class="row_heading level0 row0" >10 - 14</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow0_col0" class="data row0 col0" >35</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow0_col1" class="data row0 col1" >$2.77</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow0_col2" class="data row0 col2" >$96.95</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow0_col3" class="data row0 col3" >23</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow0_col4" class="data row0 col4" >$4.22</td> 
    </tr>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row1" class="row_heading level0 row1" >15 - 19</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow1_col0" class="data row1 col0" >133</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow1_col1" class="data row1 col1" >$2.91</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow1_col2" class="data row1 col2" >$386.42</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow1_col3" class="data row1 col3" >100</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow1_col4" class="data row1 col4" >$3.86</td> 
    </tr>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row2" class="row_heading level0 row2" >20 - 24</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow2_col0" class="data row2 col0" >336</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow2_col1" class="data row2 col1" >$2.91</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow2_col2" class="data row2 col2" >$978.77</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow2_col3" class="data row2 col3" >259</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow2_col4" class="data row2 col4" >$3.78</td> 
    </tr>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row3" class="row_heading level0 row3" >25 - 29</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow3_col0" class="data row3 col0" >125</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow3_col1" class="data row3 col1" >$2.96</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow3_col2" class="data row3 col2" >$370.33</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow3_col3" class="data row3 col3" >87</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow3_col4" class="data row3 col4" >$4.26</td> 
    </tr>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row4" class="row_heading level0 row4" >30 - 34</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow4_col0" class="data row4 col0" >64</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow4_col1" class="data row4 col1" >$3.08</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow4_col2" class="data row4 col2" >$197.25</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow4_col3" class="data row4 col3" >47</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow4_col4" class="data row4 col4" >$4.20</td> 
    </tr>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row5" class="row_heading level0 row5" >35 - 39</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow5_col0" class="data row5 col0" >42</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow5_col1" class="data row5 col1" >$2.84</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow5_col2" class="data row5 col2" >$119.40</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow5_col3" class="data row5 col3" >27</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow5_col4" class="data row5 col4" >$4.42</td> 
    </tr>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row6" class="row_heading level0 row6" >< 10</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow6_col0" class="data row6 col0" >28</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow6_col1" class="data row6 col1" >$2.98</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow6_col2" class="data row6 col2" >$83.46</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow6_col3" class="data row6 col3" >19</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow6_col4" class="data row6 col4" >$4.39</td> 
    </tr>    <tr> 
        <th id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07alevel0_row7" class="row_heading level0 row7" >> 40</th> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow7_col0" class="data row7 col0" >17</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow7_col1" class="data row7 col1" >$3.16</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow7_col2" class="data row7 col2" >$53.75</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow7_col3" class="data row7 col3" >11</td> 
        <td id="T_58ecc69e_1c1c_11e8_82d4_b0359f01b07arow7_col4" class="data row7 col4" >$4.89</td> 
    </tr></tbody> 
</table> 




```python
#                    ****TOP SPENDERS****






## Identitfying the top 5 spenders in our Heroes of PyMoli game 
#...based on "Total Purchase Value" & listing the following values in a table:
#  SN, Purchase Count, Average Purchase Price, and Total Purchase Value.


#  First we sort the users by screen name to find: 
# total purchase by SN.
purchase_amt_by_SN = pd.DataFrame(pur_data.groupby('SN')['Price'].sum())

# Number of puchases by SN
num_purchase_by_SN = pd.DataFrame(pur_data.groupby('SN')['Price'].count())

# Average price by SN
avg_purchase_by_SN = pd.DataFrame(pur_data.groupby('SN')['Price'].mean())


#  We then merge the above to a new "merged_top5":
merged_top5 = pd.merge(purchase_amt_by_SN, num_purchase_by_SN, left_index = True, 
right_index = True).merge(avg_purchase_by_SN, left_index=True, right_index=True)

# Now rename columns to reflect the values we wish to find (stated above):
merged_top5.rename(columns = {'Price_x': 'Total Purchase Value', 
'Price_y':'Purchase Count', 'Price':'Average Purchase Price'}, inplace = True)

# Since we want the top 5, we will need to...

#  First, sort from highest spending (purchase value) to lowest.
#  Then show only the top 5
merged_top5.sort_values('Total Purchase Value', ascending = False, inplace=True)
merged_top5 = merged_top5.head()

# Display our top 5 screen names based on their purchase value, purchase count, and AVG purchase price.
merged_top5.style.format({'Total Purchase Value': '${:.2f}', 'Average Purchase Price': '${:.2f}'})

```




<style  type="text/css" >
</style>  
<table id="T_59346108_1c1c_11e8_9f77_b0359f01b07a" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Purchase Value</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Average Purchase Price</th> 
    </tr>    <tr> 
        <th class="index_name level0" >SN</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_59346108_1c1c_11e8_9f77_b0359f01b07alevel0_row0" class="row_heading level0 row0" >Undirrala66</th> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow0_col0" class="data row0 col0" >$17.06</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow0_col1" class="data row0 col1" >5</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow0_col2" class="data row0 col2" >$3.41</td> 
    </tr>    <tr> 
        <th id="T_59346108_1c1c_11e8_9f77_b0359f01b07alevel0_row1" class="row_heading level0 row1" >Saedue76</th> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow1_col0" class="data row1 col0" >$13.56</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow1_col1" class="data row1 col1" >4</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow1_col2" class="data row1 col2" >$3.39</td> 
    </tr>    <tr> 
        <th id="T_59346108_1c1c_11e8_9f77_b0359f01b07alevel0_row2" class="row_heading level0 row2" >Mindimnya67</th> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow2_col0" class="data row2 col0" >$12.74</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow2_col1" class="data row2 col1" >4</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow2_col2" class="data row2 col2" >$3.18</td> 
    </tr>    <tr> 
        <th id="T_59346108_1c1c_11e8_9f77_b0359f01b07alevel0_row3" class="row_heading level0 row3" >Haellysu29</th> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow3_col0" class="data row3 col0" >$12.73</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow3_col1" class="data row3 col1" >3</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow3_col2" class="data row3 col2" >$4.24</td> 
    </tr>    <tr> 
        <th id="T_59346108_1c1c_11e8_9f77_b0359f01b07alevel0_row4" class="row_heading level0 row4" >Eoda93</th> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow4_col0" class="data row4 col0" >$11.58</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow4_col1" class="data row4 col1" >3</td> 
        <td id="T_59346108_1c1c_11e8_9f77_b0359f01b07arow4_col2" class="data row4 col2" >$3.86</td> 
    </tr></tbody> 
</table> 




```python
#                    ****MOST POPULAR ITEMS****





#  Finding the most popular 5 items based on purchase count, & listing in our table
#  Item ID, Item Name, Purchase Count of item, Item price, and the total purchase value:


# First we get a count of the items and group by their corresponding ID.  
#  We then will count the number of occurances.

# will call top5_popitems_ID.
top5_popitems_ID = pd.DataFrame(pur_data.groupby('Item ID')['Item ID'].count())

# sort from high to low total purchase count:
top5_popitems_ID.sort_values('Item ID', ascending = False, inplace = True)

# Now filter for our top 5 items:
top5_popitems_ID = top5_popitems_ID.iloc[0:5][:]


#  Now find the Purchase/Price Data*****


# the total purchase value of each item
top5_popitems_total = pd.DataFrame(pur_data.groupby('Item ID')['Price'].sum())

# Merge purchase count and total purcahse value (the two parts found above) 
top5_popitems = pd.merge(top5_items_ID, top5_items_total, left_index = True, right_index = True)

# Clear out any duplicates the from original Df
no_dup_items = pur_data.drop_duplicates(['Item ID'], keep = 'last')

# merge to get all other info from the top 5 using the no_dup items from above:
top5_merge_ID = pd.merge(top5_popitems, no_dup_items, left_index = True, right_on = 'Item ID')

# Filter out only the columns with data we are looking for:
top5_merge_ID = top5_merge_ID[['Item ID', 'Item Name', 'Item ID_x', 'Price_y', 'Price_x']]


# rename columns to reflect the values we wish to find (stated above)
top5_merge_ID.rename(columns =  {'Item ID_x': 'Purchase Count', 'Price_y': 'Item Price', 'Price_x': 'Total Purchase Value'}, inplace=True)

#format:  Display our top 5 values:
top5_merge_ID.style.format({'Item Price': '${:.2f}', 'Total Purchase Value': '${:.2f}'})

```




<style  type="text/css" >
</style>  
<table id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07a" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Item ID</th> 
        <th class="col_heading level0 col1" >Item Name</th> 
        <th class="col_heading level0 col2" >Purchase Count</th> 
        <th class="col_heading level0 col3" >Item Price</th> 
        <th class="col_heading level0 col4" >Total Purchase Value</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07alevel0_row0" class="row_heading level0 row0" >721</th> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow0_col0" class="data row0 col0" >39</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow0_col1" class="data row0 col1" >Betrayal, Whisper of Grieving Widows</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow0_col2" class="data row0 col2" >11</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow0_col3" class="data row0 col3" >$2.35</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow0_col4" class="data row0 col4" >$25.85</td> 
    </tr>    <tr> 
        <th id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07alevel0_row1" class="row_heading level0 row1" >766</th> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow1_col0" class="data row1 col0" >84</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow1_col1" class="data row1 col1" >Arcane Gem</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow1_col2" class="data row1 col2" >11</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow1_col3" class="data row1 col3" >$2.23</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow1_col4" class="data row1 col4" >$24.53</td> 
    </tr>    <tr> 
        <th id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07alevel0_row2" class="row_heading level0 row2" >772</th> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow2_col0" class="data row2 col0" >31</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow2_col1" class="data row2 col1" >Trickster</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow2_col2" class="data row2 col2" >9</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow2_col3" class="data row2 col3" >$2.07</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow2_col4" class="data row2 col4" >$18.63</td> 
    </tr>    <tr> 
        <th id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07alevel0_row3" class="row_heading level0 row3" >761</th> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow3_col0" class="data row3 col0" >175</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow3_col1" class="data row3 col1" >Woeful Adamantite Claymore</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow3_col2" class="data row3 col2" >9</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow3_col3" class="data row3 col3" >$1.24</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow3_col4" class="data row3 col4" >$11.16</td> 
    </tr>    <tr> 
        <th id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07alevel0_row4" class="row_heading level0 row4" >765</th> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow4_col0" class="data row4 col0" >13</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow4_col1" class="data row4 col1" >Serenity</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow4_col2" class="data row4 col2" >9</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow4_col3" class="data row4 col3" >$1.49</td> 
        <td id="T_598689b6_1c1c_11e8_b9c5_b0359f01b07arow4_col4" class="data row4 col4" >$13.41</td> 
    </tr></tbody> 
</table> 




```python
#                    ****MOST PROFITABLE ITEMS****






# Here we find the 5 most profitable items by total purchase value create a table
# with the following:  ItemID, Item Name, Purchase Count, Item Price, Total Purchase Value:


# First we find/sort the Purchase Values, and sort them from H to Low:
#  Calling it top5_profitable:

top5_profitable = pd.DataFrame(pur_data.groupby('Item ID')['Price'].sum())

# Sorting High to Low:
top5_profitable.sort_values('Price', ascending = False, inplace = True)

# Filtering for only the top 5:
top5_profitable = top5_profitable.iloc[0:5][:]

# Find the Purchase Count for the items:
pur_count_profitable = pd.DataFrame(pur_data.groupby('Item ID')['Item ID'].count())
 

# Merging the data
top5_profitable = pd.merge(top5_profitable, pur_count_profitable, left_index = True, right_index = True, how = 'left')

top5_merge_profitable = pd.merge(top5_profitable, no_dup_items, left_index = True, right_on = 'Item ID', how = 'left')

top5_merge_profitable = top5_merge_profitable[['Item ID', 'Item Name', 'Item ID_x', 'Price_y','Price_x']]

top5_merge_profitable.set_index(['Item ID'], inplace=True)

top5_merge_profitable.rename(columns = {'Item ID_x': 'Purchase Count', 'Price_y': 'Item Price', 'Price_x': 'Total Purchase Value'}, inplace = True)
top5_merge_profitable.style.format({'Item Price': '${:.2f}', 'Total Purchase Value': '${:.2f}'})

```




<style  type="text/css" >
</style>  
<table id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07a" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Item Name</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Item Price</th> 
        <th class="col_heading level0 col3" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07alevel0_row0" class="row_heading level0 row0" >34</th> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow0_col0" class="data row0 col0" >Retribution Axe</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow0_col1" class="data row0 col1" >9</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow0_col2" class="data row0 col2" >$4.14</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow0_col3" class="data row0 col3" >$37.26</td> 
    </tr>    <tr> 
        <th id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07alevel0_row1" class="row_heading level0 row1" >115</th> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow1_col0" class="data row1 col0" >Spectral Diamond Doomblade</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow1_col1" class="data row1 col1" >7</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow1_col2" class="data row1 col2" >$4.25</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow1_col3" class="data row1 col3" >$29.75</td> 
    </tr>    <tr> 
        <th id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07alevel0_row2" class="row_heading level0 row2" >32</th> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow2_col0" class="data row2 col0" >Orenmir</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow2_col1" class="data row2 col1" >6</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow2_col2" class="data row2 col2" >$4.95</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow2_col3" class="data row2 col3" >$29.70</td> 
    </tr>    <tr> 
        <th id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07alevel0_row3" class="row_heading level0 row3" >103</th> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow3_col0" class="data row3 col0" >Singed Scalpel</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow3_col1" class="data row3 col1" >6</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow3_col2" class="data row3 col2" >$4.87</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow3_col3" class="data row3 col3" >$29.22</td> 
    </tr>    <tr> 
        <th id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07alevel0_row4" class="row_heading level0 row4" >107</th> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow4_col0" class="data row4 col0" >Splitter, Foe Of Subtlety</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow4_col1" class="data row4 col1" >8</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow4_col2" class="data row4 col2" >$3.61</td> 
        <td id="T_59be3a18_1c1c_11e8_b7a8_b0359f01b07arow4_col3" class="data row4 col3" >$28.88</td> 
    </tr></tbody> 
</table> 




```python
# ****END
```
