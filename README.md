Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.



Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:

Select Count(*)
From Table Name
	
i. Attribute table =10000
ii. Business table = 10000
iii. Category table = 10000
iv. Checkin table = 10000
v. elite_years table = 10000
vi. friend table = 10000
vii. hours table = 10000
viii. photo table = 10000
ix. review table = 10000
x. tip table = 10000
xi. user table =10000
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

SELECT COUNT(DISTINCT(key))
FROM table

i.      Business            = id: 10000
ii.     Hours               = business_id: 1562
iii.    Category            = business_id: 2643
iv.     Attribute           = business_id: 1115
v.      Review              = id:10000, business_id: 8090, user_id: 9581
vi.     Checkin             = business_id: 493
vii.    Photo               = id: 10000, business_id: 6493
viii.   Tip                 = user_id: 537, business_id: 3979
ix.     User                = id: 10000
x.      Friend              = user_id: 11
xi.     Elite_years         = user_id: 2780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer: No
	
	
	SQL code used to arrive at answer:
Select *
From User
Where Name IS NUll OR
id IS NUll OR
review_count IS NUll OR
useful IS NUll OR
funny IS NUll OR
cool IS NUll OR
fans IS NUll OR
average_stars IS NUll OR
compliment_hot IS NUll OR
compliment_more IS NUll OR
compliment_profile IS NUll OR
compliment_cute IS NUll OR
compliment_list IS NUll OR
compliment_note IS NUll OR
compliment_plain IS NUll OR
compliment_cool IS NUll OR
compliment_funny IS NUll OR
compliment_writer IS NUll OR 
compliment_photos IS NUll 
	
	

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

Select Min(Stars), Max(Stars), Avg(Stars)
From Review
	
i. Table: Review, Column: Stars
	
		min:1		max:5		avg:3.7082
		
	
	ii. Table: Business, Column: Stars
	
		min:1		max:5		avg:3.6549
		
	
	iii. Table: Tip, Column: Likes
	
		min:0		max:2		avg:.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min:1		max:53		avg:1.9414
		
	
	v. Table: User, Column: Review_count
	
		min:0		max:2000		avg:24.2995
		


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
SELECT city, SUM(review_count) AS reviews
    FROM business
    GROUP BY city
    ORDER BY reviews DESC
	
	Copy and Paste the Result Below:
 city            | reviews |
+-----------------+---------+
| Las Vegas       |   82854 |
| Phoenix         |   34503 |
| Toronto         |   24113 |
| Scottsdale      |   20614 |
| Charlotte       |   12523 |
| Henderson       |   10871 |
| Tempe           |   10504 |
| Pittsburgh      |    9798 |
| Montréal        |    9448 |
| Chandler        |    8112 |
| Mesa            |    6875 |
| Gilbert         |    6380 |
| Cleveland       |    5593 |
| Madison         |    5265 |

	
6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:
 SELECT stars AS [star rating], SUM(review_count) AS count
    FROM business
    WHERE city == 'Avon'
    GROUP BY stars


Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
+-------------+-------+
| star rating | count |
+-------------+-------+
|         1.5 |    10 |
|         2.5 |     6 |
|         3.5 |    88 |
|         4.0 |    21 |
|         4.5 |    31 |
|         5.0 |     3 |
+-------------+-------+


ii. Beachwood

SQL code used to arrive at answer:
 SELECT stars AS [star rating], SUM(review_count) AS count
    FROM business
    WHERE city == 'Beachwood'
    GROUP BY stars


Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):

+-------------+-------+
| star rating | count |
+-------------+-------+
|         2.0 |     8 |
|         2.5 |     3 |
|         3.0 |    11 |
|         3.5 |     6 |
|         4.0 |    69 |
|         4.5 |    17 |
|         5.0 |    23 |
+-------------+-------+
		


7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
SELECT review_count, name
 From user
 Order By review_count Desc
 Limit 3

		
	Copy and Paste the Result Below:
review_count | name   |
+--------------+--------+
|         2000 | Gerald |
|         1629 | Sara   |
|         1339 | Yuri   |
		


