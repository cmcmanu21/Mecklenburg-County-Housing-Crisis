# Mecklenburg-County-Housing-Crisis
----
Author: Christopher McManus
----
Overview:

At UNC Charlotte's School of Data Science, each student is required to complete a data science & business analytics-related internship. I worked with Dr. Jean-Claude Thill and Faizeh Hatami of UNC Charlotte's Department of Geography & Earth Sciences during the spring 2022 semester. We took a look at Mecklenburg County's quarterly rental market data across 1-, 2-, and 3-Bedroom properties between 2000 and 2020. Our goal was to accomplish four objectives during this semester:

1.) Identify location-based features influencing the effective rent, or price someone pays in rent per month, using a random forest model for the year 2019 between each property segment. 

2.) Utilize local Moran's I to indentify clusters of "high" and "low" effective rents between each property segment. Then we looked to see if the clusters had changed over time and submarkets (neighborhoods).

3.) Create heat maps to highlight the effective rent growth between 2001 and 2020 for each submarket between each property segment. The heat maps were supplemented with additional geospatial visualizations to identify submarkets more easily with extreme effective rent growth rates. 

4.) Design time series plots to depict the vacancy rate for each submarket across each property segment. Then we looked to uncover submarkets with "high" vacancy rates and provided landlords in submarkets with "high" vacancy rates with initial reccomendations on improving their occupany levels. The time series plots were supplemented with additional geospatial visualizations to identify submarkets more easily with "high" vacancy rates.

----
Methods Used for Each Objective:

Objective 1.) The data used for this analysis included the density of each place-based amenity, selected by their frequency, across each submarket sourced from the Mecklenburg County GIS Data Center and MyGeodata Cloud. These amenities were then paired to average effective rent per unit adjusted for inflation for each submarket, sourced from CoStar, using a spatial join technique. Additionally, population characteristics, such as income levels, sourced from the U.S. Census Bureau, were also included. To find the density of each place-based amenity, a count of each amenity was extracted from the spatially joined submarket and amenity shapefiles. Then the count of each amenity within a submarket was divided by the area of the submarket. Amenities that were not present in the submarket were given a value of “0”. The average effective rent for each submarket was then calculated by averaging the four quarters in 2019 together. “Null” values were not imputed, as it was uncertain if the segment existed in the submarket. Due to the model’s inability to handle “null” values, submarkets with unknown effective rent values were omitted, along with their features. The effective rent values for included submarkets were then assigned a binary classification of “0” representing effective rent below $1,000 per month and “1” representing effective rent above $1,000 per month. The only pre-processing required by the LEHD data was to be combined with the amenity data and effective rent data by the unique “ID” of each submarket. 

Objective 2.) The data used for this analysis was comprised of the average effective rent per unit adjusted for inflation of each year across each submarket by again aggregating the quarterly data into an average for each year. This was again sourced from CoStar. “Null” values were again not imputed due to the uncertainty of the existence of the property segment in the submarket. This time, however, “null” values were left in the dataset because the model was able to handle missing data. The processed effective rent data was again paired with its submarket based on the unique “ID” of each submarket. To identify the clusters, 80 models were created — one for each property segment over 20 years. The models considered the eight nearest submarkets using the K Nearest Neighbors (KNN) method, which is a supervised learning technique that assumes similar things are close to each other (Harrison, 2019). To do this, the Spatial Lag, or weighted sum of values in the neighboring submarkets, was calculated and then standardized by subtracting the average value and dividing by the standard deviation (Rey et al., 2020; Murack, n.d.). These standardized values were then used to find the LISA clusters of the effective rent. Clusters that were determined to have “high” effective rents were displayed using the model’s default dark red color, while clusters that were determined to have “low” effective rents were displayed with the model’s default dark blue color.

Objective 3.) The data used for this analysis included the quarterly effective rent growth percentage for all submarkets, quarterly effective rent per unit — adjusted for inflation for all submarkets — and the quarterly number of total units for all submarkets. The data was sourced from CoStar. “Null” values were again not imputed because not all submarkets offered each property segment. “Null” values were also not considered for the models. The cleaned data was again joined with the appropriate submarket. Three heat maps were created to illustrate the changes in the effective rent growth. A red-green diverging color palette was used to indicate the change in the quarterly effective rent growth. The intensity of the red color was determined by the quarterly increase in the growth percentage, while the intensity of the green color was determined by the decrease in the quarterly growth percentage. The quarterly effective rent growth was also represented as squares on the heat map, with the size of each square depending on the amount of growth or decline realized. 

