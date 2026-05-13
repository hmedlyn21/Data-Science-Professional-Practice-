# Data-Science-Professional-Practice-
Predicting Car Prices





# Data Preprocessing
The data was extracted from Kaggle: 'https://www.kaggle.com/code/abdelhamedahmed2005/car-price-prediction' in CSV format, which allowed it to be easily reviewed in Excel for identifying cleaning opportunities and efficiently imported into Python using Pandas.

## Initial Exploration 
In Python, variables were examined for missing values and data type to assess dataset structure and suitability for regression. No missing values were identified, so no imputation or row removal was required, reducing bias risk.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/df.info%201.png?raw=true)

## Cleansing
Each column was evaluated for its relevance to the model, and on this basis the index column was removed.

Excel filters were used to review value ranges. This identified inconsistent formats in the ‘car_prices_in_rupee’ column. Prices were standardised into rupees using the Indian numbering system, where 1 lakh equals 100,000 and 1 crore equals 10,000,000 (Government of India, 2023), before text was removed and the column converted to integer format. 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/Conversion%202.png?raw=true)

Object columns were converted to numeric format, as regression models require numerical inputs (James et al., 2021). 

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/column%20conversion%203.png?raw=true)

Columns were then reassessed for null values to ensure transformations were correct and data integrity was maintained.

![image alt](https://github.com/hmedlyn21/Data-Science-Professional-Practice-/blob/main/null%20value%20check%204.png?raw=true)
