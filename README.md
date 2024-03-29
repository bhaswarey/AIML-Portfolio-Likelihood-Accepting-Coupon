# Case Study : Conditional Acceptance of Coupon

[Link to notebook:]  [AIML-Portfolio-Likelihood-Accepting-Coupon/prompt.ipynb at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/prompt.ipynb) 



## Context

The goal of this project is to predict the likelihood of customers’ acceptance of coupons during campaigns run by the hospitality industry. This is the first part in the series of studies, focusing on all the phases covering up to "Data Preparation" phase in the CRISP-DM-DM process (see Figure 1).

 ![CRISP-DM.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/CRISP-DM.png) 

**Figure 1 - CRISP-DM process model**



# 1 Business Understanding

## 1.1 Background

Imagine driving through town and a coupon is delivered to your cell phone for a restaurant near where you are driving. Would you accept that coupon and take a short detour to the restaurant? Would you accept the coupon but use it on a subsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaurant? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? 

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? What are the relevant characteristics of the driver who is likely to accept a coupon?



 ![bar_coupon_types_dist.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/bar_coupon_types_dist.png) 

**Figure 2 - Distribution of coupons by type**



Figure 2 provides a view of the distribution of the coupons offered to participants across the different types of business within the hospitality industry. The distribution in Figure 2 shows that the coupon campaign is skewed heavily towards the Coffee House businesses.



![bar_accept_reject_coupon_types_dist.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/bar_accept_reject_coupon_types_dist.png) 

**Figure 3 - Distribution of accepted & rejected coupons by type**



Figure 3 - provides a view of the distribution accepted and rejected offers across the entire coupon category. The figure highlights the coupon types that have the highest acceptance and rejection rates, providing a view of where improvements are needed.

In summary, the business problem is as follows:

·    Identify opportunities to improve acceptance rates of Bar and Coffee House based on the acceptance rate of the Carry out & Take away coupon.

·    The characteristics of the drivers with high acceptance rate. Note that the Carry out & Take away coupon has the best acceptance to rejection ratio.

 



## 1.2 Business Goals and KPI

The business goal is to:

·    Targeted offers to drivers with one or more characteristics that would improve the acceptance rate.

·    Reduce cost of rejected coupon (by eliminating production and distribution cost incurred during coupon offer campaigns).



# 2 Data Understanding

This section provides information about the data, its description and is its exploration to make sure it fits the business goals.



## 2.1 **Gathering and Describing Data**

This data comes from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’. There are five different types of coupons -- less expensive restaurants (under \$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\$20 - \$50).



![original.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/original.png?raw=true)



Here is a sample of the data, which provides information about the structure of the data including:

·    The number of rows (each row represents a single response data)

·    The number of columns

·    The name of each column

·    The data type of each column



The collected data consists of **12684** responses with **26** attributes/columns. The description of each column/variable can be seen below:

**DataFrame:**

**RangeIndex:**12684 entries, 0 to 12683





**Data columns** (total 26 columns):

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/table0.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/table0.png) 



**Total dtypes: int64(8), object(18)**



The description of each attribute is as follows:

1. User attributes
    -  Gender: male, female
    -  Age: below 21, 21 to 25, 26 to 30, etc.
    -  Marital Status: single, married partner, unmarried partner, or widowed
    -  Number of children: 0, 1, or more than 1
    -  Education: high school, bachelors degree, associates degree, or graduate degree
    -  Occupation: architecture & engineering, business & financial, etc.
    -  Annual income: less than \\$12500, \\$12500 - \\$24999, \\$25000 - \\$37499, etc.
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she buys takeaway food: 0, less than 1, 1 to 3, 4 to 8 or greater
    than 8
    -  Number of times that he/she goes to a coffee house: 0, less than 1, 1 to 3, 4 to 8 or
    greater than 8
    -  Number of times that he/she eats at a restaurant with average expense less than \\$20 per
    person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    
2. Contextual attributes
    - Driving destination: home, work, or no urgent destination
    - Location of user, coupon and destination: we provide a map to show the geographical
    location of the user, destination, and the venue, and we mark the distance between each
    two places with time of driving. The user can see whether the venue is in the same
    direction as the destination.
    - Weather: sunny, rainy, or snowy
    - Temperature: 30F, 55F, or 80F
    - Time: 10AM, 2PM, or 6PM
    - Passenger: alone, partner, kid(s), or friend(s)


