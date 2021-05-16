# Crypto Currency Analysis
## I)Introduction
---
This is a project which I'm really excited about because I myself is a crypto currency investor, and in order to know more infomation about the relationship between those crypto currencies, making an analysis is necessary. There are three main part in this project, the first one is data pre-processing which takes care of things like missing data. The second part is about data visualization. The last part is about using different models to do predictions on our model



## II)Getting Started
---
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.


- Prerequisites
    You will need a tool to run the program on your local machine such as:
    > VScode, Jupyter Note Book......

 
- Installing
    There are some packages that you will be using:
    > Pandas, Numpy, Matplotlib.pyplot, Seaborn, Scikit-learn(sklearn), bokeh, keras, pmdarima
    - Install packages on Jupyter NoteBook:
      > !pip install 'package name'


- Run the program
    The only thing you will need to do to run the test is input a CSV file with header 
    >[number, Name_of_currency, Symbo_of_currency, Date, High, Low, Open, Close, Volumn, Marketcap]


## III) Methodology
---
- Raw Data:
  
  I used the historical stock prices of some of the famous crypto currency from Kaggle. The size of these CSV file are different but most of them are over 10000 rows. Each row of record contains information like date, high, low, open, close, volume, marketcapsdf


- Data pre-processing

  From my observation, there is an interesting fact that from the beginning of the dataset till a certain time, the volume will be 0; then after that certain time, the number of volume is greater than 0. The 0 volume means there is no trading yet on this crypto currency; other wise it has. 

  Instead of keep the records of volume = 0 and volume != 0 together, I separated them into two CSV files.

- Data visualization
  
  Instead of using normal analysis packages suck as matplotlib, I used bokeh pacakge here. Since bokeh package allows users to interact with the analysis graph, it provides more accuract information for the investors.  

- Training Process:

  In this project, I used two mose popular deep learning architectures, one is auto-ARIMA and the other is LSTM. 
  Since the data we got are historical, I also have two different strategies to train them. One is by the order of date, and the other is to shuffle the data in the beginning. 



- Testing

  Each model has been tested on the test set. Besides, we have some other measurement such as RMSE(Root mean square error), MAE(Mean absolute error), MAPE(Mean absolute percentage error), MDAPE(Median absolute percentage error)


### model 1: Univariate auto_ARIMA:
  - stationary check
  - train, test split
  - prediction
  - forcasting

### model 2: Univariate, sorted LSTM
   - TimeSteps: 60
   - Neurons in first layer: 300
   - Dense layer: 64, 1
   - Batch Size: 100
   - Trainable parameters: 381729


### model 3: Univariate, shuffled LSTM
   - TimeSteps: 60
   - Neurons in first layer: 300
   - Dense layer: 64, 1
   - Batch Size: 100
   - Trainable parameters:381729


### model 4: multivariate, sorted LSTM
   - TimeSteps: 60
   - Neurons in first layer: 300
   - Dense layer: 64, 1
   - Batch Size: 100
   - Trainable parameters: 410657


### model 5: multivariate, shuffled LSTM
    - TimeSteps: 60
    - Neurons in first layer: 300
    - Dense layer: 64, 1
    - Batch Size: 100
    - Trainable parameters: 410657



## IV) Final observation
---
auto_ARIMA:
- Before using this model, one of the essential steps is to check if the series we are going to input is non-stationary. Since the the letter 'I' in ARIMA stands for differencing, and would be better to use this technic on non-stationary series. This model takes a single feature to predict the close price. 


LSTM: 
- For this architecture, we can separate it into two cases
  -  Large amount of data: under this circumstance, we can obtain high accuracy while only using epochs between 1 to 15. However, if we use higher epochs such as 100, then our error rate increases sharply.
  -  Small amount of data: under this circumstance, if we use small epochs like the above situation, then our error rate will be over 50% or evern higher. As a result, the best way to minimize the error rate is by using large epochs such as 200.

- If the dataset is large(over 2000), we can use the early stopping technic to find the best epoch so that it can return a relativly accurate prediction. However, for dataset which is small(less than 1000), early stopping technic may not work, so  we will define an appropriate epoch for it manuly. 

- Moreover, the model(function) I defined also allow users to adjust epoch, batch size, learning rate by themselves. Users can also choose to use early stopping or not while using the function. 

