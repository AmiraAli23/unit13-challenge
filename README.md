# Unit 13 - AWS 

## Clustering Crypto


![image](https://user-images.githubusercontent.com/99091066/170851830-10101ed7-4274-4c4e-b589-d48b4a6b930e.jpeg)


The objective of this assignement was to analyze the various cryptocurrencies available on the trading market, and grouping them using classification.

## Data Preprocessing

Using the `crypto_data.csv` [file](https://github.com/AmiraAli23/unit13-challenge/blob/ce29d12e8230266cf0a4d56dc56d559a5c3c9f19/crypto_data.csv), I imported the data and renamed the df `crypto_df` . 

To determine which cryptocurrencies are currently trading, I used the following code: 

```python 


dfnew=df[df['IsTrading']==True]

````

This removes any `False` values from the table. 


To keep all the currencies with a working algorithm, I used the `isnull.sum()` feature. There were 0 null values meaning all currencies had a working algorithm.

```python 

pd.isnull(dfnew['Algorithm']).sum()

````

To remove all null values , I used the same `isnull.sum()` feature and applied it to the entire dataframe to determine which column had null values. Since `TotalCoinsMined` was the only column with null values , I used the following code:

<img width="250" alt="Screen Shot 2022-05-29 at 12 21 10 AM" src="https://user-images.githubusercontent.com/99091066/170852089-5db29a48-fb6c-4462-bd6b-527daa7ae3ed.png">


````python 

dfupdates1=dfupdates.dropna()

````

Next, I removed any cryptocurrencies that had no coins mined. The values in the `TotalCoinsMined` column were either negative , 0 , or positive. Since negative coins is not a real value, I sorted the data to show all values > 0. 

 ````python 

dfupdates2=dfupdates1[dfupdates1['TotalCoinsMined']>0]

````

Before standardizing the data, I converted all "text" value columns into dummy variables, specifically columns `Algorithm` and `ProofType` as the rest were numbers.

````python 

X=pd.get_dummies(dfupdates3, columns=['Algorithm','ProofType'])


````

<img width="793" alt="Screen Shot 2022-05-29 at 12 26 42 AM" src="https://user-images.githubusercontent.com/99091066/170852222-38e38334-06d1-4bda-8505-444702b2f55b.png">


I then standardized the data using `StandardScaler` from `sk.learn.preprocessing` to produce the following array


<img width="636" alt="Screen Shot 2022-05-29 at 12 29 04 AM" src="https://user-images.githubusercontent.com/99091066/170852277-40679da3-fd4a-4b43-9cdd-e0ac321f1d99.png">


## Reducing Dimensions Using PCA

I used PCA to reduce the dimensions into three principle components.

````python

pca = PCA(n_components=3)
pcafit=pca.fit_transform(scaleX)
pcadf=pd.DataFrame(data=pcafit, columns=['Pc1','Pc 2','Pc3'])
pcadf
````


<img width="289" alt="Screen Shot 2022-06-04 at 2 42 27 PM" src="https://user-images.githubusercontent.com/99091066/172021309-8e01ca54-3eed-4a50-a7d2-f8c8d3f07653.png">

## Clustering Crytocurrencies Using K-Means

### Find the Best Value for k Using the Elbow Curve


<img width="576" alt="Screen Shot 2022-06-04 at 2 44 25 PM" src="https://user-images.githubusercontent.com/99091066/172021377-fd205667-f8c2-48da-8152-68d5f76208e0.png">

## Scatter Plot with Tradable Cryptocurrencies


<img width="698" alt="Screen Shot 2022-06-04 at 2 45 45 PM" src="https://user-images.githubusercontent.com/99091066/172021417-925f8c2d-738e-45f0-81cc-070a7d48f4f1.png">


## Table of Tradable Cryptocurrencies

<img width="689" alt="Screen Shot 2022-06-04 at 2 46 53 PM" src="https://user-images.githubusercontent.com/99091066/172021458-214b015b-5ec1-4199-b2f9-958ecb137de0.png">




