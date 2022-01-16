## Proposal

### Introduction
Every year, the bulk of book sales is made up by either 'classic' books or new releases that are heavily marketed by the publishing houses behind them. Some authors dedicate years of their lives to create amazing books, that, unless they reach 'classic' status, will not experience significant sales beyond their 1st or 2nd year.
With the pandemic, book sales have spiked, but another driving force behind this is Tiktok's "Booktok", where viral recommendations are [blowing up](https://www.economist.com/books-and-arts/2021/11/06/booktok-has-passion-and-enormous-marketing-power) book sales, even backlisted ones.
A traditional way of exploiting this phenomenon for data scientists would be to provide publishing houses with insights on \#Booktok's emerging trends, so they can focus on quickly releasing books that cater to them. But there is an oportunity to change the industry for the better, so that the focus is not on releasing soulless, haphazardly writen books that technically meet all the criteria a reader is looking for, but to guide them to the masterpieces that were lost in translation. And in turn provide an environment where writers can focus on doing their best work, instead of being pressured to release books quickly and consecutively if they want any revenue.
###### TL/RL
Tiktok's influences are blowing up book sales and making backlisted books best-sellers.

### Question / Need
For an author to get their book on the platform and hopefully trending, they will want to hand out copies of it to influential Tiktokers. The platform revolves around creative video content, so the copies will need to be physical so they can be displayed. To avoid creating negative first impressions and losing out on momemtum, they should be sent to the 'booktokers' who are least likely to create negative video content about them. 'Rants' are popular because they can increase a creator's following, but a video 'raving' about the book can get the ball rolling and create positive chatter around it. 

My project will be a classification model that will determine the probability of a booktoker liking a specific book, '[On the Jellicoe Road](https://www.goodreads.com/book/show/1162022.On_the_Jellicoe_Road)' (2006), which has ratings from 48k Goodreads users.

### Data Description
Most \#booktok accounts contain a link to their Goodreads profile, where their reading habits and past ratings are recorded, so this is where the modelling data will come from. Each book has a series of tags / genres.

##### In the model
Each observation will be a user that has rated 'Jellicoe Road', where the features will be engineered from past ratings and the target will be whether they gave a positive rating to our book (1), or not (0).

Some of the features to be tried in the model:
- Total # of books read.
- Max # books read/year
- Avg rating to the genres in our target book.
- Has read / has given (+) rating to book sagas.
- Difference between their rating and the book's average rating, aggregated over each genre. This will tell us if the user has a negative or positive bias for each genre, and how big it is.
- Avg length of highest rated books.
- Median time to complete a book. This would tell us if they're a fast reader.

##### Raw
Here I have scraped some of the reviews for a book, where the url of each reviewer is contained:
![book reviews](Screenshots/20220109213707.png)

Here is one of those reviewer's reading history, where each row is a book, and each column is information about the user's reading of the book (date they started it / how they rated it) and the book itself (avg rating, # ratings, genres, etc).
![reviewers' history](Screenshots/20220109214642.png)

### Tools
- `tiktok-scraper` by [Drawrowfly](https://github.com/drawrowfly/tiktok-scraper) to scrape \#booktok content on Tiktok.
- Goodreads API, along with Selenium and BeautifulSoup to get around its limitations. (Amazon, Goodreads' owner, does not make acquiring this data easy).
- Pandas, Seaborn & Matplotlib for EDA and feature engineering.
- Scikit-learn for building various classification models.

### MVP Goal
For the MVP I would like to present some baseline models with few features:
- kNN
- Logistic Regression
- Random Forest

Hi everyone! My project is a classification model to predict whether a reader will like a specific book based on their Goodreads reading history. Tiktok’s 'BookTok' has been making [backlisted books into bestsellers](https://www.economist.com/books-and-arts/2021/11/06/booktok-has-passion-and-enormous-marketing-power), so the idea is that an author can use the model and a 'BookToker's Goodreads profile (usually linked in their bio) to select the most likely to give their book a positive rating so they can send them a hardcoopy. This is in the hopes that they will create positive content around the book and increase its visibility (and maybe make it go viral!).