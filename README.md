# Movies-ETL

## Overview:
  Amazing Prime Video an online streaming service would like to set up a hackathon to predict which low budget movie might become popular so that they could buy the right to stream.
  
### Extract:

  The source for the movie data comes from two different sources Wikipedia which holds the movie data from 1960 and rating data from Kaggle. The first step is to extract the data from the source to simplify the process we downloaded the data and kept it in the Data folder (since the size of the data is huge we zipped the data) ![movies metadata and ratings](Data/the-movies-dataset.zip) ![wikipedia movies as JSON](Data/wikipedia.movies.json).
  
### Transform:

  Since the data is from an open-source it has a lot of unwanted and messy data, this step is not only to clean the data but also to merge the columns from both sources, remove unwanted columns and transform the data based on the columns. On top of the above transformation, we also have to fill some of the missing data from the columns selected from one of the sources over the other. This step is time-consuming and needs a lot of manual work to look at the data to make the transformation. Finally, in the transformation, we merged movie data from both the sources and merged rating data to have an idea of the popularity of the movies.
  
### Load:

  Once the data is cleaned and formated to our need we had to load into SQL tables for further analysis. This is the final step before we can start our data analysis and prediction. Jupyter notebook and python have a module named sqlalchemy to load the data into the sql table, since we have huge ratings data we had to chunk the data to load into the table

## Challenge:

### Overview:
    
   Refactor the code and make it more modular to extract movies data, transform and load the data to SQL using python function.

### Details on trnsformation and loading:

   Created functions to add alternate title field based on columns like 'Also known as' or language-specific column like 'Chinese/Cantonese' etc. Found some of the common attributes with different names and changed the name for example 'Directed by' and 'Director' is one and the same so changed to 'Director'. Created imdb_id from the imdb_link and removed duplicate movies with the same imdb_id.
   
   Removed columns that didn't have values for more than 90% of the records assuming it won't play a major role in our predictions. Normalized cost-related columns like box_office and budget from different formats like million, billion, millon, dollar amount to plain dollar amount so that we can could statistics on those data. Formated release date from multiple formats to DateTime format which would help in our analysis. We also standardized on running time of the movie.
   
   Formatted Kaggle data so that it would be easy for the merge like the budget, id, popularity is converted to an int and release_date is converted to a date. Merged both Wikipedia movies data and Kaggle movies date based on imdb_id and added corresponding suffixes.
   
   Carefully combed through the data to look for columns that can be dropped in the merged data frame. Using the scatter plot and compared some of the common data like running_time / runtime, budget_wiki / budget_kaggle, box_office / revenue to see which column makes sense. For all of the above columns, Kaggle data seems to be much better suited than Wikipedia data but for the missing data, we do take it from Wikipedia. Dropped some of the columns from Wikipedia like title_wiki, release_date_wiki, Language, Production company and used Kaggle data.
   
   Once the data is transformed we filtered the columns we are interested in and renamed some of them. This gave us consolidated movie data. Now moving on to rating data we grouped by movieId and rating and found the number of users who gave the rating, this would allow us to figure out the popularity. The number of users giving higher ratings conveys the movie is popular and similar kinds of movies might be a hit with users. Merged the movie's data and rating data to get a full picture of the reviews from Wikipedia and kaggle.
