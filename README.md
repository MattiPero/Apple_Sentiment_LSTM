# Do Social Media Sentiment Variables Improve Daily Stock Price Predictions?
### An empirical Evaluation using Twitter Data, Vader, and LSTM Networks on Apple Stock ($AAPL)

This study investigates whether incorporating sentiment-based variables can enhance the prediction of future stock price movements. To this end, we first extract daily sentiment indicators. We then compare the performance of two predictive workflows: the first relies exclusively on financial variables obtained from Yahoo Finance, while the second combines these variables with the extracted sentiment indicators. By comparing the two approaches, we assess whether the inclusion of sentiment information leads to more accurate daily stock price forecasts.

## Methodology

1. The first stage of the analysis involves the extraction of sentiment variables. To this end, we apply the pre-trained VADER sentiment analysis model to tweets related to Apple (AAPL). VADER assigns a sentiment score to each individual tweet. To account for the varying influence of different tweets, we construct a proxy for tweet popularity by summing three engagement metrics: the number of comments, retweets, and likes. This popularity measure is then used as a weight when aggregating individual sentiment scores into a daily sentiment indicator. Specifically, the daily sentiment variable is computed as the popularity-weighted average of all tweet sentiment scores published on the same day. This approach ensures that tweets generating greater user engagement have a proportionally larger impact on the daily sentiment measure.

The **Dataset** used for this analysis was obtained from Kaggle ("insert dataset link"). After preprocessing and applying the sentiment extraction and aggregation procedure described above, we produced a new dataset, hereafter referred to as "daily_APPLE_sentiment.csv". This dataset contains the daily sentiment indicator alongside the corresponding date, making it suitable for integration with the financial data used in the subsequent analysis.

2. 