3. Coupon attributes
    - time before it expires: 2 hours or one day
    
      



## 2.2 Early Data Exporation and Data Quality Check

Next step is to check the quality of the data. For example, since many of the column/variable is categorical, the summary of the data is checked for the types in each category. By doing this, the step needed for data cleaning or to be transformed is identified. For example, checking for missing/empty values.

Following is the summary statistics (mean, median, min, max, etc.) of the data:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>temperature</th>
      <th>has_children</th>
      <th>toCoupon_GEQ5min</th>
      <th>toCoupon_GEQ15min</th>
      <th>toCoupon_GEQ25min</th>
      <th>direction_same</th>
      <th>direction_opp</th>
      <th>Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>12684.000000</td>
      <td>12684.000000</td>
      <td>12684.0</td>
      <td>12684.000000</td>
      <td>12684.000000</td>
      <td>12684.000000</td>
      <td>12684.000000</td>
      <td>12684.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>63.301798</td>
      <td>0.414144</td>
      <td>1.0</td>
      <td>0.561495</td>
      <td>0.119126</td>
      <td>0.214759</td>
      <td>0.785241</td>
      <td>0.568433</td>
    </tr>
    <tr>
      <th>std</th>
      <td>19.154486</td>
      <td>0.492593</td>
      <td>0.0</td>
      <td>0.496224</td>
      <td>0.323950</td>
      <td>0.410671</td>
      <td>0.410671</td>
      <td>0.495314</td>
    </tr>
    <tr>
      <th>min</th>
      <td>30.000000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>55.000000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>80.000000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>80.000000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>80.000000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>


Following is the category of each column that is of type object:

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/table1.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/table1.png) 



Following is the percentage of missing values per column:

**car					99.15%**

**Bar					0.84%**

**CoffeeHouse			1.71%**

**CarryAway                           1.19%**

**RestaurantLessThan20    1.02%**

**Restaurant20To50             1.49%**



Finally, The number of **duplicate rows is 74**.



There is some interesting finding from the summary. For example, the there are a few columns like car that have nan (Unknown). The expiration column contains time in days and hours. The columns like Bar has ranges, for example, 4-8 or gt8, etc. The occupation column has very large stings. As a result, the data need to be cleansed and transformed followed by preparation before any analysis can be executed, so that all relevant information can be captured.



# 3 Data Preparation

This section provides information on data preparation and cleaning, to allow for analysis as part of this case study and the future case studies covering predictions.  



## 3.1 Data Transformation

Following data attributes that were treated:

a) passanger - convert "Kid(s)" -> "Kid" & "Friend(s)" -> Friend

b) time - convert AM/PM format to military (24-hour) time (integer).

c) expiration - convert from day to hours (integer)

d) age - normalize to integers

e) income - for each range convert the average (integer)

f) Bar/CoffeeHouse/ResturantLessThan20/Resturant20To50 - convert to integers

g) Shorten occupation strings



## 3.2 Data Cleansing

In this step, the data is handled based on the problem found during the data understanding phase. Based on the finding, the following steps are executed:

a) If the percentage of missing values, per column, is >= 70%, then we will drop the entire column.

b) If the percentage of missing values, per column, is < 30%, then keep the column and evaluate.

c) For columns with missing values > 10%, the values will be filled using interpolation technique or mean or media or mode. Will depend on the data characters. 

d) For columns with missing data <= 10%, the associated row will simply be dropped.

e) Finally, find and drop duplicate rows



**Post cleaned data view:**
Index: 12007 entries, 22 to 12683
Data columns (total 25 columns):



After the data clean process was executed, the columns was reduced from **26 to 25** and the rows were reduced from **12683 to 12007**, i.e., number of rows are reduced by **5.33%**.

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/table3.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/table3.png) 

## 3.3 Final Data

![image-20240303004736785.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/image-20240303004736785.png?raw=true)



# 4 Data Understanding - Deep Analysis

This section provides information about deeper exploration and analysis of the data conducted, in preparation for future machine learning model.



## 4.1 Exploratory Data Analysis

In this section, the results of exploring and visualizing insight from the data is captured.



### 4.1.1 Temperature During Campaigns

Figure 4 provide the temperature during the distribution of coupon offer campaigns.



