# Case Study : Conditional Acceptance of Coupon

**Context**

Using the CRISP-DM model (as shown in Figure 1), the likelihood of customers acceptance of coupons during coupon campaigns run by the hospitality industry will be studied. In the series of studies, this is the first part of the study which focuses on all the phases covering up to "Data Preparation" phase of the CRISP-DM-DM.

 ![CRISP-DM.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/CRISP-DM.png) 

**Figure 1 - CRISP-DM process model**



# 1 Business Understanding

## 1.1 Background

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? 

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? What  are the relevant characteristics of the driver who is likely to accept a coupon?



 ![bar_coupon_types_dist.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/bar_coupon_types_dist.png) 

**Figure 2 - Distribution of coupons by type**



Figure 2 provides a view of the distribution of the coupons offered to participants across the different types of business within the hospitality industry. The discribution in Figure 2 shows that the coupon campaign is skewed heavily towards the Coffee House businesses.



![bar_accept_reject_coupon_types_dist.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/bar_accept_reject_coupon_types_dist.png) 

**Figure 3 - Distribution of accepted & rejected coupons by type**



Figure 3 - provides a view of the distribution accepted and rejected offers across the entire coupon category. The figure highlights the coupon types that have the highest acceptance and rejection rates, providing a view of where improvements are needed.



In summary, the business problem is as follows:

- Identify apportunities to improve acceptance rates of Bar and Coffee House based on the acceptance rate of the Carry out & Take away coupon.

- Identification of opportunities includes understanding the characteristics of the drivers with high acceptance rate.

   



## 1.2 Business Goals and KPI

The business goal is to:

- Gain insight on which one or more driver characteristics would yield high acceptance rate.

- Reduce cost of rejected coupon (by eliminating production and distribution cost incurred during coupon campaigns)

  

# 2 Data Understanding

On the **Data Understanding** phase, the data is described and explored to make sure it fits the business goals.



## 2.1 Gathering and Describing Data

This data comes from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50).

Here is a sample of the data.

![original.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/original.png?raw=true)



The information about the structure of the data including:

- The number of rows (each row represent a single response data)
- The number of column
- The name of each column
- The data type of each column



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

Next step is to check the quality of the data. For example, since many of the column/variable is categorical, the summary of the data can be checked for the types in each categories. By doing this, the step needed for data cleaning or to be transformed is identified. For example, check for missing/empty values.

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


Following is the catagory of each column that is of type object:

 ![AIML-Portfolio-Likelihood-Accepting-Coupon/images/table1.png at main · bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/table1.png) 



Following is the percentage of missing values per column:

**car					99.15%**

**Bar					0.84%**

**CoffeeHouse			1.71%**

**CarryAway                           1.19%**

**RestaurantLessThan20    1.02%**

**Restaurant20To50             1.49%**



Finally, The number of **duplicate rows are 74**.



There are some interesting finding from the summary. For example, the there are a few columns like`car` that have nan (Unknown). The `expiration` column constains time in days and hours. The columns like`Bar` has ranges, for example, 4-8 or gt8, etc. The `occupation`column has very large stings. As a result, the data need to be cleansed and transformed followed by preparation before any analysis can be executed, so that all relevant information can be captured.



# 3 Data Preparation

On the **Data Understanding** phase, the data is prepared and cleansed to allow for analysis in this as part of this case study and future case studies covering predictions.  



## 3.1 Data Transformation

Following data attributes that will to be treated:

a) passanger - convert "Kid(s)" -> "Kid" & "Friend(s)" -> Friend

b) time - convert AM/PM format to military (24-hour) time (integer).

c) expiration - convert from day to hours (integer)

d) age - normalize to integers

e) income - for each range convert the average (integer)

f) Bar/CoffeeHouse/ResturantLessThan20/Resturant20To50 - convert to integers

g) Shorten occupation strings



## 3.2 Data Cleansing

On this process,  the data is handled based on the problem found during the data understanding phase. Based on the finding, the following process is executed:

a) If the percentage of missing values, per column, is >= 70%, then we will drop the entire column.

b) If the percentage of missing values, per column, is < 30%, then keep the column and evaluate.

c) For columns with missing values > 10%, the values will be filled using interpolation technique or mean or media or mode. Will depend on the data charastics. 

d) For columns with missing data <= 10%, the associated row will simply be dropped.

e) Finally, find and drop duplicate rows



Post cleaning data view:
Index: 12007 entries, 22 to 12683
Data columns (total 25 columns):

 #    

**Column				Non-Null Count 			Type**	

---  ------                --------------  -----
 **0   destination           		12007 non-null  			object 
 1   passanger             		12007 non-null  			object 
 2   weather               		  12007 non-null  			object 
 3   temperature           	      12007 non-null                          int64  
 4   time                  		      12007 non-null 		        int64  
 5   coupon                		  12007 non-null  			object 
 6   expiration            		 12007 non-null  		        int64  
 7   gender                		  12007 non-null  		         object 
 8   age                   		      12007 non-null  			int64  
 9   maritalStatus         	       12007 non-null  			object 
 10  has_children          	      12007 non-null  			int64  
 11  education             		12007 non-null  			object 
 12  occupation            		12007 non-null  		      object 
 13  income                		  12007 non-null  		       int64  
 14  Bar                   		      12007 non-null  		       float64
 15  CoffeeHouse           	     12007 non-null  		       float64
 16  CarryAway             		12007 non-null  		      float64
 17  RestaurantLessThan20       12007 non-null  		      float64
 18  Restaurant20To50      	 12007 non-null  	              float64
 19  toCoupon_GEQ5min            12007 non-null  		     int64  
 20  toCoupon_GEQ15min          12007 non-null  		     int64  
 21  toCoupon_GEQ25min          12007 non-null 		      int64  
 22  direction_same        	     12007 non-null  		      int64  
 23  direction_opp         	       12007 non-null  	              int64  
 24  Y                     			  12007 non-null  		      int64  
dtypes: float64(5), int64(12), object(8)**



After the data clean process was executed, the columns was reduced from **26 to 25** and the rows were reduced from **12683 to 12007**, i.e., As part of the cleaning process, number of rows are reduced by: **5.33%**.



## 3.3 Final Data

![image-20240303004736785.png](https://github.com/bhaswarey/AIML-Portfolio-Likelihood-Accepting-Coupon/blob/main/images/image-20240303004736785.png?raw=true)



# 4 Data Understanding (Deeper Analysis)

Further explore and analyze of the data is conducted in preparation for future machine learning model.



## 4.1 Exploratory Data Analysis

In this section, the results of exploring and visualizing insight from the data is captured.



### 4.1.1 Coupon Campaigns & Temperature

Figure 4 provide the temperature distribution covering the coupon offer campaigns.