Objective 4.) The data used for this analysis was the quarterly vacancy percentage sourced again from Costar. Outliers were present in the vacancy data. These outliers caused spikes in the vacancy rates from new units being at the beginning of each quarter. Spikes are sharp rises in the frequency of the data typically followed by a decrease (“TechTarget”, 2010). These spikes made it difficult to spot trends in the vacancy rate of the submarkets and had to be removed. To remove the outliers, the Interquartile Method was used to determine the upper and lower fence values for each segment and any value outside of either fence value was converted into a “null” value (Taylor, 2018). For 1- and 2-bedroom properties, quarterly vacancy rates between 0% and 13%, and between 0% and 14% respectively for each submarket were kept. Furthermore, for 3-bedroom properties, quarterly vacancy rates for each submarket were kept from 0% to 17%. Submarkets were removed from each model when the vaca ncy rate for any given period was not known. Submarkets were also removed from each model when the average vacancy rate was below 4% across each segment as these indicated “acceptable” vacancy rates and were not of concern (“Mansion”, 2022). “Null” values were kept in the models. The cleaned data was then again paired with the appropriate submarket.

To determine whether the vacancy rate was classified as “high” or “low”, another method was used called the Jenks Natural Breaks Classification Method (Jenks Method) and finds the “natural” classes in the data (Ahmad, 2019). Using the Jenks method is ideal when classifying data because classes that are created better represent the data at hand. This method determined that for 1-bedroom properties “high” vacancy rates were those above 6.5% and low rates were those below 4.6%. For 2-bedroom properties, “high” rates were above 6.9% and “low” rates were below 4.9%. Lastly, for 3-bedroom properties, “high” rates were above 7.1% and “low” rates were below 4.8%. The time series plots were then supplemented with additional geospatial visualizations with “high” values represented in shades of red and “low” values represented in shades of green.

----
Objective Results:

Objective 1.) Click on this link https://docs.google.com/document/d/1B_PHOpynFUY_AHSTB7wtvo4mQWsH6CkodzoPG4tbt3s/edit?usp=sharing to be directed to the summary of the random forest feature importance

Objective 2.) Click on this link https://docs.google.com/document/d/13f6r65OYx54hgRSIQrLte6QdRFQQNfYytzAQDK5YAGw/edit?usp=sharing to be directed to the results of each Moran's I model

Objective 3.) Click on this link https://public.tableau.com/views/HeatMapAnalysisofEffectiveRentGrowth/1BedroomEffectiveGrowth?:language=en-US&:display_count=n&:origin=viz_share_link to be directed to the results of each heat map model

Objective 4.) Click on this link https://public.tableau.com/views/TimeSeriesAnalysisofQuarterlyVacancyRate_16513538854440/TimeSeries1Bed?:language=en-US&:display_count=n&:origin=viz_share_link to be directed to the results of each time series model

For in-depth results and analyses of each objective, please download the "Objective Results and Analyses" file! 

----
Data Sources:

Mecklenburg County's Rental Market Dataset (subscription required): https://www.costar.com

Location-based ammenities: http://maps.co.mecklenburg.nc.us/openmapping/data.html, https://mygeodata.cloud/data/download/osm/-/united-states-of-america--north-carolina/mecklenburg-county
                           
Submarket Employment Census Data: https://lehd.ces.census.gov/data/#lodes

----
Objective Sources:

Ahmad, R. (2019, August 5). Jenks natural breaks - best range finder algorithm. Medium. Retrieved May 1, 2022, from https://medium.com/analytics-vidhya/jenks-natural-breaks-best-range-finder-algorithm-8d1907192051 

Harrison, O. (2019, July 14). Machine learning basics with the K-nearest neighbors algorithm. Medium. Retrieved May 4, 2022, from https://towardsdatascience.com/machine-learning-basics-with-the-k-nearest-neighbors-algorithm-6a6e71d01761

Mansion Global. (2022, March 7). Vacancy rate. What does vacancy rate mean? | Mansion Global. Retrieved April 27, 2022, from https://www.mansionglobal.com/library/vacancy-rate

Murack, J. (n.d.). Regression Analysis Using GIS. MIT.edu. https://libraries.mit.edu/files/gis/regression_presentation_iap2013.pdf

Rey et al. (2020). Geographic Data Science with python. Local Spatial Autocorrelation - Geographic Data Science with Python. Retrieved May 1, 2022, from https://geographicdata.science/book/notebooks/07_local_autocorrelation.html

Taylor, C. (2018, April 27). Detect the presence of outliers with the interquartile range rule. ThoughtCo. Retrieved May 1, 2022, from https://www.thoughtco.com/what-is-the-interquartile-range-rule-3126244

TechTarget Contributor. (2010, August 10). What is Spike? - definition from whatis.com. SearchSoftwareQuality. Retrieved May 1, 2022, from https://www.techtarget.com/searchsoftwarequality/definition/spike

----
Background Readings:

Mecklenburg County's Housing Affordability Crisis: https://spectrumlocalnews.com/nc/charlotte/news/2022/02/02/mecklenburg-county-says-1--of-area-apartments-rent-for-less-than--1-000

Local (Moran's I) Spatial Autocorrelation: https://geographicdata.science/book/notebooks/07_local_autocorrelation.html

Jenks Natural Breaks Classification Method: https://medium.com/analytics-vidhya/jenks-natural-breaks-best-range-finder-algorithm-8d1907192051                           
