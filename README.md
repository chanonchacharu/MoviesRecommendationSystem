# Movie Recommendation System


Task: Propose and implement your own recommendation system based on the MovieLens dataset.
Use ratings_train.csv as the training set, ratings_valid.csv as the validation set.

Your system may use information from movies.csv and tags.csv to conduct recommen-
dations. The undisclosed test set will be used to evaluate your system.

• The data file structure is available at https://files.grouplens.org/datasets/movielens/ml-latest-small-README.html

• The main goal of the recommendation system is to minimize the root-mean-square
error.
• The implementation should include a function named predict_rating. This function
accepts a DataFrame with two columns userId and movieId. Then, the function adds
a column named rating storing a predicted rating of a movieId by a userId.

## Implementation
In this section, we will discuss about the project implementation, specifically how the recommendation model is constructed. 
### Model Architecture
We have to create utility matrix where the rows are userId, the columns are movieId, and the values inside is rating which the user gave to the movie. In the case where the pair of userId and movieId doesn't exist in the dataset provided, the value would be NaN.
#### 1. Global Bias

> **Final Predicted Rating** = Global Mean + User Bias + Item Bias

* User Bias = Target User Mean - Global Mean
* Item Bias = Target Item Mean - Global Mean
#### 2. Item-based Collaborative Filtering

> **Final Predicted Rating(user, item)** =  SUM(similarity of movie and
> target movie* User rating for target movie) / SUM(similarity of movie
> and target movie)

In our implementation, number of similar items was 15. In order to deal with missing rating, skipping to the next available rating of movie with high similarity score is the implemented approach. 

#### 3. User-based Collaborative Filtering

> **Final Predicted Rating(user, item)** =  AVERAGE(target user rating ) + SUM(similarity of user and target user User * (User rating for target movie - AVERAGE(rating of target movie)) / SUM(similarity of user and target user)


Unlike item-based collaborative filtering, number of similar was 10 in this implementation.

#### 4. Latent Factor Model
This is the matrix factorization algorithm. SVD class from Surprise library was selected for this task. Please refers to the official documentation of [SVD Surprise](https://surprise.readthedocs.io/en/stable/matrix_factorization.html#surprise.prediction_algorithms.matrix_factorization.SVD).

#### Final. Ensemble Recommendation System

> **Final Predicted Rating(user,item)** = w1 * r_bias(user,item)  + w2 *
> r_item(user,item)  + w3 * r_user(user,item)  + w4 *
> r_latent(user,item)

After construction the four models independently, the models are combined into one final model, given the weighting factor, and sum all the predicted rating. 

CONSTRAINT: the sum of all weight must be added to one

The assigned weight we adjusted according to the RMSE of each model. In this implementation, the item-based collaborative filtering had the lowest RMSE; hence, it was given the highest weight. Another approach is using equally weighted, 0.25 for each model. Regardless, fine-tuning is necessary for finding the optimal weight that would yield the lowest RMSE. 

## Discussion
Collaborative filtering relies on the knowledge of pass behaviors or preferences of users. Hence, the system would not be applicable to new users with no rating on any movie. This is one of the problem that our recommendation system hadn't address since our testing set is guarantee to have the user that was being used in the training process of the model. 

In this case, content-based system might be good alternative as it depends on the constructed features (like genres) of the movie in our movie database. For this project, we experimented with content-based system but the accuracy measurement proved the method to be underwhelming with lower score than the benchmark given by the professor. 

## Mention
This task is part of DES431 Big Data Analysis. 

Submitted to: Assoc. Prof. Dr. Cholwich Nattee

Sirindhorn International Institute of Technology, Thammasat University

Group Members:
1. 6322770064 Pauruetai Kobsahai
2. 6322770114 Thanakrit Loetpricha
3. 6322770692 Chanon Charuchinda
4. 6322772367 Rawikarn Keitiwattanapong