![AIML-Portfolio-Likelihood-Accepting-Coupon/images/hist_temperature.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/hist_temperature.png) 

**Figure 4 - Temperature during coupon offer campaigns**



Figure 5-a provides a view of the accepted/rejected coupons and the associated temperature during that day.



![AIML-Portfolio-Likelihood-Accepting-Coupon/images/hist_temperature_accept_reject.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/hist_temperature_accept_reject.png) 

**Figure 5-a - Distribution of accepted/rejected coupons and associated temperature.**



Figure 5-b provides a view of the types of coupons that were offered and the associated temperature of the day.

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/hist_temperature_coupons_types.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/hist_temperature_coupons_types.png) 

**Figure 5-b - Distribution of types of coupons and associated temperature.**



From the figures above, the number of coupons offered increase with the temperature. This indicates that as the weather warmed up, the outdoor activity increased. And as a result, there were more participants outside accepting offers. 



### 4.1.2 Addressing Bar Coupon Business Questions

Following were some of the business questions answered based on the analysis of the data.

**1) What the acceptance rate between those who went to a bar 3 or fewer times a month to those who went more.**

- Acceptance rate of participants that went to a bar no more than three times are:  **5.31%** 

- Acceptance rate of participants that went to a bar more than three time are:  **1.22%** 
- The ratio between the participants who when to the bar no more than three time to the one who went more than three times is:  **4.34** 
- The acceptance rate of participants who when to the bar no more than three time is **'~4.34'** times than  the participants that went to a bar more than three time.

**2) What the acceptance rate between drivers who go to a bar more than once a month and are over the age of 25 to the all others.  Is there a difference?**

- Acceptance rate of participants (drivers) over the age of twenty five who went to a bar more than once a month are:        **2.32%** 

- Acceptance rate of all other participants:  **4.22%** 

- The ratio between drivers who go to a bar more than once a month and are over the age of 25 to the all others are:  **0.5483** 

- The acceptance rate of the participants (drivers) who go to a bar more than once a month and are over the age of 25 is  about **'~1/2'** times to that of the others. Yes there is a difference, i.e., their total rate is the same as the Bar coupon acceptance rate.

  

**3) Compare the acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry. **

- Acceptance rate of drivers who go to bars more than once a month and had passengers that were not a kid:  **3.13%** 

- Acceptance rate of drivers who go to bars more than once a month and had passengers that were not a kid  and had occupations other than farming, fishing, or forestry:  **3.26%** 

- The ratio between the two:  **0.9592** 

- The acceptance rate of the participants (drivers) who go to bars more than once a month and had passengers  that were not a kid is about **'~1'** times to that of drivers that had occupations other than farming, fishing, or forestry.

  

**4) Compare the acceptance rates between those drivers who:**

​	a. go to bars more than once a month, had passengers that were not a kid, and were not widowed ****OR**** 

​	b. go to bars more than once a month and are under the age of 30 ****OR****

​	c. go to cheap restaurants more than 4 times a month and income is less than 50K. 

- The acceptance rate of the drivers who go to bars more than once a month, had passengers that were not a kid, and were not widowed:  **3.13%** 
- The acceptance rate of the drivers who go to bars more than once a month and are under the age of 30:  **1.97%** 
- The acceptance rate of the drivers who go to cheap restaurants more than 4 times a month and income is less than 50K:  **1.27%** 
- The acceptance rate of the drivers who go to bars more than once a month, had passengers that were not a kid,  and were not widowed is about **'~1.6'** times more to that of the drivers that go to bars more than once a month and are under the age of 30. 
- The acceptance rate of the drivers who go to bars more than once a month, had passengers that were not a kid, and were not widowed  is about **'~2.5'** times more to that of drivers that go to cheap restaurants more than 4 times a month and income is less than 50. 
- The acceptance rate of the drivers who go to bars more than once a month and are under the age of 30 is **'~1.6'** time to that of drivers  that go to cheap restaurants more than 4 times a month and income is less than 50.



### 4.1.3 Identification of Opportunities Based on Deep Data Analysis 

Initial analysis of the data showed that the "Bar" performed poorly, i.e., the rejection rate was much higher than the acceptance rate. The "CarryAway" coupon acceptance to rejection rate was the best performer in the entire coupon categories. Based on this observation, the following strategy was defined:

