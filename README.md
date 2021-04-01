# StocksPrediction

Stock Market Prediction

Dataset
WIKI Prices (Stock market prices) from QUANDL. Google, Walmart, and Microsoft. Tickers: “WIKI/GOOGL”, “WIKI/WMT”, “WIKI/MSFT”.
Website: https://www.quandl.com/databases/WIKIP 

Introduction
The stock market is a place surfed by investors from around the world. Everyone wants to buy good stocks at low prices and at the right time sell them at a high price. Some just want to have the dividend gains, where it is possible to generate a passive income without much constant analysis as is done by traders, who basically want to make money in the short term.
For this project, the intention is not to get rich overnight, however much the accuracy of the forecasts are higher than 90% in its average, but to have a start for better research and development on the subject and who cares or invest in this market.
The chosen dataset was the stock market price history of the United States. Companies like Google, Walmart and Microsoft and their quotes for the last 10 years, even though some of these companies have data available since 1999. The 10-year period is a good time to analyze and create a model for future analysis.
There are two types of analysis that are performed by professionals: Technical analysis (based on stock charts traded over time) and Fundamental Analysis (based on company fundamentals data, annual balance sheets, earnings, dividends paid, price history and others).
In this dataset, despite having several features, the following were chosen for prediction, based on daily prices: date (as an index), adj_close, and adj_volume. In addition, the following features were added based on a new calculation coming from adj_high, adj_close, and adj_open, thus creating features called volatility percentage prices (vol_per) and percentage change (pct_change). These features are often used by technical analysts to predict future prices in the short to medium term.
An excerpt from the original and modified dataset is shown below:
ticker	date	open	High	Low	close	Volume	ex-dividend

GOOGL	2008-03-03	471.51	472.72	450.11	457.02	15093800	0
GOOGL	2008-03-04	450.95	453.36	435.78	444.6	27216100	0
GOOGL	2008-03-05	445.25	454.17	444	447.69	14858300	0
		split_ratio	adj_open	adj_high	adj_low	adj_close	adj_volume
		1	236.485	237.09	225.75	229.21	15093800
		1	226.17	227.38	218.56	222.98	27216100
		1	223.31	27.78	222.68	224.54	14858300
Source: QUANDL, Google Company Stock Market Prices – original data

O calculus used in Python to obtain the new features were the following:
df['pct_vol'] = (df['Adj. High'] - df['Adj. Close']) / df['Adj. Close'] * 100.0

df['pct_change'] = (df['Adj. Close'] - df['Adj. Open']) / df['Adj. Open'] * 100.0

ticker	date	adj_close	pct_vol	pct_change	adj_volume
GOOGL	2008-03-03	229.21	3.43	-3.07	15093800
GOOGL	2008-03-04	222.98	1.97	-1.4	27216100
GOOGL	2008-03-05	224.54	1.44	0.55	14858300
Source: Data prepared to start the predictions – prepared data

The purpose of this report is to analyze the data of three different companies in the stock market, make the prediction in business days of 2 days, 5 days (1 week), 21 (1 month) and 252 days (1 year) using two types of regression classifiers: Linear Regression and Support Vector Machine.
The dataset was pre-prepared on a smaller scale for a more accurate analysis of the data with this line in Python:
X = preprocessing.scale(X)

With this pre-processing, we have this format data:
[[-0.99142704  2.30348496 -2.19030633  2.62415781]
 [-1.01565439  0.92729282 -0.99348831  5.69797918]
 [-1.0096075   0.433998    0.41423361  2.56444266]
 ...
 [ 2.10963922  2.75782338 -1.67823336 -0.59114992]
 [ 2.21675058 -0.46196001  0.25750193 -0.37336282]
 [ 2.03337001  4.44998945 -3.82978603 -0.45740828]]

After the dataset is prepared and scaled, we can use the two algorithms cited above: Linear Regression and Support Vector Machine. We have used algorithms of regression because we do not have data classified with a right answer, precisely because it deals with values in dollars that can vary infinitely down or up.
For Linear Regression, the parameters were the default ones, like this code in Python:
clf_lin = LinearRegression()

For Support Vector Machine, we tried with two different parameters, using “linear kernel” with C=1e3 and “rbf kernel” with C=1e3, gamma=0.1.
clf_svr_lin = svm.SVR(kernel='linear', C=1e3)
clf_svr_rbf = svm.SVR(kernel='rbf', C=1e3, gamma=0.1)

Results
The following results were obtained using these parameters and the chosen period of forecasted dates. The green line represents the actual prices while the others are the predictions. In the top of the chart, we have the accuracies of each algorithm and the predicted days.
 
Company: Google
 
 
 
 
Company: Walmart
 
 
 
 
Company: Microsoft
 
 
 
 
Conclusion

Analyzing each graph and its resourcefulness, the SVR algorithm with the "rbf" kernel was the most successful in making predictions in short-term (2 and 5 days) and long-term (252 days). In general, all three different classifiers acted very well, not always giving the exact price of the action, but the tendency of each company, either positive or negative.
In fact, the use of this classifiers will not make anyone rich overnight, but it can help in the stock-picking process both in the short term and in the long run.
Speaking personally, this project taught me how to treat the dataset in a way that is more coherent and accurate to collect predictions with better quality. Scaling the data also helps you to have more accurate calculations. Moreover, when we have an additional knowledge of the data area we are working on it makes it easier to understand what to look for in a huge dataset. As I like to invest in stocks and follow this market, I found it fascinating to be able to forecast prices of stocks that I am interested in buying.
