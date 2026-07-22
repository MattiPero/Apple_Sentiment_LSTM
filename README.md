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
