# CM Vigil April : Portfolio

[Medium blog](https://cmapril3.medium.com/) | [Linked-IN](https://www.linkedin.com/in/cm-april/) | [github projects](https://github.com/cmrjkva/DSI_projects)
--------------------------------------------------------------------
# [Wildfire Size Predictor](https://github.com/CrazyMonkey333/DSI_projects/tree/master/project_5_wildfire_prediction)

2020 will be remembered as the year of a deadly pandemic, civil unrest, and climate disasters. In 2020 the Western United States suffered the most active fire season in its recorded history. California had the single worst fire season recorded. Arizona had the worst in a decade and Oregon had its most destructive; meanwhile Washington and Colorado had several of their largest all-time wildfires recorded. 
The global atmospheric monitoring satellite Copernicus recorded CO2 emissions from the 2020 fires and it was noted in September that “The fires are emitting lots of smoke and pollution into the atmosphere; those in California and Oregon have already emitted far more carbon in 2020 than in any other year since CAMS records begin in 2003” - [CAMS monitors smoke release from devastating US wildfires | Copernicus](https://atmosphere.copernicus.eu/cams-monitors-smoke-release-devastating-us-wildfires). 
Overall 10.2 million acres of land went up in flame and 46 people lost their lives. The total cost in material damages is upwards of 19.88 billion USD. 


![title](https://atmosphere.copernicus.eu/sites/default/files/inline-images/nasa_worldview_usa_20190911_suomiviirs_pm_small.png)
*Image from the NOAA/NASA Suomi-NPP satellite of smoke over the western US on 11 September 2020. Orange dots show active wildfires. California is at the centre of the map along the US west coast, with Oregon to its north and Washington just north of Oregon. Credit: NOAA/NASA.*

As a team we decided to investigate the relationship between weather data (precipitation, temperatures, and drought) and the occurrences of fires to build a model which would predict the size of wildfires to help our communities prepare. 

#### Our project focused on the following 11 States in the US: 
| Arizona | California | Colorado | Idaho | Montana | New Mexico | Nevada | Utah | Oregon | Washington | Wyoming |

#### Data Collection
We used two sources of data :

- [Kaggle Fire Data](https://www.kaggle.com/rtatman/188-million-us-wildfires/notebooks).
A spatial database of 1.88 million wildfires that occurred in the United States from 1992 to 2015. We collected the most current and largest dataset readily available. There was 140 million acres burned during this 24-year period. The data set includes: discovery date, final fire size, and location (latitude and longitude) among many other features.

- [NOAA Climate Data](https://www7.ncdc.noaa.gov/CDO/CDODivisionalSelect.jsp#).
Meteorological dataset covering 120 years of weather information for the 11 western US states of: AZ, CA, CO, ID, NM, NV, MT, OR, UT, WA, and WY, including metrics and indexes describing precipitation, temperatures, and droughts.
The two datasets were combined by matching weather information and fire data on the combination of month-year-state for each of the fires that burned from 1992 to 2015 in the eleven states of interest. 

![](https://github.com/cmrjkva/DSI_projects/blob/master/project_5_wildfire_prediction/visuals/fire_precip_heat.png?raw=true)

#### Modeling
The project ultimately uses two main models.
- Neural network for predictive power 
- Random Forest Classifier for feature importance. 

We optimized the neural network on recall score focusing on true positive rate as this helped us predict larger and more destructive wildfires. To improve our models, we employed the modeling technique of bootstrapping which gave us a more normal distribution of wildfire classes. This way, we were able to capture our larger fires.

The second modeling breakthrough we had was harnessing geospatial data through KMeans clustering of longitude and latitudinal data. We then One-Hot-Encoded it which gave us a sparse matrix that was the most important predictive element of our model. We believe that this is because terrain features matter immensely when determining the potential size of a wildfire.

The third major breakthrough was the trailing averages. Due to the cumulative nature of meteorological effects on drought severity, we chose to include drought, temperature and precipitation trailing averages over 12-, 9-, 6-, and 3-months. Adding that data essentially doubled our recall scores for medium sized fires, which improved our overall model recall. Next, since our Neural Network is a blackbox model, we were not able to glean as much insight into features. We utilized Random Forest Classification to compliment insights from our Neural Network model by providing top features and weights.

**Top 3 features (excluding location clusters):**

|Feature|Importance|Feature Description|  
|---|---|---|  
|tavg_t3m|0.05085|Average Temperature Past 3 Months|  
|pcp|0.04720|Month Precipitation|  
|tavg_t6m|0.04633|Average Temperature Past 6 Months|

#### Conclusions
Wildfires are extremely complex phenomena. While the NOAA data offered a set of independent variables which described weather history, we were not able to include in our model other important factors which also affect final fire size, such as wind or terrain features (e.g. land cover or incline). Switching our target variable from a continuous one (fire size, in acres) to a multi-class problem, improved the score from an R2 of under 10% accuracy to over 60%. Further, re-defining the problem as a binary classification of "large" vs "small" fires drove accuracy up to 62-77%; depending on the threshold chose to delineate between the two classes.

Because our goal was to improve preparedness and help contain damage from wildfires without putting efforts into preventing fires which weren't likely to spread, our ultimate focus was on increasing the recall of our model, and moreover - to increase its recall with regards to large fires.
Each of the seven-class classifications requires sklearn's estimators to perform 21 separate classifications - fitting some of the estimators we evaluated (e.g. SVM) was very computationally expensive. Despite being computationally expensive, we were able to create a model that gave us a significant increase in our recall score. We can confidently predict very large fires and some mid-range fires with our current model.

**Classes and model improvements:**

|Class| Size Acres|Baseline (% of dataset)|Final Model|
|---|---|---|---|
|A| >0<=0.25|62%|59%|
|B|0.26-9.9|29%|1%|
|C|10.0-99.9|6%|20%|
|D|100-299|2%|50%||
|E|300 to 999|1%|58%|
|F|1000 to 4999|2%|59%|
|G|5000+|0.07%|86%|

#### Tech Stack

| Amazon AWS S3 | Amazon CLI | Boto3 | Matplotlib | Mpl_toolkits | Tensorflow |
| Python3 | Seaborn | Sklearn | Sqlite | Statsmodels | Streamlit | 

----------------------------------------------------

# [Star Wars vs Star Trek : Web API’s and NLP](https://github.com/CrazyMonkey333/DSI_projects/tree/master/project_3_webscrape_nlp)

NLP is useful in many applications of technology that use textual and/or verbal language such as classifying scammer emails and detecting fake news, or even targeted advertising on social media sites. In this project I demonstrate how to scrape data off the web using a web application programming interface or web API and how to use classification models on language data. In this case I use the [Pushshift's](https://github.com/pushshift/api) reddit API to extract submissions. Then after processing the language data, I apply classification models to determine which subreddit the posts came from. 

#### The why
A close friend of mine recently asked “What’s the difference between Star Trek and Star Wars?” and I nearly let me emotions get the best of me. How could someone close to me go so many years living without understanding what Star Wars and Star Trek are about? It hit me that there may be a lot of people out there that do not know the difference between a Vulcan and a Gungan! So this here is a little project I decided to do to help my friend out. My project notebook, when ran will take data from these sci-fi series subreddits and make it so that you will know if the language is about Star Trek or Star Wars. 


#### Data Collection 
The code in the web scraping notebook takes 20 loops through the subreddit of choice, taking 100 posts at a time. It begins when you run the code and works backwards, taking a breather between cycles (to not alarm the website) before continuing the loop to completion.  This process gives us 4000 data entries of submissions, an evenly distributed 2000 entries for each subreddit.

#### Data Cleaning and EDA
In the data exploration and cleaning section I combined the self-text and title features, filled in null values with an empty space, and removed any special characters. Further on down the road when I found outliers I came back to remove them. I tokenized, lemmatized and stemmed out the words, considered stop words as well to explore the data in depth and even did a count vectorization that indicated the most common words in each subreddit. However, there is a lot of overlap in these similar subreddits; it is far more impactful to determine the importance of words instead of frequency, as shown below. 
![](https://github.com/cmrjkva/DSI_projects/blob/master/project_3_webscrape_nlp/images/components.png?raw=true)

#### Modeling
I tested on two models. Adaboost and logistic regression models were ran through a cross validated grid search. The adaboost was the least over/under fit model. The logistic regression performed at a higher accuracy level on both the test and training data though so I took that as the better model in this instance.

#### Evaluation and Conclusion
In conclusion for those of you that have not seen or heard of Star Wars or Star Trek, you could memorize what category these 20 words are in and have a solid idea of which fandom your friend is talking about.
![title](https://github.com/cmrjkva/DSI_projects/blob/master/project_3_webscrape_nlp/images/top10starwars.png?raw=true)
![title](https://github.com/cmrjkva/DSI_projects/blob/master/project_3_webscrape_nlp/images/top10startrek.png?raw=true)

Contextually for reddit this could be used for targeted advertising such as star trek themed video games to star trek fans vs star wars Legos for star wars fans.  This model evaluates textual data to identify what people are discussing in two distinct but similar categories.

--------------------------------------------------------------------------------

# [Determining Home Values](https://github.com/CrazyMonkey333/DSI_projects/tree/master/project_2_ames_housing)

I took on the role of analyzing and modeling housing data for the Iowa Assessors Society. We had a data set containing information from the Ames Assessor's Office in computing assessed values for individual properties sold in Ames, IA from 2006 to 2010. The population size was 2930 homes with 82 variables. The 82 variables included nominal, ordinal, discrete and continuous observations. 

We were curious to what features matter most in determining a fair market value for a home. This information has the potential to be valuable to everyone in the housing market from buyers to sellers. We also had an additional data set of homes to be appraised and we want to accurately measure their values. 
    
This project involved many steps before I started to build a model. 
1. Crafted a problem statement
2. Imported and cleaned the data (which involved dealing with lots of null values)
3. Conducted exploratory data analysis in using seaborn heatmaps and coefficients of correlation to determine feature importance
4. Feature engineered buckets for neighborhoods, exterior, and sale type
5. Feature engineered general living area combined with finished basement area for total living area.  
6. Removed 3 remarkable outliers with incredibly large living area.

![title](https://github.com/cmrjkva/DSI_projects/blob/master/project_2_ames_housing/photos/proj_2_liv_vs_sale_b4.jpg?raw=true)
![title](https://github.com/cmrjkva/DSI_projects/blob/master/project_2_ames_housing/photos/proj_2_liv_vs_sale_after.jpg?raw=true)

#### Setting Up a Baseline Model
The baseline model I set up for my example is a basic linear regression using only the top 5 variables.
1. Overall Quality
2. Total Living Area
3. Exterior Quality
4. Kitchen Quality
5. Garage Area

Doing a train test split on our training data, I got back a score of 84.6% on our split train, and 83.3% on our split testing data. This is not bad considering these are only 5 variables out of 82.

#### Setting Up the Model
I utilized polynomial features to the 2nd degree and fit the data to a standard scaler in order transform the data so rankings from 1-5 and rankings from 1-10 would be comparable. After attempting a few different methods, I settled on fitting the data to a ridge cross validation model. The model's r2 score indicated that the model was 93.6% fit to the training data and 87.6% accurate at determining the price in my split test set.

#### Conclusion/Recommendations:        
We can say with confidence that the overall quality, total living area, exterior quality, kitchen area and garage area have the most significant impacts on the price of the house. Going from 5 variables to 19 variables and using a more robust model we only gained 4.3% accuracy on the testing datasets. However excluding Lot Frontage due to the many null values likely had a significant dampening effect on improving our accuracy.

---------------------------------------------------------------------------------------

<script type="text/javascript" src="https://platform.linkedin.com/badges/js/profile.js" async defer></script>
