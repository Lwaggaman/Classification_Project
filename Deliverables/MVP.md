## Classification Project MVP
The goal of this project is to create a classification model to predict whether readers will like a specific [book](https://www.goodreads.com/book/show/1162022.On_the_Jellicoe_Road) based on their Goodreads reading history.
**Target** - 1 if reader rated target book 4-5 stars, and 0 for lower ratings.

#### Peliminary Feature Engineering
I engineered 6 features at the reader level:
- Avg publication year of books read.
- Avg rating they give to books read.
- Avg rating bias (their rating compared to books' avg rating).
- Avg length of books read.
- Avg \# ratings in books read (measure of book popularity).

#### Performance
I used the features to train 4 different typer of classifiers and compared their performance on a test set, without any hyperparameter tuning.

![bar plot](Visualizations/20220115155055.png)

The Random Forest Classifier had the best performance across the board, while the Logistic Regression model had 0 accuracy. While this may be in part due to a slight imbalance in the dataset, and improves as we adjust the cutoff, it implies that the feature-target relationship is not linear.

In the ROC Curve we can appreciate how the models have better performance than a naive, random guess model at different thresholds.

![ROC Curve](Visualizations/20220115160148.png)

#### Next Iterations
I believe I can improve model performace by engineering features at the reader-genre level, dealing with the slight class imbalance, regularization, and other hyperparameter tuning. While doing this, I should balance complexity, and avoid overfitting to my test set with techniques like cross-validation and pruning (for tree-based models, which seem to be the best suited for this problem).
