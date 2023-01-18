# Purpose
## Implement a data warehouse for student immigration data
This project generates a data warehouse to allow analytics on international students in the USA. Data from following sources are extracted, transformed and loaded into a data warehouse:
* I94 data from DHS, US-Gov (provided by Udacity; data available for purchase from https://www.trade.gov)
* Weather data for different cities (US and global) from Kaggle (https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data)
* Climate data - processed from aforementioned weather data
* US city demographics data from OpenSoft (https://public.opendatasoft.com/explore/dataset/us-cities-demographics/export/)

#### Scope 
Many international students come to the USA either for acedmic studies (F1, F2 visa) or vocational training (M1, M2 visa). Often, dependents accompany these students (F2/M2 visa holders). This project aims to prepare a data warehouse to perform analytics on incoming international students. 

Questions that are likely to be answered by the analytics team:
1. Which cities are preferred by international students?
2. Do international students directly arrive at their destination city or do they prefer traveling through busy hubs (often with cheaper tickets; i94 address vs. location of entry)?
3. Does city demographics play a role in inernational student's preference? For example, do international students prefer cities with more foreign-born population?
4. Do students prefer cities/localities with similar weathers to their origin cities?

This analytics pipeline will be utilized by Universities (to tailor their offerings to international students), airlines (for route optimization) and/or real-estate investors (student housing development).

#### Describe and Gather Data 

Following data will be aggregated in the data warehouse:
1. Student arrivals data. Monthly data snapshot provided by DHS, US gov (from I94 records).
2. Demographics data for each US cities. Released during census.
3. Weather data for US cities (destination cities for international students) and foreign cities (origin cities for international immigrants; inferred data from I94 records).

## Note

* To save processed tables in S3 bucket, please provide S3 bucket folder locations in the 'oputput_dir' variable. Also, please provide AWS S3 access credentials.
* The code is assumes I94 data is saved in a local directory. S3 bucket can be provided in the 'fname' along with AWS S3 credentials.
* Please follow along 'Capstone Project_ImmigrantStudents.ipynb' jupyter notebook to get insights into the steps of the ETL process.

# Database desgin
The database was designed by following a star schema, with arrivals_table being at the center of the star. Other tables are:
	* student_table
	* city_table
	* weather_table
	* climate_table
	* visa_post_table
This design was chosen to facilitate a wide range of analytics that could be performed with minimal number of joins.
