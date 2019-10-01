# NewYorkCityTaxi
Analysis on the June 2014 NYC Taxi Data

### An explanation of why you selected or constructed the variable you used to represent income:

For the purpose of this analysis, I simply used the total_amount column to determine the optimum days/times to be a taxi driver. While this is not what would be used for actual income (which would be closer to Total Amount – tolls – MTA tax), it does provide an easy and close approximation to the per trip income.


### Thoughtful exploration of model variables prior to modeling.

#### vendor_id: 
This was one-hot encoded to allow for additional analyses. In the end it had only a minor difference in the overall outcome, but I did not know that to start.

#### pickup_datetime: 
This was one of the primary fields used for analysis. I broke this up into dates and times separately, changing dates to day of the week and times rounded to the nearest hour. 

#### dropoff_datetime: 
Due to the strong relation to pickup_datetime, I did not use this column for this analysis. Later work would optimize the total trip time and try to have minimal gaps between fares, but not at this time.

#### passenger_count:
I analyzed this column to understand whether passenger count affected the total fare and found there was no real connection. Due to this, I decided to not use this column at this time.

#### trip_distance: 
This is useful and is fairly accurately calculated from the pickup latitude/longitude and the drop off latitude/longitude. While I did not use it for this analysis, this is something I would want to use in future analyses

#### pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude: 
These were the key fields I wanted for this analysis. While we cannot control where the passengers want to go, we can control the locations we pick the passengers up. 
While I originally planned on converting these into more human understandable addresses, the API to make this translation was too slow and inconsistent to make this change in time. To get around this, I rounded the latitudes/longitudes to the nearest hundredth of a degree, which brings us to approximately a mile radius for the trips. This was enough to allow us to generalize the data while still maintaining some semblance of accuracy.

#### rate_code: 
I did not find this column to be useful, which I was somewhat surprised by. After some consideration, the fare_amount would have the rate_code built in, so this becomes somewhat of a superfluous column.  

#### store_and_fwd_flag: 
I dropped this column as the ability for the taxi to send information to the servers is not something we need to be too concerned with. With additional time, I would look into whether this flag affected the columns with bad data present. 

#### payment_type:
While I originally thought this would be useful, I determined that if there is any correlation between the fare amount, location, and payment type, we can derive the same information from the fare amount and location by itself. May be useful for other analyses, but unneeded at this time. 

#### Fare_amount: 
After careful consideration, I decided to focus on the total_amount instead of fare_amount due to ease of use.

#### Surcharge: 
After careful consideration, I decided to focus on the total_amount instead of fare_amount due to ease of use.

#### mta_tax:
I dropped this column as it was a static value of 0.5 for every row. This is not helpful for this analysis.

#### tip_amount: 
This is a fascinating field which has a relationship to the fare_amount/distance of the trip, but for ease of use I focused on total_amount. For future analyses, I would look at optimizing tip_amounts to see how that changes ideal outcomes.

#### tolls_amount: 
After careful consideration, I decided to focus on the total_amount instead of fare_amount due to ease of use. This column is one that will skew the data slightly, but after viewing the data and how often it is present, I determined it would not skew the data enough to alter the final outcome. 

#### total_amount: 
For simplicity, I used this column for the primary metric for income. For driver income we would remove toll amounts and mta_tax, but this was an easy to use column for this problem. 


### Conclusions summarized so that a wide variety of people can understand them.

While I would love to continue to experiment in this space, I am turning the analysis in at this point. 
From this analysis, we can tell that the best time to be a taxi driver is Monday and Sunday, typically between 6PM and midnight. The best location is around midtown manhattan (roughly near Times Square and Central Park). Ideally, being a VTS driver will increase the total amount earned slightly as well.

If a driver only has 10 hours a week he can drive, he should focus on being in midtown manhattan between 6PM and 11PM Sundays and Mondays as a VTS driver.

There is a lot more work that can go into this to verify, validate, and optimize things, but this is a good place to start for now. If I had time, I would look into creating a model to predict demand in an area over time, and how to chain fares together over time in order to minimize the total time without a passenger in the cab, but there was not enough time for that at this time.


### Additional Data I would like

While working on this problem, I attempted to bring in the address information related to the GPS coordinates, but ran into issues with the API timing out. Ideally, I would have this information in order to more accurately predict where to go for new fares.

In addition, I would like to see temperature data, weather information (raining, snowing, dry, etc.), and major event information (i.e. major conferences, new broadway shows, etc.) in the area in order to better predict where to be and when.
