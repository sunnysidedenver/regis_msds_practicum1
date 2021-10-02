# Analyzing and Predicting Crime in the City of Denver

This project analyzes crime in the City and County of Denver from 2016-2021 using Jupyter Notebook (Python) exclusively and associated libraries.

The intent of the project is to visualize and understand trends in crime over this period of time. Is crime increase/decreasing over time, and in what neightborhoods? The project also seeks to understand if crime can be predicted using both multivariate regressions and time series forecasts.

# THE DATA

The analysis pulls crime data from the City and County of Denver from 2016-2021, which includes over a half-million crimes. These crime data conveniently break crime down by neighborhood. Crime has also been categorized by type (e.g., murders, larceny, theft, etc.). Code was written to tally up crime year over year for each neighborhood such that trends could be visualized in tables and plots. The data file is named crime.csv and has been zipped down to a file size just under 25 MB.

Additional data has been acquired from the US Census Bureau's American Community Survery (ACS) 5-year. It has been pre-processed in ArcGIS Pro to bin crimes by Denver neighborhood.The attribute table was then exported to a table which was then transformed into an excel file using a geospatial tool called Table to Excel. Given the ease of working with .csv files in Pandas, I converted the .xls files to .csv. These variables were then closely analyzed to see if there was an obvious correlation to crime. If so, they were included in the analysis. 

Attributes initially included: total population, percent hispanic, percent white, percent black, median age, median age male, median age female, number owner occupied households, number renter occupied households, total households, number of male households with no wife present, number of female households no husband present, number of non-family households, median rent, median home value, percent poverty, median household income, median family income, per capita income, number enrolled in school, number with less than a high school diploma, number of high school graduates, number of thos with some college or community college, number with bachelors degree or higher, and if the household is Spanish-speaking. The data file is named acs.csv.

The analysis also seeks to look at the influence certain businesses in a neighborhood have on crime. Specifically the analysis looks at marijuana dispensaries, number of Starbucks, and the number of bar and liquor stores in each neighborhood. The hypothesis is crime increases as the number of liquor licenses and marijuana dispensaries increases, but decreases with increased Starbucks. These data were acquired from ArcGIS Online, a repository of datasets made available to the ArcGIS community of users. The data did not include neighborhood attribute details, so they were merged a neighborhood boundary shapefile, aslo acquired in ArcGIS Online, in ArcGIS Pro, using a spatial join technique. Once joined, the data were transformed to .csv files using the same technique used to transform the ACS data. These files are respectively named mj.csv, sb.csv, and liquor.csv.

These five datasets were then merged based on a common neighborhood name attribute. Significant data cleaning efforts were made in order to ensure the joins were successful and that there were no missing data. For example, some of these datasets used alternate spellings and/or names. All data had to match exactly.

# VISUALIZING THE DATA

The data have been organized such that trends in crime can be visualized at the neighborhood level year over year. You can see which neighborhoods have the most and least amount of crime. Additionally tables were created that show the different crime types for select neighborhoods and their corresponding counts. The plots were created with the matplotlib.pyplot and seaborn libraries. The tables were created using the pandas library. 

# MODELING THE DATA

Two approaches were explored in order to predict crime. The first involves a using a multivariate regression. This regression uses the statsmodels.formula.api to import ols. 

The second uses a time series analysis and forecast, which uses the statsmodels.tsa.arima_model library to import ARIMA.

# CONCLUSIONS

Crime is not normally distributed across Denver and predictor variables do not seem to have a strong enough relationship to crime. Fitting a non-normal distribution with weak predictors has its challenges. Deleting the outliers to normalize the distribution is not in the best interest of the analysis. So while there is fairly strong relationship between crimes and the number of liquor stores in a neighborhood, for example, liquor stores alone do not describe (or fit) the whole distribution of crime across Denver. The regression was fitted over 10 times in order to improve model perfomance (as measured by an AIC score), but still returned a fit with a very low r-squared. Also, the model has issues with multicolinearity and heteroskedasticity. Attempts were made to minimize both using Breusch-Pagan tests and a VIF score. A recurisive feature elimination was used in the end in order to automate selection of the best attributes, but the r-squared was only 25%. Because the model never reached a high enough accuracy the data were never split into test and train. There was no model good enough to fit in the end. 

Nonetheless, I am left with a final equation of: total crime = 91 * number of liquor stores + 0.33 * total population + 255 * number of marijuana dispensaries + 278.63

The time series forecast does a better job of at least predicting short term trends in crime. The analysis looks at crime for the entire period of record, but broken down into 67 months. This supplied the model with sufficient data points to return a reasonable prediction. The data were checked to see if they were stationary using a Dickey Fuller Test. They were not. The data were manually analyzed in order to optimize the order of differencing [and make more stationary] as well as the MA and RA terms.  I then used an autotuning function from the pmdarima library to further improve my model. My final, trained and fitted model, has a fairly large RMSE but when plotted again actual crime, it doesn't a baisc job at indicating trends into the near term.

At this time I would not suggest crime can be easily modeled using a multivariate linear regression with the attributes chosen for this analysis. However, the relationships between crime and these variables might give subjective insight into whether an increase in crime is likely, and may be of use to decision makers. For example, there is 70% correlation between crime and the number of liquor stores/bars in a neighborhood. Aslo, as income increase in a neighborhood, crime generally decreases. Crime really jumps with more rental units, too.

I could recommend, with further refinement, that a time series analysis could be used to determine short term increases/decreases in crime but the error bar is still fairly high.


