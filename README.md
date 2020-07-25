# Creating categorical variables from a string in one line of code

#### One of the more difficult tasks of cleaning data can be figuring out what to do when you have a column made up of a long string of attributes. This string can be the description of the object written by someone looking at the object. While this column can be daunting, it can present incredibly valuable information to your analysis, as the data may not have been captured in the other available columns and can bring further analytical details.

#### When scraping data from websites, most of the object attributes can be placed into specific columns. For example, when scraping car inventory data, you can drop the car make, model, year, mileage, and price into columns designated for those specifications. However, many car dealership websites include a description of the car with key features that may not be captured anywhere else in the listing. These key features are likely what car buyers are looking for in addition to primary specifications and will drive the price up or down.  

#### It only takes one line of code in R to create a new column with this categorical information. In the example of car inventory data, I wanted to create a column that would designate whether or not a car had heated seats. I did just that, and was then able to determine how much (or little) heated seats contributed to the car’s price, against the other specifications. I created additional columns for the availability of Bluetooth and a backup camera, as these were crucial features in my own car search several years ago. 

### Now, for the code. You will first need to import your dataset and give it a name. 

car_data <- read.csv("/Users/Kyra/Desktop/cardata.csv")

#### Next, you will need to identify which column the string is in and determine the exact spelling of the data you would like to use for the new column. In my example, the existing column is called ‘options’, and I would like to pull ‘Heated Seats’ from there to create my new variable called ‘heatedseats’. 

car_data$heatedseats <- ifelse(grepl("Heated Seats", car_data$options), "yes", "no")

#### In this case, if the car has heated seats, R will print ‘yes’, and if not, ‘no’. R will automatically create the dichotomy, meaning you will not need to define what ‘yes’ and ‘no’ mean. 

#### If you would like to create an integer dichotomy, simply modify the code to insert ‘1’ or ‘0’ for the presence of the feature. You will then need to change the data structure to integer for that column. 

car_data$heatedseats <- ifelse(grepl("Heated Seats", car_data$options), "1", "0")

car_data$heatedseats <- as.integer(car_data$heatedseats)

#### I went on to add the other two crucial car features in this dataset for analysis reasons, and more can be added in this way. I opted for the ‘1’ ‘0’ approach, as I needed the data in integer form. 

car_data$bluetooth <- ifelse(grepl("Bluetooth", car_data$options), "1", "0")

car_data$backupcamera <- ifelse(grepl("Backup Camera", car_data$options), "1", "0")

car_data$bluetooth <- as.integer(car_data$bluetooth)

car_data$backupcamera <- as.integer(car_data$backupcamera)

#### Lastly, to check the results of your added columns, you can use the ‘Summary Tools’ package, which will show the dichotomous breakdown.

library(summarytools)

print(dfSummary(car_data$heatedseats, graph.magnif = 0.75), method = 'render')

print(dfSummary(car_data$bluetooth, graph.magnif = 0.75), method = 'render')

print(dfSummary(car_data$backupcamera, graph.magnif = 0.75), method = 'render')
