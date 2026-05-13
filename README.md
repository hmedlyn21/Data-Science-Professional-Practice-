# Predicting Car Prices
Data Science Project





# Data Preprocessing
The data was extracted from Kaggle: 'https://www.kaggle.com/code/abdelhamedahmed2005/car-price-prediction' in CSV format, which allowed it to be easily reviewed in Excel for identifying cleaning opportunities and efficiently imported into Python using Pandas.

## Initial Exploration 
In Python, variables were examined for missing values and data types to assess dataset structure and suitability for regression. No missing values were identified, so no imputation or row removal was required, reducing bias risk.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/df.info%201.png?raw=true)

## Cleansing

Firstly, Excel filters were used to review value ranges. This identified inconsistent formats in the ‘car_prices_in_rupee’ column. Prices were standardised into rupees using the Indian numbering system, where 1 lakh equals 100,000 and 1 crore equals 10,000,000 (Government of India, 2023), before text was removed and the column converted to integer format. 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/Conversion%202.png?raw=true)

Object columns were converted to numeric format, as regression models require numerical inputs (James et al., 2021). 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/column%20conversion%203.png?raw=true)

Columns were then reassessed for null values to ensure transformations were correct and data integrity was maintained.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/null%20value%20check%204.png?raw=true)

## Anomaly Detection

To reduce the risk of poor model performance, anomalies are evaluated due to their ability to distort relationships between variables, causing inaccuracy. 

A box plot was used to show the distribution of log10-transformed car prices - making large values easier to interpret - necessasary due to the range of car prices. 

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

# Relationship Analysis

The relationships between numeric variables in the training dataset were examined first. Numerical columns were selected and a correlation matrix calculated to measure the strength of linear relationships between variables. A hypothesis was formed that kms driven would affect car price the most.

A heatmap is then created to visualise these correlations more clearly, with values close to 1 or -1 indicating strong relationships. The heatmap has been halved because a correlation matrix is symmetric, showing only one half removes duplicate information and makes the visual easier to read for less technical users.


![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/Heat%20map.png?raw=true)

This also identifies and prints pairs of variables with correlation values above 0.80, as these may indicate multicollinearity. This step is important before building a regression model, because highly correlated predictors can reduce the reliability and interpretability of the model. Overall, the results show a strong relationship between kms driven and manufacture year, while engine and seats show limited linear assocation. 

# Model Fitting & Performance

## Model Selection

A standard linear regression model was initially applied, but its R² score of 0.37 showed limited explanatory power. This suggests car prices were not well represented by a simple linear relationship. As pricing is influenced by interacting factors such as mileage, age, engine size, etc, Random Forest was more suitable because it can model non-linear relationships without the assumptions required by linear regression. It is also more robust to outliers and variation, making it a better choice for improving predictive performance (James et al., 2021).

## Performance

The Random Forest model performed moderately well on the test data, achieving an MAE of ₹532,779, RMSE of ₹1,194,290, and R² of 0.63. The MAE shows that predicted prices were around ₹5.3 lakh from the actual value. The higher RMSE suggests that some predictions had larger errors, as this metric gives more weight to bigger mistakes. The R² value indicates that the model explained 62.7% of the variation in car prices. Overall, these results suggest the model captured some of the pricing pattern, although some variation remained unexplained.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/Error%20metrics.png?raw=true)

The visual below helps understand the error metrics by showing them graphically. Points close to the red line indicate more accurate predictions, while points further away show larger errors. This makes the error metrics easier to interpret, as the overall accuracy and where the model over or under predicts car prices can be seen.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/prediction%20plot.png?raw=true)

## Hypothesis Results

Finally, to evaluate the hypothesis a table assessing feature importance scores is built, ranking from most important to least important, helping identify which features had the greatest influence on the model’s predictions, with kms driven having the greatest impact.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/feature%20importance.png?raw=true)

# References

Microsoft. (2024). *Microsoft Excel Documentation*. Available at: Microsoft Excel Documentation 

Great Britain. *UK General Data Protection Regulation*. Available at: https://www.legislation.gov.uk/eur/2016/679/contents (Accessed: 11 May 2026). 

McKinney, W. (2022). 8Python for Data Analysis*. O’Reilly Media. 

Government of India (2023) *Office Procedure Manual*. New Delhi: Department of Administrative Reforms and Public Grievances

James, G., Witten, D., Hastie, T. and Tibshirani, R., 2021. *An introduction to statistical learning: with applications in R*. 2nd ed. New York: Springer. 

Jaguar Land Rover Automotive plc (2024) *Annual report 2024*. Available at: https://www.jlr.com/annual-report-2024 (Accessed: 13 May 2026). 

Kuhn, M. and Johnson, K. (2019) *Feature engineering and selection: A practical approach for predictive models*. Boca Raton: CRC Press. 

Micci-Barreca, D. (2001). *A preprocessing scheme for high-cardinality categorical attributes in classification and prediction problems*. ACM SIGKDD Explorations Newsletter, 3(1), 27–32. 

