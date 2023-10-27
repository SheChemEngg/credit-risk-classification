# Module 20 Report 

## Overview

* In this study, a dataset of historical lending activity from a lending services company is analyzed for loan risk.  
The risk assessment is classified as ‘0’ for ‘no loan risk’ and ‘1’ for ‘high loan risk’.

Logistic model 'lbfgs' is used to predict outcomes ‘0’ or ‘1’.
The predicted classifications are compared with the data classifications.
If the results emerge to be satisfactory, the model can be successfully used to determine the ‘Creditworthiness’ of borrowers.

* The features in the dataset pertaining to each borrower are: 
 	'loan_size',
 	'interest_rate',
 	'borrower_income',
 	'debt_to_income',
 	'num_of_accounts',
 	'derogatory_marks',
 	'total_debt',
 	'loan_status'.

The last feature 'loan_status', comprising of values '0' and '1' is used as the target to be compared with predictions made by the model.

* The number of '0' ('no risk loan') and the number of '1' ('high risk loan') are obtained using `value_counts` for the target feature.

* The records for borrowers in the dataset are separated into training and testing data in the ratio 0.75 : 0.25, by random selection.
Logical regression model 'lbfgs' is instantiated.
Training features, and training target are fit into the model.
Predictions of target values are made by using the testing portion of features, in the model created with the training data. 

* 'lbfgs' - Limited-memory Broden-Fletcher-Goldfarb-Shanno, is an algorithm suitable for Logistic Regression analysis.  This algorithm is capable of handling large scale data for modeling. In the present example, the data is moderately large, and 'lbfgs' is used for its ease of usage.

* The target data has 625 '1's and 18759 '0's. Due to this large disparity, the results obtained are favorable to '0's and less favorable to '1's.  To remove the bias, RandomOverSampler algorithm is used to boost the '1' values.  With equal number of '0's and '1's, the predictions made by the model show improvement.


## Results


** 'lbfgs' Logistic Regression model with Original Data:
  
  * From the ‘accuracy’ value alone of 99%, the model appears to fit the data well for healthy loan ('0').
    However, ‘accuracy’ is (TP+TN) / (TP+TN+FP+FN). From the Confusion Matrix, (TP+TN) >> (FP+FN). Therefore, (FP+FN) can be neglected yielding a value approaching 100%.

  * The number of outcome ‘1’ is insignificant compared to that of ‘0’ (625 << 18759), resulting in imbalance of outcome numbers. 	Also, TP << TN.
   The dominance of outcome ‘0’, decreases the outcome ‘1’, by resulting in lower ‘precision’, ‘recall’, ‘f1-score’ values for 	outcome ‘1’ compared to those of outcome ‘0’.

  * ‘precision’, ‘recall’, ‘f1-score’ for outcome ‘1’, have the small value of TP in the numerator, which results in 87%, 89%, 88% for these values, respectively.

  * Conclusion: Thus the model does not predict outcome 'high risk loan' as well as it does for 'healthy loan'.
    A more balanced number of occurrences of ‘0’ and ‘1’ could result in values of ‘precision’, ‘recall’, ‘f1-score’ being larger than the present values and  also result in higher value of ‘accuracy’.

  * Note: 'balanced_accuracy score', is the average of 'recall' values for both '1'(89%) and '0'(100%) outcomes and results in ~94%.




** 'lbfgs' Logistic Regression model with Unbiased Data:

  * Using RandomOverSampler, the severe imbalance in number of outcomes ‘1’ and ‘0’ , is removed, resulting in equal number of outcomes for each class (18759 = 18759). Now, TP ~ TN.

  * The ‘accuracy’ value remains at 99%.
    This is because ‘accuracy’ = (TP+TN) / (TP+TN+FP+FN). From the revised Confusion Matrix, (TP+TN) >> (FP+FN). As before, (FP+FN) can be neglected yielding a value approaching 100%.

  * The number of outcome ‘1’ is exactly equal to that of ‘0’ (18759 = 18759).
    ‘precision’, ‘recall’, ‘f1-score’ for outcome ‘1’, have the large value of TP in the numerator, which results in 100%, 99%, 99% for these values, respectively.

  * 'balanced_accuracy score', the average of 'recall' values for both '1'(99%) and '0'(100%) outcomes, improved from ~94.4% to ~99.5%.

  * Conclusion: The model now predicts for outcome 'high risk loan' just as well as it does for 'healthy loan'.
    A balanced number of occurrences of ‘0’ and ‘1’ results in values of ‘precision’, ‘recall’, ‘f1-score’ for both outcomes '1' and '0' as apploaching 100%.

## Summary

From the two sets of classification values discussed above, it can be cocluded that 'lbfgs' Logistic Regression model with Unbiased Data, performed better than the 'lbfgs' the original data.

The reason is, for each parameter calculated in the classification analysis, the values of TN, FP, TP, FN are unbiased and all results are are obtained on equal footing. Increase in most values, indicates that the model performs better with unbiased data.

