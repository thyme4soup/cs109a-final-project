---
nav_include: 5
title: Predicting the 2018 Midterm Election
---
 
## Objective
 
The objective here is to use model selection and data methods from 2016 to predict the 2018 election outcome. 
 
## Methods and Results

### Selected Models

We selected the top-performing models found during testing and applied them to the test data. These models were LASSO, Ridge, Neural Network, and Random Forest.

### Results

The following models were trained using available 2016 data in two forms: with and without previous election data (see data exploration section for more info). The accuracies reported describe the models' efficacy on predicting 2018 outcomes.

| Model          | Accuracy on Full Test Data | Accuracy on Demographic Only Data |
|----------------|---------------------------:|----------------------------------:|
| LASSO          |                     90.93% |                            79.93% |
| Ridge          |                     91.16% |                            79.77% |
| Neural Network |                     91.63% |                            76.28% |
| Random Forest  |                     89.53% |                            82.79% |

## Interpretation

![Figure 14](figures/14.png "Figure 14)
