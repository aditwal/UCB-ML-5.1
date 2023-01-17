**UCB-ML&AI Practical Application Assignment 5.1**

### Will a Customer Accept the Coupon?

**Context**

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? How would you determine whether a driver is likely to accept a coupon?

**Problem Statement**

The goal of this project is to use visualizations and probability distributions to distinguish between customers who accepted a driving coupon versus those that did not.

**Deliverables**

A brief report that highlights the differences between customers who did and did not accept the coupons by exploring data utilizing knowledge of plotting, statistical summaries, and visualization using Python.

**Data**

This data comes from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50). 

Note: these values mentioned below are average values.

The attributes of this data set include:
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

**Analysis Notebook**

The data exploration, cleaning and analysis is performed in the Jupyter notebook 'coupon analysis.ipynb'. 

**Data Exploration and Cleaning**

Data contains 12684 rows of 25 attributes and 1 response. Column 'car' has only 108 non-null values. So it may not be useful for analysis. 605 rows has some attributes with null values. Dropping the column 'car' and rows with null values, the usable data in the dataset has 12079 rows of 24 attributes and 1 response. 

Digging deeper by looking at value counts for all the categorical attributes, it reveals 

1. Columns 'age' describes a range but the values are only marked as a single number. Therefore, column 'age' was converted to a range for better readablilty. Furthermore, a new column is added with the first integer value of the range for easier analysis. 

2. Columns 'has_children' describes the number of children the user has. However, the max number is 1.  

3. Since columns 'direction_same' and 'direction_opp' are mutually exclusive, for each record only one of them should be marked as 1 and the other as 0. This was confirmed by checking if the values in the two columns are not equal in any rows. 

4. The column 'Bar_int' is added with the last integer value in the range of column 'Bar' for easier analysis

**Data analysis and visualization**

Overall, 56.94% of the users chose to accept the coupons presented to them. Figure below depicts the acceptance rate by different coupon categories as per the data. 

<img width="1035" alt="image" src="https://user-images.githubusercontent.com/90078929/212805114-5386f047-47e5-4956-8be5-76d707935072.png">

#### Investigation of bar coupons

1.  1913 drivers were presented with the 'Bar' coupons, among them 41.19% of the drivers accepted the coupons. 
2.  Acceptance rate for drivers who went to bar 3 or fewer times was only 37.27% compared to 76.17% acceptance rate for drivers who went to bar more than 3 times.  
3.  Furthemore, 68.98%  of the drivers who went to bar more than once and are over the age of 25 accepted the coupons. On the other hand, all others has only 33.77% acceptance rate.
4.  Acceptance rate for drivers who go to bar more than once and had passengers that were not a kid and had coocumpation other than farming, fishing, or forestry was 70.94%, while others had acceptance rate of 29.79%. 
5.  Acceptance rate for drivers who go to bar more than once, had passengers that were not a kid and were not widowed - 70.94%
    Acceptance rate for drivers who go to bar more than once and are under the age of 30 - 71.95%
    Acceptance rate for drivers who go to cheap restaurants more than 4times a month and income less than $50k - 45.65%

From the above analysis,it can be hypothesized that drivers who go to bar more than 3 times, are between the age of 25 and 30, had passengers that were not a kid, had coocumpation other than farming, fishing, or forestry, were not widowed are more inclined to accept the bar coupons.  

#### Investigation of coffee coupons
1.  3816 drivers were presented with the 'Coffee' coupons, among them 49.63% of the drivers accepted the coupons.
2.  Coupon acceptance rates for drivers with different Destination were as follows - 

	Destination       Acceptance rate. 
	Home               0.362613. 
	No Urgent Place    0.578178. 
	Work               0.440000. 
	
	<img width="1032" alt="image" src="https://user-images.githubusercontent.com/90078929/212858936-7f3ab386-f868-4baf-8137-7c3cfdb61b06.png">

    Based on the analysis, drivers who are going to no urgent place are more likely to accept coffee coupons. 

