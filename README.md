# Project 2 : No Dogs Left Behind!
 No Dog Left Behind Project- Data for dog adoption use
 
 Group members:
 - [Jackelyne Gutierrez](https://github.com/Jackelyneg)
		
- [Juliana Puskar](https://github.com/Anikraze)
		
- [Tricia Toffey](https://github.com/ttoffey)

![image](https://user-images.githubusercontent.com/76538768/123885840-47b09a80-d91c-11eb-8afd-701558b58d83.png)

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
- First create a table schema on pgAdmin for AKC web scrape
		
		Create table dog_breds_akc(
			breed_id  INT,
			breed  VARCHAR,
			breed_rank INT
			);
			


Selects the top 5 breeds accoring to 2017 AKC:
			
		select * from dog_breds_akc
		select * from dog_breds_akc
		where breed_rank <= 5;
Look up any dog breed to see if it is top ranked:
		
		select * from dog_breeds_akc
		where breed = ['insert breed name']
		
Example:
		
		select * from dog_breds_akc
		where breed = 'Shih Tzu'
		


![image](https://user-images.githubusercontent.com/81592631/123883359-db7f6800-d916-11eb-81a9-d89283cedb56.png)




## Creating a QuickDBD Flow chart:

Created the schema for 3 tables - akc_table, nyc_data_table and characteristics_table; 
the akc_table and characteristics_table were joined via breed_rank; 
we were not able join the nyc_table via a foreign key but did use in SQL queries - the "breed names" are not consistent in all three tables.

We uploaded the QuickDBD to PGAdmin to create the tables and then uploaded the data.

Sample Queries:

- Selects breed_rank, breed_name, and average_price for top 5 breed ranks and the price below $2000:

		select a.breed_rank, c.breed_name, c.average_price
		from akc_table as a
		left join characteristics as c
		on a.breed_rank = c.breed_rank
		where a.breed_rank <= 5 AND c.average_price < 2000
		order by a.breed_rank;

![image](https://user-images.githubusercontent.com/67808647/123884854-349ccb00-d91a-11eb-84d3-f89e2c0deda4.png)


- Selects breed_name, breed_rank and NYC borough for top 5 breed ranks according to AKC by NYC borough:

		select c.breed_name, c.breed_rank, n.borough
		from characteristics as c
		left join nyc_table as n
		on c.breed_name = n.breed_name
		where c.breed_rank <= 5
		order by n.borough, c.breed_rank;

![image](https://user-images.githubusercontent.com/67808647/123884929-60b84c00-d91a-11eb-8f06-e8cc552b0208.png)
![image](https://user-images.githubusercontent.com/67808647/123884996-834a6500-d91a-11eb-84f0-647449a22467.png)


- Selects all Shih Tzu's by NY borough with average price.
		select n.breed_name, n.borough, c.average_price
		from characteristics as c
		left join nyc_table as n
		on c.breed_name = n.breed_name
		where c.breed_name = 'Shih Tzu';
		
![image](https://user-images.githubusercontent.com/67808647/123886278-1d131180-d91d-11eb-9334-7bd88fbadaae.png)
	


