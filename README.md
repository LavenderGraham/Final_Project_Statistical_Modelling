# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
This is a project about connecting to the CityBikes, Foursquare, and Yelp APIs and getting data from there about CityBike locations as well as bars, restuarants, and lasertag
establishments near the CityBike locations. Then it is about processing the data and determining how many CityBike locatations are near each establishment, as well as drawing relationships
between the citybike locations and the types of nearby establishments. Unforntunately I did not find any laser tag locations near city bike locations in Montreal so this is restricted to Bars and
Restaurants. 

## Process
### Step 1:
I connected to the free city bikes API and downloaded their information about what cities have city bike services. Then I unpacked their locations stored in dictionaries in the location column using json.normalize() and found their information under location. After filtering the data frame for Montreal I was able to find a link to connect to another city bikes API which contained the information about the city bikes in Montreal including their coordinates. I cleaned the resulting data frame and extracted the coordinates as a list of tuples for later. I saved my results as a csv.
### Step 2:
I connected to the Foursquare API and used a looping function and my foursquare API key and my list of coordinate tuples to extract the information about all the points of interest near bike stations in Montreal. I then had to clean and process the data by dropping irrelevant columns and normalizing columns (using json.normalize) that had information packed in dictionaries. I then dropped unprocessed columns from my FourSquare dataframe and stitched the unpacked columns back to my FourSquare dataframe using pd.concat. I Saced my results as a csv.
### Step 3:
I did the same process that I did to collect and process data from the Foursqaure API to collect and process data from the Yelp API. Except this was more difficult because it was harder to find my Yelp API key and unpack the dictionaries and normalize the columns. I saved my results as a csv.
### Step 4:
I compared the results from the Foursqaure and Yelp APIs and decided to proceeed with using information from the YELP API because it had review counts, ratings, and pricing information.
### Step 5:
I opened up my dataframes from my CityBikes and Yelp csvs. I wrote functions called haversine() and find_closest_points() to find out which bike stations were close to which establishments. I also calculated the numer of bikes stations near each bar/restaurant and had to collect all this data together into one dataframe using merge() and concat() functions. I had to unpack the bike latitude and longitude using an apply lambda function.
### Step 6:
I conducted exploratory data analysis on my data by using seaborn to make a bar graph of which establishments had the most bike stations near them, and another bar graph of which bike stations had the closest bike stations. Also a histogram of the distribution of bike stations near points of interest.
### Step 7:
I saved my results from step 5 as SQLite files.
### Step 8:
I opened up my main SQLite file from the previous step as a dataframe and conducted linear regressions using statsmodels to test if the number of bike stations nearby an establishment is predictive of its Yelp rating and 
its Yelp listed price.
### Step 9
I conducted logistic regressions using statsmodels to test if the number of bike stations nearby an establishment is predictive of whether or not it is outstanding (4.5 star or more on Yelp) or whether or not it is
exhorbiantly priced.

## Results
I found that the Yelp API was very useful for examining the bars and restaurants near bike stations in Montreal. Unfortunately my Yelp API call did not find any laser tag establishments near city bike locations.

My linear regression analyses found that the number of bike stations nearby a bar or restaurant is statistically significantly positively correlated with its ratings and its prices. But these correlations are very weak.

My logistic regression analyses found that the number of bike stations nearby a bar or restaurant is statistically significantly negatively correlated with whether or not it is outstanding but that this association is very weak.
They also found that the number of bike staions is statistically significantly positively correlated with whether or not it is exhobiantly priced. But this association is very weak.

## Challenges 
During this assignment I mostly had trouble with connecting to the Yelp API, making my looping function to query the API work effectively, and normalize the columns that were dictionaries in this API.

I got assistance from mentors who helped me find my YELP API key and helped me find the documentation needed to edit my function to query Yelp. I tried for a few hours to unpack my categories list in the Yelp API but I could not
figure out the python code to do this without generating bugs like missing rows. So I saved my semi-unpacked dataframe as a csv and opened it in Excel and used the Text To Columns function to split by delimiters and edited the
data frame there, then saved it as a different csv and opened that csv in VSCode.

I also had trouble figuring out how to set primary keys and connections in my SQLite files. I just abandoned that as it was not an official part of the assignment.

## Future Goals
I would analyse how the categories of the restaurants and bars affect the number of bike stations nearby.

I would re-do my linear and logistic regression analyses to see if the results are different for various categoreis of restaurants and bars.


