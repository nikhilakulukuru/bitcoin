# ml-bitcoin

## Classifying the Price Movement of Bitcoin

### ABSTRACT

During the seven years from April 2015 to April 2022, the standard deviation of Bitcoin’s daily return rate was 3.85%, which was 3.36 times the standard deviation of the S&P 500 return. Using hourly percentage change as a measure of volatility, maximum volatility on Bitcoin close price is observed on Mar 12, 2020, where the price changes by 21.10% within an hour. Unlike traditional assets, it is more reasonable to access the Bitcoin price movement on an hourly basis due to the sharp fluctuation of the cryptocurrency price. [A]

Machine learning methods have been applied increasingly within the crypto market, due to their ability to learn complex, high-dimensional relationships. Politis et al. (2021) [1] applied a Long-Short Term Memory (LSTM) model to predict the price of Ethereum and achieved an accuracy of 84.2%. Patrick et al. (2021) [2] analyzed the predictability of the bitcoin market across different prediction horizons ranging from 1 to 60 minutes. Aggarwal (2019) [3] studied the relationship of the gold price with Bitcoin price movement using Convolutional Neural Network (CNN), (LSTM), and Gated Recurrent Unit (GRU). Liu et al. (2021) [4] later expanded the range of covariates to 40 explanatory variables including the macro market index (i.e. S&P 500 price) and crude oil price for Bitcoin price prediction.

While previous studies focused on exploring the correlation between Bitcoin and traditional assets, its relationship with investors' sentiment and other cryptocurrencies' prices has been neglected. Here, we assess the predictability of hourly price trends of Bitcoin using social media sentiment, foreign exchange rate, as well as the price movement of other major cryptocurrencies. In this project, we would like to classify the direction of bitcoin price movement in the near future using various economic and financial indicators.

The majority of our models achieved accuracy rates of around 80%. However, the main limitations in our model were scarcity of data points, less relevant features, and highly noisy features. Additionally, the feature selection provided by some models shows us that the price change of other crypto coins affects the price of bitcoin the most. This suggests high correlation and potentially high collinearity between these inputs and our response variable; therefore, extensive assessments are highly suggested in order to improve the current model.

### DATA

We extracted data from Bloomberg, Augmento AI [5], and kucoin.com [6] ranging from Jan 01, 2019, to Nov 29, 2022. Our Bloomberg dataset includes hourly data for the VIX index, USD/GBP exchange rate, and the 10-year bond yield. From Augmento AI, we obtained the hourly cryptocurrency sentiment on Reddit, Twitter, and Bitcointalk. Combined with the hourly Bitcoin (BTC), Ethereum (ETH), Ripple (XRP), and Cardano (ADA) price data from kucoin.com, the dataset comprises 26 covariates. While cryptocurrency markets remain open 24/7, the VIX options and the 10-year Treasury bond are not traded over the weekend. In such cases, we forward-filled the missing values using the latest historical data.

Upon calculating the percentage change of Bitcoin close price, we encoded the price direction with binary labels - 1 as upward movement and 0 as downward movement. This formulates the prediction problem into a binary classification problem. Since the range of the cryptocurrencies’ daily closing prices varies significantly, we compute the percentage change of price with respect to each coin. Additionally, to preserve the cyclical nature of weeks, we constructed a datetime feature to represent the day of week information. When decomposing the time series Bitcoin price [B], we see that the price trend is mainly driven by trend and does not possess any obvious seasonality. Additionally, we scaled all the columns and normalized them.

### FINDINGS

In our empirical analysis, we analyze the short-term predictability of the bitcoin market, leveraging different machine learning models. Based on the evaluation metrics - ROC, F1-score, we conclude that Logistic Regression and XGBoost slightly outperformed other methods. From the feature importances graphs, we see that technical indicators (change of other major cryptocurrencies price) remain prevalent in predicting the Bitcoin price movement.

Traditional time series models like ARIMA were not used as the time series Bitcoin price does not show obvious seasonality during time series decomposition [B]. While more complex models like QDA random forest are known to better capture high-dimensional relationships in the data, they (especially deep learning models) are notoriously data-hungry. Data augmentation techniques and generative models like Generative adversarial networks (GAN) can be used to generate synthetic data for further model training. With a larger dataset and more relevant covariates, more techniques (e.g. attention mechanism in NN) and frameworks (e.g. transformer, temporal convolutional network) can also be employed to better capture the long-term temporal dependencies of the financial data.

Since hourly data can be highly noisy, we recommend applying smoothing methods like simple exponential smoothing and adaptive bandwidth local linear regression to reduce the noise in the training data. In addition, the data preprocessing method can also be further enhanced by implementing a rolling window approach for train and test sets instead of using a fixed number of data points, which could potentially improve the models significantly given the time series nature of our data.


### REFERENCES
[1] Politis, A.; Doka, K.; Koziris, N. Ether price prediction using advanced deep learning models. In Proceedings of the 2021 IEEE International Conference on Blockchain and Cryptocurrency (ICBC), Sydney, Australia, 3–6 May 2021; pp. 1–3.

[2] Patrick Jaquart, David Dann, and Christof Weinhardt (2021, March 18). Short-term bitcoin market prediction via machine learning. The Journal of Finance and Data Science. Retrieved February 28, 2023, from https://www.sciencedirect.com/science/article/pii/S2405918821000027

[3] Aggarwal, Apoorva, Isha Gupta, Novesh Garg, and Anurag Goel. 2019. Deep Learning Approach to Determine the Impact of Socio-Economic Factors on Bitcoin Price Prediction. Paper presented at 2019 Twelfth International Conference on Contemporary Computing (IC3), Noida, India, August 8–10.

[4] Liu, Mingxi, Guowen Li, Jianping Li, Xiaoqian Zhu, and Yinhong Yao. 2021. Forecasting the price of Bitcoin using deep learning. Finance Research Letters 40: 101755.

[5] “Bitcoin Sentiment – Bull & Bear Index.” Augmento, 14 Apr. 2020, https://www.augmento.ai/bitcoin-sentiment/.

[6] Crypto Exchange: Bitcoin Exchange: Bitcoin trading. KuCoin. (n.d.). Retrieved February 28, 2023, from https://www.kucoin.com/
