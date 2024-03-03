# Case Study : Conditional Acceptance of Coupon

**Context**

Using the CRISP-DM model (as shown in Figure 1) is used to study the likelihood of customers acceptance of coupons during coupon campaigns run by the hospitality industry. In the series of studies, this first part of the study which focuses on all the phases covering up to "Data Preparation" phase of the CRISP-DM-DM.

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

Figure 3 - provides a view of the distribution accepted and rejected offers across the entire coupon category. The figure highlights the coupon types that have the highest acceptance and rejection rates, providing a view of where improvements are needed.





In summary, our business problem is:

- Identify apportunities to improve acceptance rates of Bar and Coffee House based on the acceptance rate of the Carry out & Take away coupon.
  - Identification of opportunities includes understanding the characteristics of the drivers with high acceptance rate.
- Identify options to improve acceptance rate and further 



## 1.2 Business Goals and KPI

The business goal is to:

- Gain insight on which driver characteristics would yield high acceptance rate.

- Reduce cost of rejected coupon (by eliminating production and distribution cost incurred during coupon campaigns)

  

# 2 Data Understanding

On the **Data Understanding** phase, we will gather, describe and explore the data to make sure it fits the business goal.

The deliverable or result of this phase should include:

- Data description

- Early data exploration report

- Data quality report

  

## 2.1 Gathering and Describing Data

This data comes to us from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50).

Here are some samples of the data.

![image-20240303004736785](/Users/haswarey/Projects/AIML/AIML/Module 5/application/AIML-Portfolio-Likelihood-Accepting-Coupon/image-20240303004736785.png)



