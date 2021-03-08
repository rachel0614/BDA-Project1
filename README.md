# BDA Project
This is my BDA project. The purpose of this project is to analyze the dataset provided by Consumer Financial Protection Bureau (CFPB) by applying big data related techniques.
## Code files
The analysis is implemented by Jupyter Notebook, see file **CustomerComplaint.ipynb**.

## Abstract
This is a customer complaint dataset about financial product consumption in the USA. We would like to hear the voice of these customers by analyzing it. How many valid complaints in this dataset? What is the most concerning problem? What is the strongest voice of these complaints? Have those financial companies improved their service from this? Can we predict the trends of the complaints?
With these questions, we are going to have an exploration to this dataset. Take a breath, hear the voices of the customers. Let the millions of complaints records tell us what happened because charts never lie.

## Introduction
In this project, we are going to analysis the consumers complaints about financial products in the USA. The dataset of this project obtained from the data.gov website which is collected by the Consumer Financial Protection Bureau, an agency of the United States government responsible for consumer protection in the financial sector \cite{datasource}. It includes complaints dating from 2015 by now. 

The volume of this dataset is roughly 2 million items. We apply big data analytic related techniques, such as Spark, machine learning, natural language process (NLP) and so force, to achieve the goal of the project:

1. providing descriptive analysis combined with visualization, such as bar charts and word cloud charts, to give an insight and summarization of these data.
2. providing prediction model by machine learning approaches.

We prepared questions below before expoloration of this dataset
- What's the most complained from different dimensions, such as complained channels,companies, products. Have they changed over time?

- Pictures speak louder than text, what can we get from the narrative of those complaints.
- Can we predict the issue type? Can we predict the process result to guide the urgency of these complaints, so that the companies can give a  higher priority when dealing with the urgent complaints.
- The quality of service - responding time, where, what and which providers got the most complaints. Any improvement later? 

## Method
### Data preparation
#### Filtering
After checking date range of this dataset, we keep the sent date between 2012 and 2020 (full-year)
#### Check null/emptyvalue
- replace empty **sub_issue** with issue value, replace empty **sub_product** with product value
- remove empty **states** and outliers name; remove empty rows from **consumer_consent_provided** column
- remove **zip_code**. Due to page limit, we don't focus on geographical analysis in this report. There're hundreds of thousand empty cells in this column, drop instead of fix it. 
- remove **complaint_id** which contributes nothing to analysis and prediction.
- remove **tags** for less reference value and most values of this column are empty.
- remove **company_public_response**

#### Feature engineering
##### New features
- Add the length of the complaint content as a new feature named **complaint_len** 
- Add **weekday_received** to show weekday number of the **date_received** column
- Merge **Credit card or prepaid card	** and **Credit card or prepaid card ** of the product column	to **Card** 
- Merge the product of **Credit reporting, credit repair services, or other personal consumer reports** and **Credit reporting** 

##### Company response
We choose **company response** as prediction goal because whether the company closed with relief or not is an interesting question, and it's meaningful business analysis. But the **company_response** consists several different unique values. Let's simplify the value to closed with relief or not.
clear the unclosed complaints.

##### One hot encoding
- After processing the null/empty values of each column in the previous steps, we transform these categorical values numeric by one hot encoding, so that the machine learning model can deal with it easily.

### Data modeling
 - The Random forest and Decision tree has been used for machine learning, Cross-validation, Grid Search for hyperparameter tunning.
 - Stacked Bar chart is used for proportion analysi based on different dimensions such as product, issue, and so forth.
 - Words Cloud chart is used for showing the high frequency words extracted from the sentences of the narrative column.


## Conclusion
From the above analysis, we have heard the voices from the customers in consuming financial products. From this process of manipulating this dataset, we have known the pipeline of dealing with big data. By applying big data analytics techniques, we can have deep and clear insight about out dataset.
The time expense of data preparation is high, and it's the essential part of the whole pipeline.

## Future work
We can do further analysis as below:
- geographical features based analysis.
 - Date columns related analysis.
 - Make full use of the narrative content of the complaints,such as sentiment analysis, words cloud based on sentiment, and involve it as the feature in training our models. 

