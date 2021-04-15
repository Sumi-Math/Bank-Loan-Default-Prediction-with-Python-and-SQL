# Bank-Loan-Default-Prediction

Predicting whether or not a client will repay a loan or have difficulty is a critical business need. This sample database includes 4 different sources of data:

* **application_train/application_test:** the main training and testing data with information about each loan application at Home Credit. Every loan has its own row and is identified by the feature SK_ID_CURR. The training application data comes with the TARGET indicating 0: the loan was repaid or 1: the loan was not repaid.

* **bureau:** data concerning client's previous credits from other financial institutions. Each previous credit has its own row in bureau, but one loan in the application data can have multiple previous credits.

* **bureau_balance:** monthly data about the previous credits in bureau. Each row is one month of a previous credit, and a single previous credit can have multiple rows, one for each month of the credit length.

* **previous_application:** previous applications for loans at Home Credit of clients who have loans in the application data. Each current loan in the application data can have multiple previous loans. Each previous application has one row and is identified by the feature SK_ID_PREV.

### Processed data by using SQL

To prepare the data for analysis, at first we pulled the essential data in the required format by writing SQL queries. We explored in tables, understand the distribution of the data in each table. Then we process the data as required for the analysis. In some cases, we had multiple rows of data for the same loan ID. In that case, we aggregated and flatten the data accordingly. Finally we joined the table by using SQL LEFT Joins. For the big size of the data we splited it into three portions. At first we joined the application table with the processed bureau table which is named as 'Base'. Then we joined the 'bureau_balance table with the 'Base' table named as 'Base 2'. Finally we joined the 'previous_application' table with the 'Base 2' table and named as  'Base 3'. 

### Data Analysis in Python

After extracting data from the database we fit the data in pandas dataframe. We did an EDA of the data, cleaned the data by handling missing values and duplications.For simplicity we extracted each joined table as a csv file and later merged them based on the common column. In the final table there are all together 307511 rows. On anaother  note there are many categorical variables in this final table. We used 'one hot encoding' technique to handle those categorical variables. Finally we fit tha dataset to both of the logistics regression and random forest classifier model to predict the loan default. Random Forest Classifier showed a better accuracy than Logistic Regression model with better AUROC (Area Under the Receiver Operating Characteristics) score. 

!![AUROC](https://user-images.githubusercontent.com/76721123/114818433-cc623280-9d89-11eb-8377-6a6858258697.JPG)
[Uploading AUROC.JPG…]()