a) Study the "CarryAway" coupon type to help identify opportunities to improve coupon acceptance rate across all coupon categories

b) Base on the correlation results, identify the characteristics/features of the passenger/driver who accepted the coupon.

c) Identify opportunities to increase acceptance rate by examining the conditional probability of acceptance/rejections; where the conditions derived base on the combination of one or more characteristics/features of the driver/passenger.



### 4.1.3.1 Passenger/Driver Attribute Identify 

Identify attributes associated with passenger's/driver's characteristics "CarryAway" coupon for study. Using the correlation approach, the correlation between the passenger/driver features/characteristics & coupon categories is provided in Figure 6.



 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/heatmap_attributes_coupons.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/heatmap_attributes_coupons.png) 

**Figure 6 - Heatmap of passenger/driver features/characteristics & coupon catagories**



### 4.1.3.2 Observation   

The moderate negative correlation could be an indication that the technique use for transformation of the attributes from string to integer/float may have introduced unintended anomalies, skewing the heatmap. For example, the "maritalStatus" attribute may not have been transformed correctly (i.e., data type has no defined order). One-hot-encoding is a powerful technique that can be used to treat categorical data, but it can lead to increased dimensionality, sparsity, and over-fitting.

From the correlation data, the attributes selected for study are:

a) income

b) maritalStatus

c) has_children

d) education

e) age

f) occupation

Next, lets understand the relationship between passenger types the selected attributes.



### 4.1.4   Passenger/Driver Characteristics Features of The Accepted "CarryAway" Coupon Population

Identify the passenger/driver characteristics features based on the accepted "carryAway" coupon population.

Figure 7 provides the relationship between passenger & education/age/children/marital status, from the population of accepted "CarryAway" coupon.



 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/histplot_accepted_carryaway_passanger_attributes.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/histplot_accepted_carryaway_passanger_attributes.png) 

**Figure 7 - Relationship between passenger & education/age/children/marital status**





### 4.1.4.1   Observation 

From Figure 7, the attributes observed to have independently-highest acceptance are:

a) Passange Type - Alone

b) Education (top 2) - Some College or Bachelors

c) Age - < 37 years of age

d) Marital Status - Single

e) Income - (< 20K) followed by (90K - 100K) followed by (30K - 55K). When grouped, majority would fall in the range of 10k - 55K & 90K - 100K

f) Occupation (top 4) - Student, Unemployed, ComputerMath, SalesRelated





### 4.1.5   Independent Conditions - Probability of Accepting/Rejecting 

Examine the probability of accepting/rejecting CarryAway coupon given the user's/driver's occupation, income, education, and marital status features. These features will be examined as independent conditions.

Figure 8 provides the conditional probability for occupation, income, education, and marital status features.



 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/catplot_accept_reject_education.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/catplot_accept_reject_education1.png) 

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/catplot_accept_reject_income.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/catplot_accept_reject_income1.png) 

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/catplot_accept_reject_maritalstatus.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/catplot_accept_reject_maritalstatus1.png) 

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/catplot_accept_reject_occupation.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/catplot_accept_reject_occupation1.png) 



**Figure 8 - Probability of accepting & rejecting offers base on independent condition**





### 4.1.5.1   Observation 

From the conditional probabilities shown in Figure 8, the following is observed:

**a) Occupation:** The types that had the highest acceptance and the lowest rejections are (in no specific order):

·    Protective Services [0.17, 0.01]

·    HealthPractTech [0.17, 0.01]

·    ConstructExtraction [0.18, 0.01]

·    BldGndCleaningMaintenance [0.2, ~0.0]

·    ProdOccup [0.2, 0.03]

Note: Selected top five.

**b) Income:** The ranges that had the highest acceptance and the lowest rejections are (in no specific order):

·    ~$12K [0.15, 0.05], ~18K [0.14, 0.05], ~31K [0.15, 0.04]

·    ~56K [14, 0.04] Note: Selected top four

**c) Education:** The education level that had the highest acceptance and the lowest rejections are (in no specific order):

·    Some Highschool [0.17, 0.01]

·    Associate degree [0.15, 0.03] Note: Selected top two

**d) MaritalStatus** Marital status that had the highest acceptance and the lowest rejections are (in no specific order):