8. Does posting more reviews correlate with more fans?

	Please explain your findings and interpretation of the results: Yes Generally more reveiws leads to more fans

 SELECT review_count, name, fans
  From user
 Order By fans Desc
 Limit 25
	
review_count | name      | fans |
+--------------+-----------+------+
|          609 | Amy       |  503 |
|          968 | Mimi      |  497 |
|         1153 | Harald    |  311 |
|         2000 | Gerald    |  253 |
|          930 | Christine |  173 |
|          813 | Lisa      |  159 |
|          377 | Cat       |  133 |
|         1215 | William   |  126 |
|          862 | Fran      |  124 |
|          834 | Lissa     |  120 |
|          861 | Mark      |  115 |
|          408 | Tiffany   |  111 |
|          255 | bernice   |  105 |
|         1039 | Roanna    |  104 |
|          694 | Angela    |  101 |
|         1246 | .Hon      |  101 |
|          307 | Ben       |   96 |
|          584 | Linda     |   89 |

	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer: Love  1780 > Hate 232

	
	SQL code used to arrive at answer:
 SELECT Count(text)
  From review
Where Text LIKE "%Hate%" 

 SELECT Count(text)
  From review
Where Text LIKE "%Love%" 

	
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
 SELECT fans, id, name
  From user
Order BY fans DESC
Limit 10
	
	
	Copy and Paste the Result Below:
 fans | id                     | name      |
+------+------------------------+-----------+
|  503 | -9I98YbNQnLdAmcYfb324Q | Amy       |
|  497 | -8EnCioUmDygAbsYZmTeRQ | Mimi      |
|  311 | --2vR0DIsmQ6WfcSzKWigw | Harald    |
|  253 | -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |
|  173 | -0IiMAZI2SsQ7VmyzJjokQ | Christine |
|  159 | -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |
|  133 | -9bbDysuiWeo2VShFJJtcw | Cat       |
|  126 | -FZBTkAZEXoP7CYvRV2ZwQ | William   |
|  124 | -9da1xk7zgnnfO1uTVYGkA | Fran      |
|  120 | -lh59ko3dxChBSZ9U7LfUw | Lissa     |
+------+------------------------+-----------+
		

Part 2: Inferences and Analysis

1. Pick one city (Las Vegas) and category (Shopping) of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
i. Do the two groups you chose to analyze have a different distribution of hours?
  No, there is not a noticeable difference in hours broken down by star rating mostly due to small sample size


ii. Do the two groups you chose to analyze have a different number of reviews?

 Yes generally higher stars equals more reviews, but again the sample size is not big enough to discern with high insight
         
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.
  No. Neighborhood data is only provided for half of the rows so it's not a representative sample. 

SQL code used for analysis:

SELECT name, category, neighborhood, stars, review_count, city, hours
  From business
  INNER Join category
  ON business.id = category.business_id
  INNER Join hours
  ON business.id = hours.business_id
  WHERE category == "Shopping" AND
  city LIKE "Las Vegas"
  Group By stars
  Order By stars DESC
LIMIT 100
		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
         The businesses still open tend to have high review counts  2 out of the top 25 results are Closed
         
ii. Difference 2:
 The businesses still open have higher STARS  2 out of the top 25 results are Closed
         
         
         
SQL code used for analysis:

SELECT is_open, review_count, name, neighborhood, city, stars
From Business
Where city LIKE "Las Vegas" 
Order By stars DESC, review_count DESC  
LIMIT 100

	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
i. 	Indicate the type of analysis you chose to do:
	
		Predicting whether a business will stay open or close. 
	
ii.	Write 1-2 brief paragraphs on the type of data you will need for your analysis
		and why you chose that data:
		
	---	In order to understand the importance of different factors which
		will help their business stay open. 
        
        Some column field may be important such as 
        number of reviews, star rating of business, hours open, and location.
		
   ---     In addition, it would be nice to  gather the latitude and longitude, city, state, 
		postal_code, and address to make processing easier later on. 
        
        Attributes as well as categories is used to better distinguish 
        between different types of businesses. 
		
iii.	Output of your finished dataset:


+--------------------------------+-----------------------------+---------------+-------+-------------+----------+-----------+--------------+-------+--------------+---------------+-----------------+----------------+--------------+----------------+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+
| name                           | address                     | city          | state | postal_code | latitude | longitude | review_count | stars | monday_hours | tuesday_hours | wednesday_hours | thursday_hours | friday_hours | saturday_hours | sunday_hours | categories                                                                                                                                                                                                 | attributes                                                                                                                                                                                                                                                                                                                          | is_open |
+--------------------------------+-----------------------------+---------------+-------+-------------+----------+-----------+--------------+-------+--------------+---------------+-----------------+----------------+--------------+----------------+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+
| Flaming Kitchen                | 3235 York Regional Road 7   | Markham       | ON    | L3R 3P9     |  43.8484 |  -79.3487 |           25 |   3.0 | 12:00-23:00  | 12:00-23:00   | 12:00-23:00     | 12:00-23:00    | 12:00-23:00  | 12:00-23:00    | 12:00-23:00  | Asian Fusion,Restaurants                                                                                                                                                                                   | RestaurantsTableService,GoodForMeal,Alcohol,Caters,HasTV,RestaurantsGoodForGroups,NoiseLevel,WiFi,RestaurantsAttire,RestaurantsReservations,OutdoorSeating,RestaurantsPriceRange2,BikeParking,RestaurantsDelivery,Ambience,RestaurantsTakeOut,GoodForKids,BusinessParking                                                           |       1 |
| Freeman's Car Stereo           | 4821 South Blvd             | Charlotte     | NC    | 28217       |  35.1727 |  -80.8755 |            8 |   3.5 | 9:00-19:00   | 9:00-19:00    | 9:00-19:00      | 9:00-19:00     | 9:00-19:00   | 9:00-17:00     | None         | Electronics,Shopping,Automotive,Car Stereo Installation                                                                                                                                                    | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,WheelchairAccessible                                                                                                                                                                                                                                              |       1 |
| Motors & More                  | 2315 Highland Dr            | Las Vegas     | NV    | 89102       |  36.1465 |  -115.167 |            7 |   5.0 | 7:00-17:00   | 7:00-17:00    | 7:00-17:00      | 7:00-17:00     | 7:00-17:00   | 8:00-12:00     | None         | Home Services,Solar Installation,Heating & Air Conditioning/HVAC                                                                                                                                           | BusinessAcceptsCreditCards,BusinessAcceptsBitcoin,ByAppointmentOnly                                                                                                                                                                                                                                                                 |       1 |
| Baby Cakes                     | 4145 Erie St                | Willoughby    | OH    | 44094       |  41.6399 |  -81.4064 |            5 |   3.5 | None         | 11:00-17:00   | 11:00-17:00     | 11:00-20:00    | 11:00-17:00  | 10:00-17:00    | None         | Bakeries,Food                                                                                                                                                                                              | BusinessAcceptsCreditCards,RestaurantsTakeOut,WheelchairAccessible,RestaurantsDelivery                                                                                                                                                                                                                                              |       1 |
| Snip-its Rocky River           | 21609 Center Ridge Rd       | Rocky River   | OH    | 44116       |  41.4595 |  -81.8587 |           18 |   2.5 | 10:00-19:00  | 10:00-19:00   | 10:00-19:00     | 10:00-19:00    | 10:00-19:00  | 9:00-17:30     | 10:00-16:00  | Beauty & Spas,Hair Salons                                                                                                                                                                                  | BusinessAcceptsCreditCards,RestaurantsPriceRange2,GoodForKids,BusinessParking,ByAppointmentOnly                                                                                                                                                                                                                                     |       1 |
| Standard Restaurant Supply     | 2922 E McDowell Rd          | Phoenix       | AZ    | 85008       |  33.4664 |  -112.018 |           15 |   3.5 | 8:00-18:00   | 8:00-18:00    | 8:00-18:00      | 8:00-18:00     | 8:00-18:00   | 9:00-17:00     | None         | Shopping,Wholesalers,Restaurant Supplies,Professional Services,Wholesale Stores                                                                                                                            | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,BikeParking,WheelchairAccessible                                                                                                                                                                                                                                  |       1 |
| What A Bagel                   | 973 Eglinton Avenue W       | York          | ON    | M6C 2C4     |  43.6999 |  -79.4295 |            8 |   3.0 | 6:00-15:30   | 6:00-15:30    | 6:00-15:30      | 6:00-15:30     | 6:00-15:30   | 6:00-15:30     | None         | Restaurants,Bagels,Breakfast & Brunch,Food                                                                                                                                                                 | NoiseLevel,RestaurantsAttire,RestaurantsTableService,OutdoorSeating                                                                                                                                                                                                                                                                 |       1 |
| Pinnacle Fencing Solutions     |                             | Phoenix       | AZ    | 85060       |  33.4805 |  -111.997 |           13 |   4.0 | 8:00-16:00   | 8:00-16:00    | 8:00-16:00      | 8:00-16:00     | 8:00-16:00   | None           | None         | Home Services,Contractors,Fences & Gates                                                                                                                                                                   | BusinessAcceptsCreditCards,ByAppointmentOnly                                                                                                                                                                                                                                                                                        |       1 |
| Alterations Express            | 17240 Royalton Rd           | Strongsville  | OH    | 44136       |  41.3141 |  -81.8207 |            3 |   4.0 | 8:00-19:00   | 8:00-19:00    | 8:00-19:00      | 8:00-19:00     | 8:00-19:00   | 8:00-18:00     | None         | Shopping,Bridal,Dry Cleaning & Laundry,Local Services,Sewing & Alterations                                                                                                                                 | BusinessParking,BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessAcceptsBitcoin,BikeParking,ByAppointmentOnly,WheelchairAccessible                                                                                                                                                                                         |       1 |
| Extra Space Storage            | 2880 W Elliot Rd            | Chandler      | AZ    | 85224       |  33.3496 |  -111.892 |            5 |   4.0 | 8:00-17:30   | 8:00-17:30    | 8:00-17:30      | 8:00-17:30     | 8:00-17:30   | 8:00-17:30     | 10:00-14:00  | Home Services,Self Storage,Movers,Shopping,Local Services,Home Decor,Home & Garden                                                                                                                         | BusinessAcceptsCreditCards                                                                                                                                                                                                                                                                                                          |       1 |
| Gussied Up                     | 1090 Bathurst St            | Toronto       | ON    | M5R 1W5     |  43.6727 |  -79.4142 |            6 |   4.5 | None         | 11:00-19:00   | 11:00-19:00     | 11:00-19:00    | 11:00-19:00  | 11:00-17:00    | 12:00-16:00  | Women's Clothing,Shopping,Fashion                                                                                                                                                                          | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,BikeParking                                                                                                                                                                                                                                                       |       1 |
| Buddy's Muffler & Exhaust      | 1509 Hickory Grove Rd       | Gastonia      | NC    | 28056       |  35.2772 |    -81.06 |            4 |   5.0 | 8:30-17:00   | 8:30-17:00    | 8:30-17:00      | 8:30-17:00     | 8:30-17:00   | 9:00-15:00     | None         | Automotive,Auto Repair                                                                                                                                                                                     | BusinessAcceptsCreditCards                                                                                                                                                                                                                                                                                                          |       1 |
| Five Guys                      | 2641 N 44th St, Ste 100     | Phoenix       | AZ    | 85008       |   33.478 |  -111.986 |           63 |   3.5 | 10:00-22:00  | 10:00-22:00   | 10:00-22:00     | 10:00-22:00    | 10:00-22:00  | 10:00-22:00    | 10:00-22:00  | American (New),Burgers,Fast Food,Restaurants                                                                                                                                                               | RestaurantsTableService,GoodForMeal,Alcohol,Caters,HasTV,RestaurantsGoodForGroups,NoiseLevel,WiFi,RestaurantsAttire,RestaurantsReservations,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,BikeParking,RestaurantsDelivery,Ambience,RestaurantsTakeOut,GoodForKids,DriveThru,BusinessParking                      |       1 |
| All Storage - Anthem           | 2620 W Horizon Ridge Pkwy   | Henderson     | NV    | 89052       |  36.0021 |  -115.102 |            3 |   3.5 | 9:00-16:30   | 9:00-16:30    | 9:00-16:30      | 9:00-16:30     | 9:00-16:30   | 9:00-16:30     | None         | Truck Rental,Local Services,Self Storage,Parking,Automotive                                                                                                                                                | BusinessAcceptsCreditCards,BusinessAcceptsBitcoin                                                                                                                                                                                                                                                                                   |       1 |
| Mood                           | 1 Greenside Place           | Edinburgh     | EDH   | EH1 3AA     |   55.957 |  -3.18502 |           11 |   2.0 | None         | None          | None            | 22:30-3:00     | 22:00-3:00   | 22:00-3:00     | 22:30-3:00   | Dance Clubs,Nightlife                                                                                                                                                                                      | Alcohol,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,AgesAllowed,Music,Smoking,RestaurantsGoodForGroups,WheelchairAccessible                                                                                                                                                                                    |       0 |
| Starbucks                      | 4605 E Chandler Blvd, Ste A | Phoenix       | AZ    | 85048       |  33.3044 |  -111.984 |           52 |   3.0 | 5:00-20:00   | 5:00-20:00    | 5:00-20:00      | 5:00-20:30     | 5:00-20:00   | 5:00-20:00     | 5:00-20:00   | Coffee & Tea,Food                                                                                                                                                                                          | BusinessParking,Caters,WiFi,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,BikeParking,RestaurantsTakeOut                                                                                                                                                                                                         |       1 |
| Big Smoke Burger               | 260 Yonge Street            | Toronto       | ON    | M4B 2L9     |  43.6546 |  -79.3805 |           47 |   3.0 | 10:30-21:00  | 10:30-21:00   | 10:30-21:00     | 10:30-21:00    | 10:30-21:00  | 10:30-21:00    | 11:00-19:00  | Poutineries,Burgers,Restaurants                                                                                                                                                                            | RestaurantsTableService,GoodForMeal,Alcohol,Caters,HasTV,RestaurantsGoodForGroups,NoiseLevel,WiFi,RestaurantsAttire,RestaurantsReservations,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,WheelchairAccessible,BikeParking,RestaurantsDelivery,Ambience,RestaurantsTakeOut,GoodForKids,DriveThru,BusinessParking |       1 |
| Subway                         | 2904 Yorkmont Rd            | Charlotte     | NC    | 28208       |  35.1903 |  -80.9288 |            7 |   3.5 | 6:00-22:00   | 6:00-22:00    | 6:00-22:00      | 6:00-22:00     | 6:00-22:00   | 10:00-21:00    | None         | Fast Food,Restaurants,Sandwiches                                                                                                                                                                           | Ambience,RestaurantsPriceRange2,GoodForKids                                                                                                                                                                                                                                                                                         |       1 |
| Red Rock Canyon Visitor Center | 1000 Scenic Loop Dr         | Las Vegas     | NV    | 89161       |  36.1357 |  -115.428 |           32 |   4.5 | 8:00-16:30   | 8:00-16:30    | 8:00-16:30      | 8:00-16:30     | 8:00-16:30   | 8:00-16:30     | 8:00-16:30   | Education,Visitor Centers,Professional Services,Special Education,Local Services,Community Service/Non-Profit,Hotels & Travel,Travel Services,Gift Shops,Shopping,Parks,Hiking,Flowers & Gifts,Active Life | BusinessAcceptsCreditCards,GoodForKids                                                                                                                                                                                                                                                                                              |       1 |
| Scent From Above Company       | 2501 W Behrend Dr, Ste 67   | Scottsdale    | AZ    | 85027       |  33.6656 |  -112.111 |           14 |   4.5 | 6:00-16:00   | 6:00-16:00    | 6:00-16:00      | 6:00-16:00     | 6:00-16:00   | None           | None         | Home Cleaning,Local Services,Professional Services,Carpet Cleaning,Home Services,Office Cleaning,Window Washing                                                                                            | BusinessAcceptsCreditCards,ByAppointmentOnly                                                                                                                                                                                                                                                                                        |       1 |
| The Charlotte Room             | 19 Charlotte Street         | Toronto       | ON    | M5V 2H5     |  43.6466 |  -79.3938 |           10 |   3.5 | 15:00-1:00   | 15:00-1:00    | 15:00-1:00      | 15:00-1:00     | 15:00-2:00   | 18:00-2:00     | None         | Event Planning & Services,Bars,Nightlife,Lounges,Pool Halls,Venues & Event Spaces                                                                                                                          | BusinessParking,HasTV,CoatCheck,NoiseLevel,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,Music,WheelchairAccessible,Smoking,Ambience,BestNights,RestaurantsGoodForGroups,HappyHour,GoodForDancing,Alcohol                                                                                                        |       0 |
| PC Savants                     | 11966 W Candelaria Ct       | Sun City      | AZ    | 85373       |  33.6901 |  -112.319 |           11 |   5.0 | 10:00-19:00  | 10:00-19:00   | 10:00-19:00     | 10:00-19:00    | 10:00-19:00  | 11:00-18:00    | 11:00-18:00  | IT Services & Computer Repair,Electronics Repair,Local Services,Mobile Phone Repair                                                                                                                        | BusinessAcceptsCreditCards,BusinessAcceptsBitcoin                                                                                                                                                                                                                                                                                   |       1 |
| Sweet Ruby Jane Confections    | 8975 S Eastern Ave, Ste 3-B | Las Vegas     | NV    | 89123       |   36.015 |  -115.118 |           30 |   4.0 | 10:00-19:00  | 10:00-19:00   | 10:00-19:00     | 10:00-19:00    | 10:00-19:00  | 10:00-19:00    | None         | Food,Chocolatiers & Shops,Bakeries,Specialty Food,Desserts                                                                                                                                                 | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,WheelchairAccessible                                                                                                                                                                                                                                              |       0 |
| Oinky's Pork Chop Heaven       | 22483 Emery Rd              | North Randall | OH    | 44128       |  41.4352 |  -81.5214 |            3 |   3.0 | 6:00-23:00   | 6:00-23:00    | 6:00-23:00      | 6:00-23:00     | 6:00-23:00   | 6:00-23:00     | 6:00-23:00   | Soul Food,Restaurants                                                                                                                                                                                      | RestaurantsAttire,RestaurantsGoodForGroups,GoodForKids,RestaurantsReservations,RestaurantsTakeOut                                                                                                                                                                                                                                   |       1 |
| Sushi Osaka                    | 5084 Dundas Street W        | Toronto       | ON    | M9A 1C2     |  43.6452 |  -79.5324 |            8 |   4.5 | 11:00-23:00  | 11:00-23:00   | 11:00-23:00     | 11:00-23:00    | 11:00-23:00  | 11:00-23:00    | 14:00-23:00  | Sushi Bars,Restaurants,Japanese,Korean                                                                                                                                                                     | RestaurantsTakeOut,WiFi,RestaurantsGoodForGroups,RestaurantsReservations                                                                                                                                                                                                                                                            |       1 |
+--------------------------------+-----------------------------+---------------+-------+-------------+----------+-----------+--------------+-------+--------------+---------------+-----------------+----------------+--------------+----------------+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+
(Output limit exceeded, 25 of 70 total rows shown)


	iv. 	Provide the SQL code you used to create your final dataset:
	
		SELECT Bu.name, Bu.address, Bu.city, Bu.state, Bu.postal_code,
			   Bu.latitude, Bu.longitude, Bu.review_count, Bu.stars,
			   MAX(CASE
			   WHEN H.hours LIKE "%monday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS monday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%tuesday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS tuesday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%wednesday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS wednesday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%thursday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS thursday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%friday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS friday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%saturday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS saturday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%sunday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS sunday_hours,
			   GROUP_CONCAT(DISTINCT(C.category)) AS categories,
			   GROUP_CONCAT(DISTINCT(A.name)) AS attributes,
			   Bu.is_open
		FROM business Bu
		INNER JOIN hours H
		ON Bu.id = H.business_id
		INNER JOIN category C
		ON Bu.id = C.business_id
		INNER JOIN attribute A
		ON Bu.id = A.business_id
		GROUP BY Bu.id
