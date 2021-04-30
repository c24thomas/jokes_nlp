# Project 3 - Web Scraping and APIs


## Problem Statement

I was hired by ***greeting card company*** to classify whether or not a joke is a 'dad-joke'. Father's day is approaching; the company wants to run a dad-joke-based ad campaign. No one at the company can agree on what consititutes a *dad-joke*. So, the goal of this project is to properly classify jokes as either 'dad-jokes' or 'standard jokes', based off of data pulled from Reddit posts.


## Datasets Used:

* [`jokes.csv`](./data/jokes.csv): Posts from [`r/Jokes`](https://www.reddit.com/r/jokes)
* [`dadjokes.csv`](./data/dadjokes.csv): Posts from [`r/DadJokes`](https://www.reddit.com/r/dadjokes)
* [`full.csv`](./data/full.csv): Combined .csv containing all posts


## Preliminary Findings:

It turns out that it's pretty difficult to classify the caliber of a joke based solely on vocabulary. We had plenty of models that outperformed the null model (simply guessing the majority class (51%)), but were unable to achieve above 65% test accuracy on any of the models we tested.

Here we have our top 3 models, their parameters, and train/test accuracy scores:

(The LogisticRegression model used all default CountVectorizer hyperparameters, except stop_words=english)

| KNN | LR | RFC |
|---|---|---|
| weights: uniform | C: 0.05 | n_estimators: 750 |
| p: 2 | class_weight: balanced | min_samples_split: 4 |
| n_neighbors: 7 | penalty: L2 | min_samples_leaf: 3 |
| - | solver: liblinear | max_features: auto |
|-|-| max_depth: 25 |
|-|-|-|
| cvec__stop_words: None | cvec__stop_words: english | cvec__stop_words: None |
| cvec__ngram_range: (1, 3) | - | cvec__ngram_range: (1, 1) |
| cvec__min_df: 1 | - | cvec__min_df: 3 |
| cvec__max_df: .95 | - | cvec__max_df: 0.9 |
| cvec__max_features: 5,000 | - | cvec__max_features: 5,000 |
|-|-|-|
| **Train Accuracy** | **Train** | **Train** |
| 0.6646 | 0.7371 | 0.6990 |
| **Test Accuracy** | **Test** | **Test** |
| 0.5531 | 0.6458 | 0.6367 |
| **Test F1 Score** | **Test** | **Test** |
| 0.4437 | 0.5935 | 0.5643 |


## Conclusion

In summary, I think that this project is a good proof of concept. It shows that with the right data and appropriate modeling, classification *is* possible here. As it stands now, I would recommend the company use the RandomForestClassifier model, as it performed the best (of the models we tried) with regard to accuracy and bias/variance. The LogisticRegression model had a slightly better accuracy score, but was more overtrained (higher variance) than the RFC model. In the future, I plan on revisiting this problem with more robust modeling techniques and NLP tools to try to improve model performance.
