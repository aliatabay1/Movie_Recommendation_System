# Movie Recommendation Systems

### I - Introduction

**Problem Statement & Objective**

[Project Proposal](https://github.com/aliatabay1/Movie_Recommendation_System/blob/main/Project%20Proposal.pdf)


A movie streaming platform receives complaints about irrelevant movie recommendations from users. Improving their recommendation system is highly important to decrease the retention rate and keep their current subscribers more engaged.

This project aims to create a movie recommendation system that improves the quality of search results and provides more relevant movies according to users' search history.

<img src="https://user-images.githubusercontent.com/91096434/205394189-3b5c80d0-7d4b-499d-8895-42e44f33a6b1.png" width="600">

### II - Data Wrangling & EDA

[Data Wrangling & EDA](https://github.com/aliatabay1/Movie_Recommendation_System/blob/main/Data%20Wrangling%20and%20EDA.ipynb)

**a) Movies Dataset**

Initially, there were some missing values on homepage, tagline, release date, overview, and runtime columns. I removed these columns from the dataset because they were irrelevant to our analysis. There was just one movie with a missing release data value. After looking up this movie, I saw that most of the information was missing. Therefore I dropped this movie altogether. Then I manually filled the missing values in overview and runtime columns by making a google search. 

<img src="https://user-images.githubusercontent.com/91096434/205394674-e59c5ca2-1dd4-4e2c-b967-7b54cba6b1e8.png" width="700">


Initially, there were some missing values on homepage, tagline, release date, overview, and runtime columns. I removed these columns from the dataset because they were irrelevant to our analysis. There was just one movie with a missing release data value. After looking up this movie, I saw that most of the information was missing. Therefore I dropped this movie altogether. Then I manually filled the missing values in overview and runtime columns by making a google search. 


After graphically visualizing the data, I realized that 3376 of 4803 movies didn’t make any revenue. That meant either this information is not available or they were not shown in theaters. I removed the revenue column from the dataset to make the analysis more coherent.

**b) Credits Dataset**

There were no null and duplicate values in the credit dataset. 



### III - Pre-processing & Modeling

[Pre-processing & Modeling](https://github.com/aliatabay1/Movie_Recommendation_System/blob/main/Pre-processing%20and%20Modeling.ipynb)

Using cleaned data, I built demographic, content based and collaborative recommender systems. 

**a) Demographic Filtering**

I used vote average as the only decisive factor to rank the movies. However, some movies have very low vote count which makes the ranking unfair. To solve the issue I used 99 percentile as my cut off. As a result, I included 481 movies in the ranking. 

![image](https://user-images.githubusercontent.com/91096434/205394885-056e5171-58c4-49ef-b306-ca03e2c26172.png)

This ranking can be used for simple movie recommendation to users who wants to watch high ranked movies. It is not influenced by any user preference or choice therefore It will be basic and same for everyone.

**b) Content Based Filtering**

I built an engine that computes similarity between movies based on certain metrics and suggests movies that are most similar to a particular movie that a user liked. 

Firstly, I used similarity scores of words in overview column that uses movie descriptions to recommend movies that includes the higher number of similar words. I excluded the most common english words from the vectorizer to increase the accuracy of the engine. 

![image](https://user-images.githubusercontent.com/91096434/205395164-c71e506b-c1a9-4a5a-a0de-ceca588afd45.png)

I received similar results to The Godfather movie mostly but Easy Money and Made movies doesn’t really have similar genre and cast with The Godfather.

I decided to add cast, crew and genre columns to my recommendation engine to increase the quality of the results. 

![image](https://user-images.githubusercontent.com/91096434/205395136-4a55db25-56d6-4bfe-81e9-fab3db856b2f.png)



Adding more features significantly improved the results. The new recommendation engine suggested movies with relevant genre and cast.

**c) Collaborative Filtering**

Content based recommendation system has some disadvantages. The engine that we built is not really personal in that it doesn't capture the personal tastes and biases of a user. Anyone querying our engine for recommendations based on a movie will receive the same recommendations for that movie, regardless of who s/he is. 



Collabrative filtering aims to predict how much a user is expected to like a product by considering preferences of similar users. Therefore, I usec collabrative filtering to build a more personilzed recommendation engine considering users' preferences.

I did not implement Collaborative Filtering from scratch. Instead, I used the Surprise library that used powerful algorithms like Singular Value Decomposition (SVD) to minimise RMSE (Root Mean Square Error) and give good recommendations. SVD calculates similarty between both users and movies to give predictions which enables us to use advantages of both user and item based collabrative filtering.
 
After building the algorithm. I randomly picked a user to look at his/her past movie ratings and make predictions using collabrative filtering I created.

![image](https://user-images.githubusercontent.com/91096434/205395283-45f36f99-7b18-44d7-bf41-fb0db9f1c8e7.png)

User 2 mostly rates action movies. Therefore I gave the recommendation engine one action and one romance movie to predict the rating based on the User 2’s past ratings.

![image](https://user-images.githubusercontent.com/91096434/205395333-033ae65a-825d-44f6-bafa-e8be695a0107.png)

User 2 rates Action movie The Fifth Element (3.76) higher than Romance movie The Notebook (3.44) which makes sense if we look at his/her rating history.

One great feature of this recommender system is that it doesn't care what metadata movie contains. It works purely on the basis of an assigned movie ID and tries to predict ratings based on how the other users have predicted the movie.

### IV - Conclusion 
For the movie streaming platform to give more relevant results to subscribers, two recommendation system could be implemented: Content based recommender and Collaborative filtering.  

**Content Based Recommender:** The company can use this algorithm if they want to give recommendations to customers using similarities of movies such as overview, cast, crew and genre. This engine will be the same for all users and will not take into consideration users’ past activity and individual preferences. This engine is a good option if the company doesn’t have a lot of active users, therefore data, to process. 

**Collaborative Filtering:** If the company would like to give more personalized recommendations according to users’ likes, dislikes and view & search history, collaborative filtering is the best option. Also this engine is dynamic and improves as we collect more data about users. This option would be great if the company has significant number of active users which would make the recommendations more relevant. 