3.  Coupon acceptance rates for drivers travelling with different Passenger were as follows - 

   Passenger  Acceptance rate. 
   
    Alone        0.433936. 
	
    Friend(s)    0.597447. 
	
    Kid(s)       0.471503. 
	
    Partner      0.567010. 
	
	
	<img width="1038" alt="image" src="https://user-images.githubusercontent.com/90078929/212859156-85f4a176-c45c-4ec4-b40e-628d5b40a7ff.png">
	
	It can be observed that drivers travelling with friends or partner are more likely to accept the coffee coupons.

4.  Effect of the time on the coupon acceptance rates - 

	Time  Acceptance rate
	
    7AM     0.440000. 
	
    10AM    0.634772. 
	
    2PM     0.545455. 
	
    6PM     0.412272. 
	
    10PM    0.429078. 
	

	<img width="1040" alt="image" src="https://user-images.githubusercontent.com/90078929/212859299-37539d1a-ca6f-446c-a3b7-ffe6c126b782.png">

	It can be seen that drivers in the morning are more likely to accept coffee coupon.

5.  Coupon acceptance rates for drivers based on how frequently they visit the coffeehouse were as follows - 

	Coffehouse Freq   Acceptance rate. 
	
    1~3              0.647694. 
	
    4~8              0.682446. 
	
    gt8              0.657895. 
	
    less1            0.480989. 
	
    never            0.175223. 
	

	<img width="1035" alt="image" src="https://user-images.githubusercontent.com/90078929/212859519-96e0c78e-07cf-4036-a944-91113658cd5f.png">

	Based on the analysis, drivers who go to coffeehouse at least once are more likely to accept coffee coupons

6.  By intuition, the Drivers are more likely to accept coffee coupons for the venue in the same direction. The data also shows the same. 

    direction_same:	0.526536. 
	
	direction_opp:	0.489355. 

7.  The data also shows that students are more likely to be accept the coffee coupons. Similar results can be seen if education of the drivers are considered. 'Some High School' and 'High School Graduate' who are more likely to be students have more acceptance rate for coffee coupons. The same conclusion can also be arrived when age is considered. Acceptance rates for drivers of age less than 20 years are significantly higher than the other groups. 

    Occupation: Student                 > Acceptance rate: 0.614737.
	
    Education: High School Graduate     > Acceptance rate: 0.540441. 
	
    Education: Some High School         > Acceptance rate: 0.607143. 
	
    Age: 0-20                           > Acceptance rate: 0.678322. 
	

    <img width="1038" alt="image" src="https://user-images.githubusercontent.com/90078929/212859858-692ab8a9-3759-4680-a022-7e31402247b7.png">

    <img width="1045" alt="image" src="https://user-images.githubusercontent.com/90078929/212860908-c5455c09-d8f9-4d64-a21e-6e2f7a8a2bde.png">

    <img width="1032" alt="image" src="https://user-images.githubusercontent.com/90078929/212860978-1ecf088e-d867-4b5a-97f2-35e7327508f6.png">


8.  The data showed that gender, marital status and has_children have no effect on likelihood of accepting the coffee coupons. The same was observed in case of income as well. However, there is a interesting dip in the acceptance for income range $75000 - $87499 as shown in figure below.

Gender  Acceptance rate

Female    0.491112

Male      0.501895


Has children      Acceptance rate

0                   0.501695

1                   0.487637


Marital Status    Acceptance rate

Divorced             0.517483

Married partner      0.491132

Single               0.514362

Unmarried partner    0.470414

Widowed              0.352941

<img width="1037" alt="image" src="https://user-images.githubusercontent.com/90078929/212861243-74df65a7-b3c3-4dc7-831b-454085978e45.png">



In conclusion, Students who go to coffeehouse at least once a week traveling in the morning with friends goint to no urgent place are more likely to accept the coffee coupons. The acceptance rate for such drivers are 91.67% while only 49.37% other drivers accept coffee coupons. 

