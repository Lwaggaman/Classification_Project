## Project Description
#### Abstract
The bulk of book sales is made up by either 'classic' books or new releases, but Tiktok has been making [backlisted books into bestsellers](https://www.economist.com/books-and-arts/2021/11/06/booktok-has-passion-and-enormous-marketing-power). I believe this has the potential to provide an environment where writers can focus on doing their best work, instead of being pressured to release books quickly and consecutively, and readers get less books of better quality. My project is a classification model to predict whether a reader will like a specific book based on their reading history, so an author can use the model and a 'BookToker's Goodreads profile (linked in their bios) to select those most likely to give their book a positive rating so they can send them a hardcopy to create social media content.

#### Design
My project is a classification model to determine the probability of a booktoker liking a specific book, '[On the Jellicoe Road](https://www.goodreads.com/book/show/1162022.On_the_Jellicoe_Road)' (2006). Each observation is a reviewer of the book, to be classified as liking the book if they rated it 4-5 stars (1), and not liking the book if they rated it 1-3 stars (0).

#### Data
- Reviews of the target book, with reviewers' rating and user ID. (4351, 2)
- Reviewrs' reading history, with the books' IDs. (458921, 11)
- Books' data. (8503, 15)
#### Algorithms
*Feature Engineering*
Based on readers' past reviews, I was able to engineer features at the reader level. For granularity in capturing a readers' tastes, aggregations were made at the subgenre level, aiming to quantify the reader's behavior by contrating their rating against a book's rating distribution.

*Feature Selection*
With over 900 features, shap values grouped by type of statistic were used to find those most effective.
To further reduce dimensionality, highly correlated subgenres were dropped, based on the times they were labeled together (each book has 10 subgenres) through Pearson coefficients.

*Models*
Logistic regression, k-nearest neighbors, and random forest classifiers were used before settling on XGBoost because it allowed for MNAR, structurally important values. 

*Model Training and Performance*
The final dataset was split 60/20/20 to train the model on the training set, using the test set as a performance benchmark, using the validation set only at the end to test out-of-sample performance on the final model, once it had been trained on the training+test set. I tuned hyperparameters itearing over 10-fold CV models, then conducting a randomized search cross validating the best performing ones or values near them.
Test set predictions had an F1 score, with a .8 precision score (the relevant metric for our purposes) with threshold adjustment.
Validation set predictions had an F1 score, with a .8 precision score with threshold adjustment.

#### Tools
- Selenium, BeautifulSoup, and Goodreads API for data extraction. 
- Numpy, Pandas, and SerialBinarizer for data wrangling and feature engineering.
- Shap for feature selection and model interpretability.
- Scikit-learn library and xgboost API for modeling.
- Matplotlib and Seaborn for visualizations.