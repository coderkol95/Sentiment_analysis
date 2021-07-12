# Business problem

I have always been fascinated by the stock market. I also traded for major part of 2020. I booked profits and suffered losses too. Along with a friend at work, we always tried to predict the movement of BANK NIFTY and a few other tickers. He went to do his MBA and I changed my plans from MBA to building a career in analytics. This project is my first attempt at trying to predict the stock market movement on a daily basis based on sentiment analysis of news. 

# Methodology

This is a long term project. Currently I have tested the waters with a comparison of sentiment based analysis between rule based and atutomated models. 
The dataset used is Apple's news. In the rule based analysis I have trained a machine learning model on the data. 
In the automated analysis I have gauged each news article's sentiment polarity and objectivity. Then I have run it through a sigmoid transformation to get a probability value.
When the probability is above a particular threshold, it predicts the positive class.

# Wordcloud vizualized

![image](https://i.ibb.co/1bcv5DM/aples.png)

# Model testing

## Rule based model performance

Model| Accuracy|	Precision|	Recall|	F1 score|
|---|---|---|---|---|
GaussianNB|	0.883871|	0.888646|	0.992683|	0.937788|
Random Forest|	0.877419|	0.881210|	0.995122|	0.934708|
SVM|	0.873118|	0.887417|	0.980488|	0.931634|
GBM|	0.875269|	0.909302|	0.953659|	0.930952|
DecisionTree|	0.851613|	0.891954|	0.946341|	0.918343|
Adaboost|	0.851613|	0.895592|	0.941463|	0.917955|
BernoulliNB|	0.855914|	0.927681|	0.907317|	0.917386|
Logistic|	0.843011|	0.896471|	0.929268|	0.912575|
KNN|	0.763441|	0.926136|	0.795122|	0.855643|

We'll use GBM based on the above table as it scores >=0.90 in precision, recall and F1 score. Also, a very high recall and stagnant precision score indicates that those models predict the negative class for almost all the observations in the test set.

       
## Automated model performance

After each sentiment is run through the sigmoid transformation:

![prob](https://i.ibb.co/SrX5hfv/prob.png)

I have used a threshold of 0.5 for the positive class. But very small changes in the probability threshold drastically change the classifications.

The result of lexicon based sentiment analysis:

F1 score:  0.905885156063855

Precision:  0.8837749883774988

Accuracy:  0.8299612569952648

As we can see that the performance is very comparable. Automated sentiment analysis will be very helpful in the cases of cold start and it is also easier to use. However it may require regular tweaking of the probability threshold to keep making money in the market.




# Web scraping

To do sentiment analysis and predict stock movement we are scraping the [live](https://economictimes.indiatimes.com/markets/stocks/liveblog) blog of ETNow at a daily basis. We are using Beautiful Soup to scrape the news headlines. Then we are doing sentiment analysis for each headline and fltering out the 0 values. Then these sentiments are passed through a sigmoid transformation to get a probability of market's downward movement the next day. If the probability>=0.519 we are predicting that the market will go down the next day.

# Deployment

The model is deployed using streamlit at:https://share.streamlit.io/coderkol95/data-science-projects/news_app.py

It accepts the URL for the blog and using regex retrieves the second page. Then it performs sentiment analysis, plots a graph of the sentiment distribution and gives the mean sentiment and prediction value.

|Sr. No.|Data|Maket movement|Sentiment mean|Predicted market movement|Incorrect|
|--|--|--|--|--|--|
1|31-May-2021|	Up|	0.5164|	Up|	-|
2|1-Jun-2021|	Down|	0.5274|	Down|	-|
3|2-Jun-2021	|Down|	0.5130|	Up|	1|
4|3-Jun-2021|	Up|	0.5137|	Up|	-|
5|4-Jun-2021|	Down|	0.5252|	Down|	-|
6|7-Jun-2021|	Up|	0.5110|	Up|	-|
7|8-Jun-2021|	Down|	0.5221|	Down|	-|
8|9-Jun-2021|	Down|	0.5199|	Down|	-|
9|10-Jun-2021|	Up|	0.5181|	Up|	-|
10|11-Jun-2021|	Up|	0.5188|	Up|	-|
11|14-Jun-2021|Up|0.5207|Down | 2|
12|15-Jun-2021|Up|0.5100|Up|-|
13|16-Jun-2021|Down|0.5154|Up|3|
14|17-Jun-2021|Down|0.5161|Up|4|
15|18-Jun-2021|Up|0.5152|Up|-|
16|21-Jun-2021|Up|0.5052|Up|-|
17|22-Jun-2021|Up|0.5125|Up|-|
18|23-Jun-2021|Down|0.5172|Up|5|
19|24-Jun-2021|Up|0.5067|Up|-|
20|25-Jun-2021|Up|0.5155|Up|-|
21|28-Jun-2021|Down|0.5098|Up|6|
22|29-Jun-2021|Down|0.5232|Down|-|
23|30-Jun-2021|Down|0.5170|Up|7|
24|1-July-2021|Down|0.5205|Down|-|
25|2-July-2021|Up|0.5191|Up|-|
26|5-July-2021|Up|0.5151|Up|-|
27|6-July-2021|Down|0.5104|Up|8|
28|7-July-2021|Up|0.5057|Up|-|
29|8-July-2021|Down|0.5078|Up|9|
30|9-July-2021|Down|0.5080|Up|10|
31|12-July-2021|Down|0.5077|Up|11|
32|13-July-2021||||-|
33|14-July-2021||||-|
34|15-July-2021||||-|
35|16-July-2021||||-|
