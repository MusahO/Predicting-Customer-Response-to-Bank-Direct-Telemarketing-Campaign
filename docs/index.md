# Bank Telemarketing 
## predict Customers responses to future marketing campaigns.

### ABSTRACT
Telemarketing is a method of direct marketing in which a salesperson solicits prospective customers to buy products or services, either over the phone or through a subsequent face to face or Web conferencing appointment scheduled during the call. Telemarketing can also include recorded sales pitches programmed to be played over the phone via automatic dialing.
[Wikipedia](https://en.wikipedia.org/wiki/Telemarketing) it ebnables Babks to focus on customers who are most likely to subscribe to their products. identifying customers is difficult and expensive for Banks. Thats i why i built a model to predict customer response to bank telemarketing campaign by using naive bayes which got ACCURACY of 75%( roc_auc_score) ***Reciever Operating Characteristics Area Under Curve Score***

**results showed:**
  * students and retired people
  * Clients with age less than 30 or 60 and above
  * older People age 60+ with loans
  were the best targets for a positive response to the marketing campaign
**NOTE:** there is room for improvement, a regression model  can be used for Predicting duration of calls which can benefit both the bank and its clients. it will increase the efficiency of the bank’s telemarketing campaign, saving time, expenses and prevents some clients from receiving useless calls. 

## DATA

The data is related with direct marketing campaigns of a Portuguese banking institution. The marketing campaigns were based on phone calls. Often, more than one contact to the same client was required, in order to access if the product (bank term deposit) would be ('yes') or not ('no') subscribed. source: [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/datasets/Bank+Marketing#)
**There are four datasets, i chose the one below more information about the dataset can be got in the above**
 1. bank-additional-full.csv with all examples (41188) and 20 inputs, ordered by date (from May 2008 to November 2010), very close to       the data analyzed in [Moro et al., 2014]
 
 ## EXPLORATORY DATA ANALYSIS (understanding the dataset) && DATA VISUALIZATION
 
 ### VISUALIZING OF CATEGORICAL FEATURES
 
 <!---![image 1](/images/1.png)--->
 <img src="https://github.com/MusahO/Predicting-Customer-Response-to-Bank-Direct-Telemarketing-Campaign/blob/master/images/1.png?raw=true"/>
 
**The dataset is clearly unbalanced as we can see mot of the catgeorical features there is a very low number of subscribers compared to    the those that didn't**
**in the job categorical feature, it seems the subcribe/nonsubcribe ratio for students and retired is worth the study(doesn't look that    imbalanced)**

 ### VISUALIZING OF NUMERICAL FEATURES
 
 <img src="/images/2.png"/>
 
**Age**: the bank has called people of from the age of 18 to about 100 but those contacted most are middle aged in there 30's
**Duration**: the duration of calls is skewed. there are calls longer than 15 minutes, i will have to remove them, because they will       affect our models prediction

 <img src="/images/3.png"/>
 
 ### Relationship between Duration of calls and Number of calls with client response
 
 <img src="/images/4.png"/>
 
**the plot shows that clients that contacted for a shorter duration and a few times have a higher rate of subscription. so the bank      should not persiste on calling clients for a long time and repeatedly**
 
 ### Subscription rate vs Contact Rate against Age groups
 
 <img src="/images/5.png"/>
 
 **The Bank should priotize the eldery(+60) and those below 30. it seems the elderly are subcribing more because of retirement
 the campaign team pritoized the middle aged which had poor returns**

### Loans(yes,no) vs response rate

<img src="/images/6.png"/>

**older people tend to subscribe more, the bank priotize them because the have a higher response rate(subscription)**

### subscription rate per JOB

<img src="/images/7.png"/>

**Students and Retired People yet have the most subscriptions rates**

### HEATMAP AND CLUSTERMAP TO VISUALIZE CORRELATION AMONG FEATURES AND RESPONSE AND MULTICOLLINEARITY

<img src="/images/8.png"/>

<img src="/images/9.png"/>

**emp.var.rate(employment variation rate) is highly collinear with nr.employed(number of employees) and euribor3m(euribor 3 month rate)/euro interest rate. illl use variance inflation factor to remove one of th features**
**cons.price.idx(consumer confidence index) is collinear with euribor3m, emp.var.rate and nr.employed which i further studied using variance_inflation_factor check out notebook**

## MACHINE LEARNING MODELS: (CLASSIFICATION )

classification algorithms will be used to achieve the objective set above. A classification model will be built to classify all customers; "yes" for subcribing to term deposits and "no" to for not subscribing to term deposits.

### DATA PREPARATION
Transformation of categorical data is must because the am going to use numerical data:
**'job', 'marital', 'education', 'default', 'housing', 'poutcome', 'loan'** arent ordinal so they are transformed into dummy variables using pandas get_dummies() function.

feature inputs for models was done using 70/30 split for training and testing

### BUILDING CLASSIFICATION MODELS

LogisticRegression, GaussianNB, KNeighborsClassifier XGBoost, lightgbm algorithms were used and the best performing was chosen for the final model.

<img src="/images/10.png"/>

**The LightGM Model outperforms all models but at the expense of having a high variance with a roc_auc_score of 75% with std of 0.014, while the GaussianNB model had a roc_auc_score of 73% with std of 0.00999. ill use The Naives Bayes Model(GuassianNB) because of it interpretability(its clear for each feature how much it affects the prediction)**

### RESULTS

<img src="/images/11.png"/>

A naive bayes model was successfully built for the classifcation problem. The bank will be able to predict a client's response to its telemarketing campaign before contacting him/her. The bank should priotize clients who are highly likely to accept term deposits, and call less to those who are unlikely to make term deposits.

## CONCULSION
USEFUL features
students and retired people
Clients with age less than 30 or 60 and above
older People age 60+ with loans

NOTE: Predicting duration of calls can benefit both the bank and its clients. it will increase the efficiency of the bank’s telemarketing campaign, saving time, expenses and prevents some clients from receiving useless calls. This can be done using REGRESSION MODELS WHICH WEREN'T IMPLEMENTED IN THIS NOTEBOOK
