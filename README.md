# regis_msds_practicum1
Analyzing and Predicting Crime in the City of Denver

This project analyzes crime in the City of Denver from 2016-2021 using Jupyter Notebook (Python) exclusively and associated libraries.

The intent of the project is to visualize and understand trends in crime over this period of time. Is crime increase/decreasing over time, and in what neightborhoods? The project also seeks to understand if crime can be predicted using both multivariate regressions and time series forecasts.

THE DATA

The analysis pulls crime data from the City of Denver and includes over a half-million crimes. These crime data conveniently break crime down by neighborhood. Crime has also been categorized such that you can distinguish between different types of crime (e.g., murders, larceny, theft, etc.). Code was written to tally up crime year over year for each neighborhood such that trends could be visualized in tables and plots. 

Additional data has been acquired from the US Census Bureau's Ammerican Community Survery 5-year. It has been pre-processed in ArcGIS Pro to bin crimes by Denver neighborhood. These variables were closely analyzed to see if there was an obvious correlation to crime. If so, they were included in the analysis. Attributes include...

The analysis also seeks to look at the influence certain businesses in a neighborhood have on crime. Specifically the analysis looks at marijuana dispensaries and bar and liquor stores. The hypothesis is crime increases as these establishments increase.

These dataset were merged based on a common neighborhood name attribute. Significant data cleaning efforts were made in order to ensure the joins were successful. 