·    Widowed [0.16, 0.03]

Based on these findings from the conditional plots, complex conditionals is defined by taking more than one features/characteristics. This approach will help to understand the interrelationship between these participants with the top acceptance.



### 4.2   Identify Opportunities - Acceptance Rate Improvement  

Based on the observation in section 4.1.5.1 and taking into account findings in section 4.1.4.1, define possible opportunities and identify attributes to execute complex conditional probability based the analysis. 

The attributes identified in section 4.1.4 has relatively higher probability of rejection to the attributes identified in section 4.1.5. This means that there are two approaches that can be taken to improve the chance of the acceptance rate:

a) Reduce the rate of rejection in the attributes identified in section 4.1.4

OR / AND

b) Given a high acceptance relative to the rejection rate, increase the number of offers to the population with attributes identified in section 4.1.5. 

Following are the refined attributes to investigate (as an example approach):

A - Passanger Type - Alone

B - Education - Some College or Bachelors or Graduate degree

C - Age - < 37 years of age

D - Occupation - Unemployed or Student

E - Marital Status - Single or Divorced

F - Combination - (Single or Divorced) and (Unemployed)

G - Combination - (Single or Married) & (Bachelors or Graduate degree) & (< 37 years of age)

Note: This is an example to demonstrate the strategy behind selection of the attributes and their combination, understanding the key characteristics to help drive down the rejection rate.  



### 4.2.1   Complex Conditional Probability of Acceptance 

Conditional probability of acceptance given the following defined conditionals:

A - Coupon acceptance rate per condition

B - Passanger Type - Alone

C - Education - Some College or Bachelors or Graduate degree

D - Age - < 37 years of age

E - Occupation - Unemployed or Student

F - Marital Status - Single or Divorced

G - Combination - (Single or Divorced) and (Unemployed)

H - Combination - (Single or Married) & (Bachelors or Graduate degree) & (< 37 years of age)

I - Combination - (Single or Divorced) & (Bachelors or Graduate degree) & (< 37 years of age)

Figure 9 provides the results of the following conditional probabilities:

​    1. P(A|B)

​    2. P(A|C)

​    3. P(A|D)

​    4. P(A|E)

​    5. P(A|F)

​    6. P(A|G)

​    7. P(A|H)

   8. P(A|I)

      

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/histplot_complex_con_probability_coupon_attributes.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/histplot_complex_con_probability_coupon_attributes.png) 

**Figure 9 - Probability of accepting & rejecting offers base on complex condition**



### 5.0   Summary

The conditional probability plots in section 8.2.4 provide insightful information. The results can be viewed from two angles:

a) likelihood of acceptance of CarryAway relative to other coupon types, given a single driver/passenger characteristic.

b) likelihood of acceptance of CarryAway relative to other coupon types, given a combination of driver/passenger characteristics.

The first subplot which is the output of a single driver/passenger characteristic condition ("Passange == Alone") yields a lower likelihood of acceptance 0.73 compared to the last subplot where the condition takes multiple driver/passenger characteristics into account (complex condition), with a likelihood of 0.76. The last two subplots, based on complex condition, yields a difference of 0.03 acceptance likelihood. This shows that it is important to understand the interrelationship between the driver/passenger characteristics to derive the right combination, maximizing the acceptance rate of the coupon campaign. 

If the business decide to increase the number of coupons distribution then this approach will help identify the appropriate target audience. The business can take the approach of “right mix of driver/passenger characteristics” distribution, proportional to the coupon category. In other words, the coupon distribution campaign will be targeted to participants who fit the defined combination of driver/passenger characteristics. This in turn will reduce wastage in coupon production and distribution overhead costs while maximizing acceptance rate revenue. 

Additionally, to further improve the acceptance rate, the analysis based on complex conditional likelihood can focus on reducing the rejection rate by identifying driver/passenger characteristics of the population who would be excluded from offers of a specific type of coupon. 



### 6.0   Next Steps

The insights gained from the data analysis and the conditional probability approach provided, sets the stage for this study to be followed up with the next phase, i.e., to start creating model to find pattern inside our data and to make future prediction for business purpose. As part of the next steps, additional steps maybe taken to fine-tune the definition of the conditions, based on driver's inter-characteristics/features, to maximize acceptance rate and reduce rejection rate across the coupon category.
