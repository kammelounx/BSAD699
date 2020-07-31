# Analysis of Airbnbs in Munich, Germany

#### With the ongoing pandemic, it's no wonder that people feel the urge leave home and travel. Since the ability to travel has largely been out of question, I thought I could combat my itch by at least looking at Airbnbs in a city I would like to visit: Munich, Germany. 

#### After scouring the Kaggle website, I found a dataset that scraped Airbnb data and placed all the information into organized columns. Specifically, my goal was to use R to determine which amenities/characteristics of Airbnbs drive the price. Perhaps, this could be used for future travellers looking to make the most of their money when booking, or it could help a new host determine how to set their Airbnb's price per night. 

#### One of the more difficult tasks of this project was finding a way to clean up the "Amenities" column, which was a string of all the amenities included in the Airbnb listing. Common amentities included Wifi/internet connection, presence of a patio or balcony, and the availability of parking, among others. I pulled nine total amenities from this column and created a separate dichotomous variable that determined if the Airbnb listing in question had this amenity. The amenities I pulled are as follows:

* A/C - air conditioning
* Balcony
* Coffee Maker
* Family Friendly
* Iron
* Kitchen
* Washer
* Wifi
* 24 Hour Check In

#### These nine amenities were put up against other Airbnb characteristics, including room type, number of ratings, numbers of bedrooms/bathrooms, number of beds, minimum number of nights, availability within 365 days, neighbourhood, and how many guests it can accommodate. 

#### In order to pull these nine amenities from the "Amenities" column, I used one line of code for each amenity:

MunichAirbnbClean$Balcony <- ifelse(grepl("balcony", MunichAirbnbClean$amenities), "yes", "no")

#### Since R automatically assigns this new variable as character, it required one additional line of code to convert it to factor:

MunichAirbnbClean$Balcony <- as.factor(MunichAirbnbClean$Balcony)

#### These two steps were done for each amenity, which then allowed my analysis to run much more smoothly. 

