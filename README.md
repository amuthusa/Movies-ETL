# Movies-ETL

## Overview:
  Amazing Prime Video an online streaming service would like to set up a hackathon to predict which low budget movie might become popular so that they could buy the right to stream.
  
### Extract:

  The source for the movie data comes from two different sources Wikipedia which holds the movie data from 1960 and rating data from Kaggle. The first step is to extract the data from the source to simplify the process we downloaded the data and kept it in the Data folder (since the size of the data is huge we zipped the data) ![movies metadata and ratings](Data/the-movies-dataset.zip) ![wikipedia movies as JSON](Data/wikipedia.movies.json).
  
### Transform:

  Since the data is from an open-source it has a lot of unwanted and messy data, this step is not only to clean the data but also to merge the columns from both sources, remove unwanted columns and transform the data based on the columns. On top of the above transformation, we also have to fill some of the missing data from the columns selected from one of the sources over the other. This step is time-consuming and needs a lot of manual work to look at the data to make the transformation. Finally, in the transformation, we merged movie data from both the sources and merged rating data to have an idea of the popularity of the movies.
  
### Load:

  Once the data is cleaned and formated to our need we had to load into SQL tables for further analysis. This is the final step before we can start our data analysis and prediction. Jupyter notebook and python have a module named sqlalchemy to load the data into the sql table, since we have huge ratings data we had to chunk the data to load into the table
