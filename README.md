# Project 2 : No Dogs Left Behind!
 No Dog Left Behind Project- Data for dog adoption use
 
 Group members:
 - [Jackelyne Gutierrez](https://github.com/Jackelyneg)
		
- [Juliana Puskar](https://github.com/Anikraze)
		
- [Tricia Toffey](https://github.com/ttoffey)


## Brief Description:

The intent of this database is to help shelters to place dogs based on breed characteristics. By breaking down the most popular breeds and their standardized breed behavior, it helps shelters to make suggestions as to which dog may best suit the personality and lifestyle of a potential adopter. The database should help to answer:

Which dog breeds are the most popular?

What are the most common personality traits within those breeds?

In a set area, how many people own the breeds we would expect?



### Technologies used:
1. Python
2. Pandas
3. Splinter
4. Beautiful Soup
5. Quick DBD
6. Pg admin SQL


### ETL Steps 
1. Scrape data for popular dog breeds and rank 2017 from [AKC](https://www.akc.org/most-popular-breeds/2017-full-list/)
2. Collect data from other sources such as [Kaggle]
3. Create a quick dbd flow chart 
4. Merge collected from kaggle into postgres database
5. Create queries

### Data Sources:
- [American Kennel Club](https://www.akc.org/most-popular-breeds/2017-full-list/)
- Dog characteristics
- NYC Dog data base




## Step 1. Scraping from AKC:
- [Click here for website used](https://www.akc.org/most-popular-breeds/2017-full-list/)
- Used Beautiful soup and splinter to scrape table data 
- Cleaned up by renaming column names and resetting index to breed_id
- Remove 's' from Dog breeds to make it singular

- Click [Here](https://github.com/anikraze/no_dog_etl/blob/main/dog_breed_etl.ipynb) to see full steps


![image](https://user-images.githubusercontent.com/81592631/123521815-0ce20480-d687-11eb-8fbb-5ac5e058ba9c.png)

## Step 2 Cleaning data sources from Kaggle:
- Dog Characteristics Data Base:
	-This database consists of Breed_name, characteristics, weight, Price etc.
	- Remove unecessary columns ex:("AltBreedName", "MalaysiaGuardedDog",etc.)
	- Dropped any rows with missing data
	- Remove duplicates
	- Rename columns to appropriate names
- NYC Dog Data Base:	
	-This data base consists of NYC dog license, zip_code. borough, breed_name etc.
	- Uploaded NYC_dogs_clean.csv from Kaggle
	- Removed unecessary columns ex:("Unnamed: 0", "CommunityDistrict", "CensusTract2010", etc.)
	- Dropped any rows with "Unknown" or missing values
	- Renamed columns "AnimalName" and "AnimalGender" to "Name" and "Gender"
	- Exported to .csv



## Step 3 Sample queries for finding dog breed options :
-

## Creating a QuickDBD Flow chart:







