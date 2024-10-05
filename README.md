# Practical-Application-3
A hands-on project to comparing the performance of the following classifiers: k-nearest neighbors, logistic regression, decision trees, and support vector machines. This is the third Practical Application project for the UC Berkeley AI/ML Professional Certificate.

Detailed Analysis can be found in the Jupyter notebook

## Data
The data is sourced from  UCI Machine Learning repository, and linked in the "Data" folder of this project

The classification goal is to predict if the client will subscribe a term deposit (variable y). 

## Processing
The Target variable was mapped such that "Yes" = 1, and "No = 0"

One-hot encoding was conducted on all categorical features

Standard scalar was applied to all numeric features. 

I used a test/train split for an initial investigation, and then 5-fold Cross Validation for tuning the hyper-parameters of the models 


## Evaluation
I chose to primary evaluate the Algorithms based on "Accuracy" metric. In this type of application (predicting customer behavior) we are primary concerned about the best performing model overall. Type 1 or Type 2 erros are similar. In other words, there isn't a major difference between predicting a customer would purchase who did not, or predicting a customer would not purchase who did. The algorithm could be tuned to either be optimistic (recall) or pessemistic (precision). There is further discussion of this trade-off below. 

## Algorithms
This project review 4 algorithms:
- k-nearest neighbors
- logistic regression
- decision trees
- support vector machines (SMV)

The Initial Analysis was to run a simple version of these models without any tuning. This produced the following results:
- Accuracy of SVC: 0.9078
- Accuracy of LogisticRegression: 0.9029
- Accuracy of KNeighborsClassifier: 0.8993
- Accuracy of DecisionTreeClassifier: 0.8823

The performance here is fairly tightly grouped, with SVC performing the best. 


## Tuning

After completing the initial analysis to baseline model performance, I ran a GridSearch to further refine these models and find the optimal hyper parameters. The details of the optimal weights are available in the Notebook, but here are the highlights: 

- Best cross-validated accuracy for LogisticRegression: 0.9141
- Best cross-validated accuracy for SVC: 0.9104
- Best cross-validated accuracy for DecisionTreeClassifier: 0.9056
- Best cross-validated accuracy for KNeighborsClassifier: 0.9022

While all of the models improved, LogisticRegression overtook SVC for the top-spot.

## Confusion Matrixes

For this application, there is not a high cost for either flase positive or false negatives. However, it is still interesting to check the confusion matrices. It could be possible for two models with comparable accuracies to present very different error types. On marginal calls like this one (91.4% accuracy for LogisticRegression and 91.0% accuracy for SVC), business considerations might prefer one type of error over the other. For example, if we were concerned about maximing the productivity of our calls, we might be willing to take the trade of slightly lower overall accuracy for slightly higher precision. Conversely, if we had a limited list of potential customers to call, we might be more concerned about over-looking some "yes" responses and prefer higher recall. Here the Confusion Matrixes do not show much variation in error types
![Confusion Matrix](images/age_distribution.png)
![Confusion Matrix](images/age_distribution.png)
![Confusion Matrix](images/age_distribution.png)
![Confusion Matrix](images/age_distribution.png)

## Feature Importance
Interpretting the Feature Importance of the Logistic Regression model can be tricky. Here are the outputs for the top 10 most impactful features: 


Here is a chart
![Feature Importance](images/age_distribution.png)

## Conclusion
Over-all the LogisticRegression model performs the best, and should be selected to predict 

- Many of the top features are months. Without knowing other details of the business (sign-up practices, monthly discounts etc) it's hard to say that we should conduct these campaigns in March (positive correlation) and avoid it in May (Negative correlation). But these are questions to take and look at potnetial other aspects of the business. Did we do anything different in May/VS/ March
- Contact over the telephone has a negative association. This suggests that calling cellphones is preferable to calling homephones
- poutcome-failure: This variable tracks if a previous campaign was unsuccessful. This implies it would be better

## Possible Continuations

The model could be adjusted to the likelihood that a customer converts. This could be used to prioritize a call list. Since calling as a form of marketing can be expensive, it would be valuable to be able to only call those with a >80% likelihood of purchasing. 

Linear combinations of the numeric features could give the model more expressive power. 

Ensemble techniques could be applied to further improve the model. 





