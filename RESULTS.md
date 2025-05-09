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

Based off the AUC score the random forest is 0.7808 and the XGBoost is 0.7686. So the random forest did better than the XGBoost model. 

Random first might outperform the other model because of overfitting. Random forests usually has a lot of trees which can lead to overfitting. Random forest also can capture non linear relationships between features which can also contribute to the outperformance. 

Adding time series features improved the model because it allowed them to account for temporal depdencies and also catches patterns that we didn't see before. Random forests might have benefitted more from these features due to the fact that this model can capture complex interactions. 

## Part 3: Logistic Regression with Balanced Data

### Improvement Analysis

In this section, analyze the improvements gained by addressing class imbalance:

- Which metrics showed the most significant improvement?
- Which metrics showed the least improvement?
- Why might some metrics improve more than others?
- What does this tell you about the importance of addressing class imbalance?

The recall and AUC improved by a lot while precision didn't improve that much. When some metrics improve while others don't it usually because of an imbalance. There is also tradeoffs meaning you can get one metric good but have to sacrafice for the other. This is why its important to address imbalance because you don't want a model that ignores the minority class because it will lead to poor recall. Balancing the model will imporve some of the metrics such as the recall and AUC. 

## Overall Conclusions

Summarize your key findings from all three parts of the assignment:

- What were the most important factors affecting model performance?
- Which techniques provided the most significant improvements?
- What would you recommend for future modeling of this dataset?

The most important factors is the actual model. Choosing the model with the highest AUC and better values in metrics is better. Feature engineering is als important because when you include these features it improved the model as we saw in the random forest. Fixing the imabalance was also very helpful because we got precision and recall to not be so highly skewed. 

The ones that gave us the best results was balancing the dataset as we saw a huge imporvement. AUC increased by 3.51% and F1 score improved by 22.15% and recall improved by 156.56%. 

For future models I will for sure be using time-series feature engineering because of how effective it is. Also making sure I check the data if its skewed or not so I can see if I have to balance the data. I will also make sure to monitor the trade offs especially in high stakes applications. 