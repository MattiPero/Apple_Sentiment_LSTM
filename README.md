# Enhancing Apple Stock Price Forecasting with Twitter Sentiment Analysis and LSTM Networks

## Project Description

The aim of this project is to investigate whether information extracted from Twitter sentiment can improve the prediction of **Apple**'s stock price.

The analysis is based on a publicly available Kaggle dataset containing tweets about several companies, including engagement metrics such as likes, comments, and retweets. Only tweets related to Apple were considered.

Each tweet was analyzed using **VADER (Valence Aware Dictionary and sEntiment Reasoner)** to compute a sentiment score. These scores were then aggregated at the daily level using a popularity-weighted average, where the weight of each tweet is the sum of its likes, comments, and retweets.

The resulting daily dataset includes:

the weighted sentiment score;
the number of tweets published each day.

This information was combined with Apple's historical closing price to compare two **LSTM (Long Short-Term Memory)** forecasting models:

a baseline model using only historical closing prices;
an enhanced model that also includes the sentiment score and tweet count.

The objective is to evaluate whether incorporating social media sentiment improves forecasting performance.

## Datasets
**1. Twitter Dataset**

Sentiment information was extracted from the following Kaggle dataset:

Dataset: [Tweets about the Top Companies from 2015 to 2020]
Source: [https://www.kaggle.com/datasets/omermetinn/tweets-about-the-top-companies-from-2015-to-2020?select=Tweet.csv]

After filtering Apple-related tweets and applying the sentiment analysis pipeline, a new daily dataset named [daily_APPLE_sentiment.csv] was created. It contains the weighted daily sentiment score and the daily number of tweets.

**2. Apple Stock Price Dataset**

Historical stock prices were obtained from **Yahoo Finance**.

Dataset: [AAPL_yahoofin.csv]

Only the daily closing price was retained and merged with the sentiment dataset to build the forecasting models.

## Tools and Technologies

The project was developed in two stages using different tools.

**Sentiment Analysis**

The preprocessing of the Twitter data, sentiment extraction, and the creation of the daily sentiment dataset were performed in **Jupyter Notebook** using **Python**.

Forecasting

The forecasting workflows and the comparison between the two LSTM models were implemented in **KNIME Analytics Platform**.

# Methodology

**1. Sentiment Feature Extraction**

Starting from the [Tweets about the Top Companies from 2015 to 2020] dataset, an initial data cleaning step was performed before applying the VADER sentiment analysis algorithm to each tweet, obtaining a sentiment score for every observation.

Next, an engagement variable was created by summing the number of likes, comments, and retweets, providing a measure of each tweet's popularity.

Finally, the tweet-level information was aggregated on a daily basis by computing:

the total number of tweets published each day;
a daily sentiment score obtained as the engagement-weighted average of the individual tweet sentiment scores.

**2. Forecasting Workflow**

The forecasting phase was implemented in KNIME Analytics Platform and consists of a common preprocessing pipeline followed by two alternative LSTM workflows.

The common preprocessing steps are:

The closing price was transformed into logarithmic returns to improve the training process.
A 30-day rolling standardization was applied to the log returns in order to reduce the impact of changes in scale over time.
A 10-day lag window was created, generating the input sequences required by the LSTM model.

After these preprocessing steps, the workflow splits into two different forecasting pipelines.

**2.1 Baseline Model**

The baseline forecasting model uses only the historical log returns as input.

After the preprocessing stage, the data was split into training and test sets. An LSTM neural network with a hidden layer of 16 neurons was then trained on the training set and evaluated on both the training and test sets to monitor potential overfitting.

The predicted values were subsequently transformed back to the original scale. To avoid data leakage, the denormalization of the predictions was performed using the mean and standard deviation computed from the previous day.

Finally, for a more intuitive interpretation of the results, the predicted log returns were converted back into closing prices and compared with both the actual prices and a naïve forecasting model.

**2.2 Sentiment-Enhanced Model**

The second workflow extends the baseline model by incorporating sentiment-related features.

The preprocessed log returns and their 10 lag values were combined with the dataset [daily_APPLE_sentiment.csv], containing the daily tweet count and the daily weighted sentiment score.

A 30-day rolling standardization was then applied to both additional variables to normalize their values while preserving the temporal structure of the time series. Subsequently, 10 lag features were generated for each variable to create the input sequences required by the LSTM model.

From this point onward, the workflow follows the same steps as the baseline model, including the train/test split, LSTM training, overfitting evaluation, prediction denormalization, and comparison with the naïve model.

## Results

The comparison between the two LSTM workflows shows that the inclusion of Twitter-based sentiment features does not provide a significant improvement over the baseline model based only on historical price information.

Both approaches achieve very similar performance in terms of explained variance and directional accuracy, suggesting that the additional sentiment variables extracted from Twitter do not add substantial predictive power within the considered framework.

One possible explanation is related to **market efficiency**. In highly followed and liquid markets, such as Apple's stock market, publicly available information may already be rapidly incorporated into the stock price, limiting the additional value of sentiment extracted from social media. Furthermore, the sentiment of a company may not be fully represented by tweets explicitly mentioning its name, as relevant information can also emerge from broader market discussions, news, or sector-related events.

Another possible limitation concerns the sentiment extraction approach. The use of VADER provides a general-purpose sentiment measure, but more advanced language models specifically designed for financial texts could potentially capture nuances such as uncertainty, expectations, or market-related opinions more effectively.

Future improvements could involve exploring alternative sentiment analysis techniques, incorporating additional sources of information, or investigating different financial variables. For example, sentiment information may have a stronger relationship with **trading volume**, **volatility**, or short-term market reactions rather than directly improving stock price prediction.
