# Arvato Financial Solutions Customer Segmentation

## Purpose:

Knowing your customers is a very important part of running any business. One way companies accomplish this is through customer segmentation. Segmentation involves using data about customers to group them by similar characteristics, and ideally use those characteristics to make profitable business decisions.

This project involves performing a segmentation analysis for Arvato Financial Solutions customers. The goal of the analysis is to determine differences between Arvato customers and the general population, and which segments of the population are more likely to become customers. This information is useful for Arvato to better identify and target potential customers in their marketing efforts. The data used is demographic information for Germany's general population, and Arvato customer information in a separate dataset.

A second part to the analysis is to design a machine learning model to predict customer responses to a mailout marketing campaign. Separate but similar datasets are used for this portion to develop the model. A testing dataset without response information is used to predict customer responses and was uploaded to the associated [Kaggle competition](https://www.kaggle.com/c/udacity-arvato-identify-customers/overview). Arvato can use this model to take their targeting a step further and determine which customers are most likely to respond to a mailing campaign, allowing them to make the campaign more effective and reduce wasted effort on customers unlikely to respond.

## Files:

* 'Arvato Project Workbook.ipynb' - Notebook with analysis code and results.
* 'DIAS Attributes - Values 2017.xlsx' - Information on demographic data attribute possible values.
* 'DIAS Information Levels - Attributes 2017.xlsx' - Information on attribute descriptions and meanings.
* 'Udacity_AZDIAS_052018.csv' - Dataset of demographic data from general population. Not published due to file size.
* 'Udacity_CUSTOMERS_052018.csv' - Dataset of demographic data from current customers. Not published due to file size.
* 'mailout_train.csv' - Dataset of customer information & response to mail campaign to be used to train model.
* 'mailout_test.csv' - Dataset of customer information without response to mail campaign. Model runs of this dataset to produce predictions submitted to the associated Kaggle competition.

## Python Libraries:

This analysis makes use of the following python libraries:

* `matplotlib`
* `numpy`
* `pandas`
* `seaborn`
* `sklearn`

## Analysis Summary:

### Customer Segmentation:

The analysis applied PCA and K-means clustering to determine the groups within the general population. The clustering model was applied to the customer data and revealed four primary clusters of interest:

* Cluster 0:
Low mobility patterns and more likely to have 1-2 family homes in their area. Also less likely to have luxury cars in their area. Customers are less likely to be from this group.

* Cluster 1:
More likely to have money saver / investor financial habits. Also are more likely to be affected by older social movements. This could also imply this group is higher in age range. This group overall is less likely to be customers.

* Cluster 2:
High popularity of luxury cars in their area. Low on online affinity. These respondents are more likely to be customers than the general population.

* Cluster 7:
Low online affinity and recency of online activity. Are not likely to interact online much with businesses. They are also low on frequency of movement and high share of 1-2 family homes in their area. Are less likely to move from their current residence and likely own their own home vs. residing in a shared building like an apartment complex or condominium. People in this cluster are more likely to be customers.

Overall, it appears that customers are more likely to be individuals from the general population who meet the following critera:
- More likely to spend vs. save or invest money
- Likely in upper middle class, may enjoy showing their financial status with luxury vehicles
- Live in / own their own home vs. a shared home and do not move residences often
- Are not often online or do not rely on online interactions
- May possibly be older or influenced by older social movements

This information is valuable to Arvato and will help the business determine where to focus their advertising efforts to recruit new customers. Using segmentation, Arvato can apply this analysis to individual respondents to predict which cluster they would fall in. From there, those individuals can be further targeted (or ignored) with high confidence of successful acquisition (or reduction of lost time / resources chasing unlikely customers).

### Supervised Learning Model:

The supervised learning model was developed using several pipelines for the `LogisticRegression`, `RandomForestClassifier`, and `DecisionTreeClassifier` estimators. Some of the pipelines tested implemented PCA while others did not.

Model performance was measured using the ROC score and curve. After testing the pipelines, the `LogisticRegression` model without PCA achieved the highest ROC score at 0.669.

The model was further optimized using `GridSearchCV`, changing the  penalty, class_weight, and max_iter parameters. This optimization resulted in an ROC score of 0.675, a slight improvement over the original model. The best parameters for the optimization were:

- class_weight: None
- max_iter: 200
- penalty: l1
- solver: liblinear

This model can be deployed on Arvato's customer data to determine which customers are most likely to respond to a mailing campaign. Narrowing down the target customers allows the company to use it's time and resources effectively, ensuring effort is not wasted on customers who are not likely to resopnd, and customers who are likely to respond are not inadvertently ignored through broad targeting methods.

## Blog Post

Check out the associated blog post for this analyis here:

[Arvato Financial Customer Segmentation on Medium](https://neuralfiber0307.medium.com/arvato-financial-customer-segmentation-fca16df315c3).
