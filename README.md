# DS-Unit-2-Buildweek-Project
This is a repository for a project to use the predictive modeling.
The CSV file of the dataset is available at'https://www.kaggle.com/floser/french-motor-claims-datasets-fremtpl2freq?select=freMTPL2freq.csv'

Predicting the Insurance Claims

Insurance business has always been about data analysis. Insurers collect and analyze huge amount of data to predict the future events, calculate risks and price their products accordingly.  

Predicting the upcoming claims is an important part of these efforts. In this project, I use predictive models to anticipate the filing of a claim on a policy. 

Dataset

I use a dataset comprising a French automobile third-party liability insurance portfolio. The dataset includes 678,013 policies and 12 features for each policy.  	

Our target variable is ‘Number of Claims’. It has 11 classes while majority class is ‘no claims’ with 95% frequency.  

 

Majority of the policyholders do not file a claim. The problem with imbalanced classes is that our models would probably overfit. The algorithms would not learn the patterns to predict the future claims for the new data which is our aim for modelling. 
  
Imbalanced classes are common for datasets related with fraud, medical screening, factory production defect rates, etc. So there are several ways to handle the imbalanced data. One of them is rebalancing the dataset by sampling. I use oversampling and undersampling strategies for my dataset. 


Feature Engineering

The distribution of the classes for my target feature, Number of Claims, has 11 classes. The number of claims which are more than one comprises less than 0.3% of total observations so I transform it to a two-class feature for binary classification, ‘Claim’, ‘No Claim’. 

Majority Class 
0      94.98%
1       5.02% 

I also drop the ‘Policy ID’ column since it has no predictive power. 

Modeling

I run Logistic Regression and Random Forest Classifier models with the original dataset in order to check if we can get reasonable results without using any sampling techniques. 

The validation accuracy scores: 
Random Forest Classifier: 94.85%
Logistic Regression: 94.98%

The accuracy scores are high but the literature over the imbalanced classes states that the accuracy is a misleading metric for this kind of datasets. Accuracy can still be high while the model would be doing an awful job at predicting the minority class. 


  


Confusion matrices also tells us that models make predictions mainly for majority class (0), omitting the minority class.   

I will apply resampling techniques to create balanced classes. 

Resampling

 


Oversampling is the process of duplicating random observations from minority class to create a balanced dataset. It is prone to overfitting. 

Undersampling is the process of randomly removing observations from majority class to match the number of observations of the minority class. The drawback of this process is the loss of information. 

I apply these two strategies to the dataset and run the models again. 

 

As we can see from the table, the model with the best scores is the Random Forest Classifier with the oversampled dataset. On the other hand, the accuracy score is close to 1 which signals that the model most probably overfits. Therefore, I decide to use the second-best model Random Forest Classifier with undersampled dataset. Even though Its test accuracy is 64% and less than desired, it is still better than the majority baseline of 50%. I tried some feature engineering, but I was unable to increase the effectiveness. 


 










Random Forest Classifier 

The Permutation Importance: 

 

In our model, the most important feature is the period of exposure per policy  which is the duration of being subject to a claim. It makes sense since as the period of exposure increases the policyholder is more likely to have an incident to file a claim. Its weight shows us how much accuracy changes with randomly shuffling its values. Second most important feature is Vehicle age.


Partial Dependence Plots

Partial plots tell us how a feature affects the predictions. Y axis shows the change in the prediction as the independent variable changes. 






 


Our model shows that from the age of 18 the probability of claims decreases as the drivers’ age reach to 35. From 35 to 42, the probability of claims increases rather steeply until the drivers reaches to 43. From there on, the probability of claims increases very slightly with each passing year. 


 

In this graph we see the relationship between claim and the period of exposure for the policy.  After a little while from the beginning of the policy, the chance of a claim filed increases as time passes. The interesting part is that after three-fourths of the year passes, the chances for a claim do not increase for the rest of the policy period. 

Conclusion
The model with the rebalanced dataset did not give me a high accuracy score. I would also expect more permutation importance for ‘Driver’s age’ and population ‘Density’ features. Instead, this model told that the length of time of being subject to a claim (‘Exposure’) and ‘Vehicle Age’ are the most important features. 


 
