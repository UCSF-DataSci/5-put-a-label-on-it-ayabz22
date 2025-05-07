# Assignment 5: Health Data Classification Results

This file contains your manual interpretations and analysis of the model results from the different parts of the assignment.

## Part 1: Logistic Regression on Imbalanced Data

### Interpretation of Results

In this section, provide your interpretation of the Logistic Regression model's performance on the imbalanced dataset. Consider:

- Which metric performed best and why?
- Which metric performed worst and why?
- How much did the class imbalance affect the results?
- What does the confusion matrix tell you about the model's predictions?

The accuracy metric performed the best with a value of 91.95%. It is probably high because of the clas imbalance meaning the model is likely predicting the majority class correctly most of the time.  

The recall metric performed the worst with a value of 32.39%. The low recall means that the model is failing to capture many of the positive cases, likley due to class imabalance. 

The imbalance impact score is 1 which means that there is a severe effect of class imbalance on the results. With the high accuracy and low recall this means that the model is predicting the majority class correctly but is struggling predicting the minority class. 

The confusion matrix tells us the true positives, true negatives, false positives, and false negatives. So with the low recall we tend to see a high value of false negatives. 

## Part 2: Tree-Based Models with Time Series Features

### Comparison of Random Forest and XGBoost

In this section, compare the performance of the Random Forest and XGBoost models:

- Which model performed better according to AUC score?
- Why might one model outperform the other on this dataset?
- How did the addition of time-series features (rolling mean and standard deviation) affect model performance?

*Your analysis here...*

## Part 3: Logistic Regression with Balanced Data

### Improvement Analysis

In this section, analyze the improvements gained by addressing class imbalance:

- Which metrics showed the most significant improvement?
- Which metrics showed the least improvement?
- Why might some metrics improve more than others?
- What does this tell you about the importance of addressing class imbalance?

*Your analysis here...*

## Overall Conclusions

Summarize your key findings from all three parts of the assignment:

- What were the most important factors affecting model performance?
- Which techniques provided the most significant improvements?
- What would you recommend for future modeling of this dataset?

*Your conclusions here...*