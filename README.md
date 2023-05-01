# Project 2: Recommendation System

## This is task is part of DES431 Big Data Analysis Course
Task:
Propose and implement your own recommendation system based on the MovieLens dataset.
Use ratings_train.csv as the training set, ratings_valid.csv as the validation set.

Your system may use information from movies.csv and tags.csv to conduct recommen-
dations. The undisclosed test set will be used to evaluate your system.

• The data file structure is available at https://files.grouplens.org/datasets/movielens/ml-
latest-small-README.html.

• The main goal of the recommendation system is to minimize the root-mean-square
error.
• The implementation should include a function named predict_rating. This function
accepts a DataFrame with two columns userId and movieId. Then, the function adds
a column named rating storing a predicted rating of a movieId by a userId.
