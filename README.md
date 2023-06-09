# Predicting SyriaTel's Customer Churn
Using machine learning algorithms to build a model that classifies telecommunication customers based on predicted churn behavior.

![jake-py9Xxoia2tQ-unsplash](https://github.com/keziasetokusumo/p3_project/assets/111642763/3500ff95-373a-42b4-9dda-e8b4daa1518d)

## Contact Information
* Name: Kezia Setokusumo
* E-mail: kezia.setokusumo@stern.nyu.edu
* [Github](https://github.com/keziasetokusumo)
* [LinkedIn](https://linkedin.com/in/keziasetokusumo/)
* Date: May, 2023

## Business Overview and Problem Statement
This project focuses on leveraging data from [SyriaTel](https://www.kaggle.com/datasets/becksddf/churn-in-telecoms-dataset), a telecommunications company, to determine if a given customer will soon churn. Within a business context, churn is defined as the rate at which customers discontinue doing business with a provider over a defined period of time. Churn is a metric that companies within the telecommunications space closely track. 

Using SyriaTel's dataset and machine learning processes, the goal of this project is to identify predictable patterns that companies like SyriaTel can look for to distinguish customers that might churn. Through this, we can recommend attributes that should be addressed early on and improve the likelihood of retention.

The scope of this project includes data inspection, preprocessing, iterative modeling, final modeling, and overall evaluation.

## The Data
The data folder in the repository contains a file titled `SyriaTel_Data.csv`, which is a dataset containing information on the telecom company's customers. Below are the descriptions of each column:

* `state`: user's state
* `account length`: number of days the user's account has been active for
* `area code`: user's area code
* `phone number`: user's phone number
* `international plan`: true if the user has the international plan, otherwise false
* `voice mail plan`: true if the user has the voice mail plan, otherwise false
* `number vmail messages`: number of voicemails the user has sent
* `total day minutes`: call minutes during the day
* `total day calls`: number of calls during the day
* `total day charge`: amount charged to the user for day calls
* `total eve minutes`: call minutes during the evening
* `total eve calls`: number of calls during the evening
* `total eve charge`: amount charged to the user for evening calls
* `total night minutes`: call minutes during the night
* `total night calls`: number of calls during the night
* `total night charge`: amount charged to the user for night calls
* `total intl minutes`: call minutes for international calls
* `total intl calls`: number of international calls
* `total intl charge`: amount charged to the user for international calls
* `customer service calls`: number of customer service calls
* `churn`: true if the user terminated the contract, otherwise false

There are 21 columns in the dataset, and `churn` is treated as the target variable. A `churn` value of 1 means that a customer churns, while a value of 0 means the customer does not churn. The remaining 20 columns provide a glimpse into the customer's profile and usage patterns. At a glance, it appears that some of these columns have a strong relationship between one another. Hence, to avoid multicollinearity, we dropped one of any similar pairs in our data exploration stage.

Below is a preview of the first five columns in SyriaTel's raw datasest:

<img width="980" alt="Screen Shot 2023-05-22 at 7 03 39 AM" src="https://github.com/keziasetokusumo/p3_project/assets/111642763/7203fb0d-fa3a-403a-a875-7e24b933485a">

## Methods
To classify customers into churn or no churn, we analyzed the data with several different algorithms. We built a baseline version of each algorithm:
 * Logistic Regression
 * K-Nearest Neighbors
 * Decision Trees

Afterwards, we performed iterative modeling to identify which hyperparameters work best. To select a final model, we evaluated performance based on:
* accuracy
* precision
* recall (number of true positives out of all positives)
* F1 score (a combination of recall and precision)

Though we test for all four metrics, we give some emphasis to recall, since we want to minimize false negative predictions. In this context, we want to reduce false negative predictions because we'd rather overestimate the number of churning customers versus the number of non-churning customers. Data exploration, cleaning, and preprocessing is also done during the initial stages to ensure that all models can run without error.

## Results
After looping through the three different algorithms several times, we take the best version of each model and display the results in a summary table:

![Screen Shot 2023-05-26 at 2 21 24 PM](https://github.com/keziasetokusumo/p3_project/assets/111642763/3c40428b-d201-4f45-b991-e32e4f454c68)

The summary table indicates that a decision tree is the best algorithm to use. Though it has a slightly lower recall score than that of the logistic regression, the decision tree model is still substantially more accurate and precise than the logistic regression. Using the decision tree, we've created a confusion matrix to visualize the performance of the classification algorithm. The two dimensions are "True label" and "Predicted label":

<img width="333" alt="Screen Shot 2023-05-26 at 1 07 08 PM" src="https://github.com/keziasetokusumo/p3_project/assets/111642763/4fdf10b7-7f07-4bc2-97b7-676a45fac847">

After we've defined our final model to be the decision tree with tuned hyperparameters, we can also plot feature importance to rank which columns have the most impact on classifying churn or no churn.

<img width="724" alt="Screen Shot 2023-05-26 at 1 07 14 PM" src="https://github.com/keziasetokusumo/p3_project/assets/111642763/eff5fba5-41d3-47cb-9d9d-d193bc9ac4a5">

From the graph, we can deduce that `total day charge`, `total eve charge`, and `customer service calls` are the most significant customer behaviors to pay attention to for correctly classifying churn.

## Conclusion
A DecisionTreeClassifier with the following parameters returns predictions with the best evaluation metrics:
`DecisionTreeClassifier(criterion = 'entropy', max_depth = 13, min_samples_leaf = 1, min_samples_split = 2)`

This decision tree model has an accuracy of 0.92, precision of 0.75, recall of 0.70, and F1 of 0.73.

When we use this decision tree model to map out the most influential features for determining customer churn, we find that the most important attributes are:

* `total day charge`
* `total eve charge`
* `customer service calls`

## Recommendation
Overall, we can conclude that customer churn is highly dependent on how much a client is currently paying in phone bills and how often they experience issues requiring customer service. From our data exploration stage, it shows that the 75th percentile for `total day charge`, `total eve charge`, and `customer service calls` are $37, $20, and 2 calls, respectively. Knowing this, SyriaTel can implement some strategies to increase brand loyalty and raise retention rates for customers ranging near these numbers:

* Added value: Once consumers start paying above a certain threshold, SyriaTel should offer discounts on other services such as internet or entertainment.

* Rewards programs: Research has demonstrated that rewards for loyalty enables businesses to charge higher without as much churn.

* Omnichannel support: SyriaTel can ensure its team is well-equipped to handle requests to create a stress-free process and readily-available help.

* Price transparency: Consumers often lose sight of what they're paying for. When bills get too high, they can easily swap out for a cheaper service without knowing what they're losing out on. SyriaTel should provide a clear breakdown of every bill and use terms easily understood by the public.


## Future Analyses
* Compare churn data with that of competitors to see how SyriaTel's business fares in comparison
* Implement customer retention strategies incrementally, and repeat the same analysis to decide which course of action is the most effective
* Dive deeper into price analysis so SyriaTel can estimate the highest price they can charge customers without resulting in churns and pinpoint factors that determine a client's price sensitivity

## Additional Information
Detailed explanations of the churn analysis and corresponding code can be found in this [Jupyter Notebook](https://github.com/keziasetokusumo/p3_project/blob/main/ChurnAnalysis_Notebook.ipynb). A deliverable containing a high-level overview of SyriaTel's business problem and final recommendations for reducing churn can also be found [here](https://github.com/keziasetokusumo/p3_project/blob/main/p3_project_deliverable.pdf).

## Repository Structure
```
├── data
├── images  
├── .gitignore                           
├── ChurnAnalysis_Notebook.ipynb                                      
├── README.md
├── p3_project_deliverable.pdf
└──
```
