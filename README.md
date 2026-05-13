# Predicting Car Prices
Data Science Project





# Data Preprocessing
The data was extracted from Kaggle: 'https://www.kaggle.com/code/abdelhamedahmed2005/car-price-prediction' in CSV format, which allowed it to be easily reviewed in Excel for identifying cleaning opportunities and efficiently imported into Python using Pandas.

## Initial Exploration 
In Python, variables were examined for missing values and data type to assess dataset structure and suitability for regression. No missing values were identified, so no imputation or row removal was required, reducing bias risk.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/df.info%201.png?raw=true)

## Cleansing

Firstly, Excel filters were used to review value ranges. This identified inconsistent formats in the ‘car_prices_in_rupee’ column. Prices were standardised into rupees using the Indian numbering system, where 1 lakh equals 100,000 and 1 crore equals 10,000,000 (Government of India, 2023), before text was removed and the column converted to integer format. 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/Conversion%202.png?raw=true)

Object columns were converted to numeric format, as regression models require numerical inputs (James et al., 2021). 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/column%20conversion%203.png?raw=true)

Columns were then reassessed for null values to ensure transformations were correct and data integrity was maintained.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/null%20value%20check%204.png?raw=true)

## Anomaly Detection

To reduce the risk of an inaccurate model prediction, anomalies are evaluated due to their ability to distort relationships between variables, causing inaccuracy. 

A box plot was used to show the distribution of log10-transformed car prices, making large values easier to interpret. 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/box%20plot%205.png?raw=true)

The box plot shows the typical range of car prices, with unusually low and high values highlighted in red to draw attention to potential outliers. Clear titles and simplified descriptions were also added to improve accessibility and support understanding for less technical users.
The results show more outliers at the higher end of the price range. However, as this is car price data, luxury and lower-end models with naturally different prices are expected, which may explain these outliers.

To assess this further, the interquartile range (IQR) method was applied to log-transformed prices to identify unusual car listings. Prices below the lower threshold or above the upper threshold were flagged as anomalies, and a list of affected car models was produced to assess whether the price ranges were plausible for each model.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/Scatter%20plot6.png?raw=true)

The scatter plot was used to present the anomaly results, making it easier to see how values were distributed. Red was used consistently to highlight anomalies, helping readers associate this colour with unusual values, while blue represented regular listings so anomalies stood out more. Dashed horizontal lines showed the lower and upper anomaly thresholds, improving interpretation. Simplified titles and axis labels were also used to support understanding.

The analysis showed that the same car names appeared repeatedly among flagged anomalies, including brands associated with luxury vehicles, such as Range Rover (Jaguar Land Rover Automotive plc, 2024). This suggests these values are not true anomalies, but reflect genuine market prices. 

After assessing anomalies, the ‘car_name’ and index column were dropped due to no longer being required.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/column%20drop.png?raw=true)

## Train/Test Split

The dataset is then split into 70% training data and 30% test data so the model can be trained and evaluated on unseen data. The random_state makes the split reproducible.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/Train%20test%20split%207.png?raw=true)

## One-Hot Encoding

Three categorical variables were converted into numerical format using one-hot encoding to make them suitable for regression. This was done after the train-test split to prevent data leakage and ensure the model was built only from training data (Kuhn and Johnson, 2019). 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/one-hot%20encoding%208.png?raw=true)

Further checks for missing values confirmed that transformations had been completed successfully, as any values that could not be converted were recorded as null and could therefore be identified.
