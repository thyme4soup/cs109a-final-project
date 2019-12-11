# CS109a Final Project

Authors: Michael Chen, Michael Chenevey, Leopold Bottinger

https://thyme4soup.github.io/cs109a-final-project/
 
## Project Overview (Page 1 of website)
 
### Introduction/Motivation
 
TODO (Leo)
 
### Project Goal
 
To use demographic and previous election data to accurately predict the party winner (Democrat or Republic) of the 435 U.S. House of Representatives district. Through these individual district-level predictions, we aim to predict whether the U.S. House of Representatives will have a Democrat or Republican majority in 2018.
 
### Overview of Analysis
 
1)	We first scrape data from TODO (Leo).
 
2)	We format our final feature set that includes previous election data, comprising both presidential and U.S. House of Representatives election results data, and demographic data. The training set is composed of demographic and previous election data from 2016 and before, with the labels being the U.S. House of Representatives election results in 2016. The testing set contains demographic data from 2018 and previous election data with the aim of predicting the labels for the U.S. House of Representatives election results in 2018. We collected the ground truth labels for 2018 for the purposes of measuring accuracy generalization (but never used to fit any models).
 
3)	We conduct an exploratory data analysis to examine which features within the training set show promise in separating the election results in the 2016 U.S. House of Representatives election. We also conduct a number of other analyses to explore the feature set.
 
4)	We fit the following predictive models: LASSO, Ridge Regression, Neural Network, Random Forest, Decision Tree, and k-NN classifiers. We fit the appropriate hyperparameter(s) for each of the models through cross-validation to maximize the accuracy. We also compare the models to a “very simple” model, which looks solely at the last 3 midterm election results and takes a mode of these results.
 
5)	We compare the best performing model of each model type using cross-validation, reporting the training and validation accuracies.
 
6)	For the highest performing models, we perform feature selection to determine which features were most important for the accuracy of the models. This provides us a measure of which features “swing” the results of our highest-performing predictive models.
 
7)	We fit the highest performing predictive models on only the demographic data and report the training and validation accuracies for these models. We perform feature selection on the demographic-only models to determine which demographic features were most important.
 
8)	We fit all the models (including the demographic-only models) on the training set and predict on the test set: the 2018 midterm election feature data. We report the independent test accuracy of these models.
 
## Data Scraping (Page 2 of website)
 
### Objective:
 
TODO (Leo)
 
### Methods and Results:
 
TODO (Leo)
 
 
## Exploratory Data Analysis (Page 3 of website)
 
### Objective:
 
We perform exploratory data analysis to analyze which features are likely to give the best separation between our two outcomes (Republican or Democrat as the elected party in each district). We examine the relationship between features in order to identify which pairs of features may be useful, as well as show correlations between features that may influence our future modeling.
 
### Methods and Results:
 
#### Description of Feature Set
 
TODO (Chenevey)
 
#### Feature Histograms
 
We plot the two overlapping histograms for each of our features: one histogram for districts that ultimately elected a Democrat Representative, and one histogram for districts that ultimately elected a Republican Representative. The histograms show the total count of each value for each feature, which provides a gauge for whether or not any individual feature provides good separation between the final elected party in the districts.
 
Four notable histograms are shown in Figure 1. Figure 1a shows how the final elected party within the districts are related to the percentage of the population that is white within that district. We see a significant difference in shape and distribution between these two histograms. First, in any district that has a population with less than 50% of its population as white, the district always votes Democrat. We see that as the percentage of the district that is white increases, the proportion of districts that vote a Republican Representative into the U.S. House of Representatives increases. Once we get to districts that are above 90% white, the districts predominantly vote in a Republican Representative.
 
Figure 1b shows the relationship between the percentage of the district in the labor force separated by the elected party in the House of Representatives. We see that the Republican and Democrat histograms have a relatively similar shape, except for the fact that the Republican histogram shows a longer tail to the left, i.e. for districts that have a lower than 50% of the population in the labor force, they always vote in a Republican Representative. We also see that the Democrat histogram is shifted to the right, so that districts that have a higher proportion of people in the labor force tend to vote Democrat into the House of Representatives.
 
Figure 1c shows the voting differential in the 2012 U.S. Presidential Election, calculated as % votes for Obama - % votes for Romney. We see that the 2016 midterm elections very closely mirror the party affiliations for the 2012 U.S. Presidential Election, showing that this feature alone would be a high performing discriminator for our outcome variable of interest. However, there is still a small degree of overlap between the two histograms, so there is room for improvement beyond just this feature alone.
 
Finally, Figure 1d shows the percentage of each district’s population that is in a professional, scientific, management, or administration industry. The histograms show that the Democrat histogram is right shifted compared to the Republican histogram, with a higher proportion in one of these industries corresponding to a higher likelihood of voting Democrat in the 2016 U.S. House of Representatives election.
 
#### Pair Plot Analysis
 
In light of the four notable histograms described above, we conducted a pair plot analysis to identify any correlations or other multi-feature correspondence to our outcome variable between pairs of these four features. Figure 2 shows the results of the pair plot analysis for these four features, with the diagonal showing the kernel density estimate for each feature. One particularly interesting subplot is the plot that shows the 2012 Presidential Election voting differential on one axis and the proportion of population that is white on the other axis. We see a large degree of separation between the two parties, especially if a diagonal line is drawn on this plot. This boundary is mostly a product of the voting differential, but there is also some contribution of the proportion of white people within a district. We also see that any plot with the 2012 voting differential on an axis shows great separation from this variable alone, which is what we expect based on our histogram and kernel density estimate for this feature. All other feature pairs do not show a clearly defined separation boundary.
 
#### Analysis of Previous Election Data
 
We wanted to identify any correlations between previous election data included in the analysis. We use Sankey diagrams in order to illustrate the change in voting preferences for each district for (1) the 2008 U.S. Presidential Election to the 2012 U.S. Presidential Election and (2) the 2012 U.S. House of Representatives election to the 2014 U.S. House of Representatives election. The Sankey diagrams are shown in Figure 3. Figure 3a shows that from 2008 to 2012, the number of districts that converted from Republican to Democrat was very small (1 district), and the number of districts that converted from Democrat to Republican was slightly large (32 districts). The remaining districts all showed the same voting preference from the 2008 election to the 2012 election, showing a large degree of correlation in this variable. These general results make sense, because after one party remains in office for one term, there tends to be a swing in preference towards the other party. The 2012 election was conducted after Obama was in office for one term, following this trend. Figure 3b shows a similar pattern from the 2012 to the 2014 U.S. House of Representatives elections, where the number of districts who switched parties was even smaller (15 districts switched from Democrat to Republican, and 2 districts switched from Republican to Democrat).
 
Because of the large degree of correlation in these variables, including all of these variables within our final analysis could have a large implication for our feature analysis. For regression models, we know that regression will underestimate the coefficient of each of these features if they are highly correlated. Then, when we use the coefficient to estimate feature importance, the relative feature importance will not be accurate. A similar argument can be made for feature importance for the other non-regression models as well. However, because our focus for this assignment is on predictive modeling and accuracy, we have opted to include these features. We that these slight differences between the variables can be very important for our predictive modeling, especially because the districts that change party affiliations from election to election are likely the important “swing” districts that are harder to predict election results for. We thus would like to make clear in our feature analysis that when we find that the previous presidential election or House of Representatives results are important predictors, this likely implies that the highly correlated feature is also important to the predictive analysis. In addition, one of the main goals in feature analysis is the determine which demographic features are important in the predictive modeling (since we can already infer from Figure 1c above that previous election results are highly correlated with future election results), so our demographic-only models that do not include these features are unaffected by this correlation between variables.
 
## Model Fitting and Comparison (Page 4 of website)
 
### Objectives:
 
1)	We perform hyperparameter optimization for each of the six predictive models using cross-validation accuracy.
2)	We compare the parameter-optimized models of each of these types of models using average training and validation accuracies during cross-validation.
3)	Fit demographics-only models that use only the demographic features as inputs to see how the performance differs from the full set including the previous election data.
 
### Methods and Results (1):
 
#### Pre-processing
 
To get our dataset in a format compatible with our future model fitting, we have done a number of pre-processing steps for our data. For any features that are quantitative, we standardized the values by feature to be between 0 and 1. For any categorical features, the features are converted into dummy categories that correspond to each category of the categorical feature. The output label (the party that is elected in each district) were encoded in binary, where 0 corresponds to a Democrat elected, and 1 corresponds to a Republican elected.
 
#### LASSO and Ridge Regression
 
For LASSO and Ridge Regression, the penalty parameter is fit by testing penalty terms on the log scale from 1e-4 to 1e4 and choosing the parameter that results in the highest average accuracy on the validation folds of cross-validation.
 
The results for LASSO are shown in Figure 4, and the results for Ridge Regression are shown in Figure 5. We see that the optimal regularization parameter for both LASSO and Ridge Regression is 1. For LASSO, the performance of the model drops off significantly as the penalty term is decreased from 1, and the performance decreases slightly as the penalty term is increased from 1. For Ridge Regression, the performance across the regularization terms above 0.001 are relatively similar, but we choose a penalty term of 1 since it has the highest performance.
 
#### Multilayer Perceptron
 
For fitting the multilayer perceptron, we tune two different hyperparameters: the number of nodes in each hidden layer and the number of hidden layers. The number of nodes that were tested were 64 and 128, whereas the number of hidden layers tested was 2 or 3. We show the performance of all four possible combination of nodes and hidden layers in Figure 6. We see that the performance is very similar across all combinations, but the highest performing combination was 128 nodes and 2 hidden layers. We also did not test other combinations of hyperparameters, because in this small scale hyperparameter tuning, we saw that the performance was relatively unaffected by these hyperparameter adjustments. Because training a neural network for more combinations of hyperparameter tuning is computationally costly and the benefit did not seem to be great, we decided against further hyperparameter tuning.
 
#### Random Forest and Decision Tree
 
For the random forest and decision tree models, we tuned the maximum tree depth parameter, ranging from 1 to 100. We used 100 different trees for the random forest and found that the performance of the random forest was consistent across all different depths tested (Figure 7). The highest performing random forest model had a maximum tree depth of 5, so we chose to use 5, even though there is evidence that many other options for the maximum tree depth would work well as well.
 
For the decision tree, we found that the maximum tree depth of 1 had the largest performance of the different values tested (Figure 8). However, the confidence bars in Figure 8 show that there is overlap between many of the different values of tree depth provided, so there may be another optimal value depending on the dataset. Our evidence points to a maximum tree depth of 1 being optimal, so we used this particular tree depth for downstream analyses of the decision tree model.
 
#### k-NN
 
For the k-NN model, we tuned the number of nearest neighbors to determine how many neighboring observations to consider when making a prediction. We show that the highest performing model on average had 10 nearest neighbors, even though there was similar performance across the different parameters (Figure 9). We used a k-NN with 10 nearest neighbors for downstream analyses.
 
#### “Very Simple” Model
 
We created a “very simple” model as a sanity check to ensure that our models are outperforming a very simple predictive approach. The predictive approach is as follows: first, find the results of the last 3 U.S. House of Representatives elections. Then, take the elected party in at least 2 of the 3 elections (a majority) as the predicted party to win the next election. We report the results of this model in the next section below, with the other model results.
 
### Methods and Results (2):
 
Figure 10 shows the cross-validation results across the best performing model for each type of model. We see that in terms of training accuracy, the random forest has near perfect accuracy, followed by neural network, Ridge Regression, and LASSO. However, we see that for all of the predictive models, excluding the “very simple” model, the training accuracy is higher than the validation accuracy, showing overfitting.
 
The validation is most important, since this best represents the accuracy on an independent set of data compared to the training accuracy. We see that in terms of validation accuracy, the highest performing models are the neural network (multilayer perceptron) and Ridge Regression. The next highest performing model is LASSO, and then the Random Forest. It is important to note that these validation accuracies are all very close and within the error bars, so there is no strong evidence that one is better than the other. We see that there is a drop in average validation accuracy to the decision tree, then the k-NN. The “very simple” model underperforms compared to the other models significantly, having an accuracy of 10% worse compared to the next lowest performing model.
 
Because Ridge Regression had the highest accuracy with the smaller difference between training and validation accuracy, we will choose the Ridge Regression model as our chosen model for the prediction of the 2018 U.S. House of Representatives midterm elections. We will also use the generally high performing models for future analyses in the demographic-only models and feature selection analyses below.
 
### Methods and Results (3):
 
We also fit demographic-only models, which are the Neural Network, LASSO, and Ridge Regression trained only on the features that represent demographics. The previous election data features are left out of the feature set for this analysis. The purpose of this analysis was to (1) determine if we can accurately predict the election results solely based on demographic data and (2) use these models for feature analysis to determine which variables were most important in determining model predictions (described in the next section with the feature importance analysis). The same hyperparameters were used in the demographic-only models as in the full feature set models discussed above.
 
Figure 11 shows the demographic-only model performance (left) and the performance of the corresponding models including both demographics and previous election data (right). We see a larger amount of overfitting in all three demographic-only models, where the gap between the training and validation accuracy is higher compared to the full feature set models. The validation accuracy has gone down by over 10% for each of the models compared to the corresponding full feature set models. The highest performing demographic-model was the Neural Network, which still showed a significant accuracy drop very high performance on the full feature set. The Random Forest performs next best, followed by Ridge Regression. None of the demographic-only models outperform the “very simple” model that used only the previous election data.
 
## Feature Importance Analysis (Page 5 of website)
 
### Objective:
 
1)	To determine which features (of all features tested) in the election districts led to the biggest swings in the results from 2016 midterm election.
2)	To determine which demographic features in the election districts are most important for the 2016 midterm election results for the demographic-only models.
 
### Methods:
 
#### Ridge Regression
 
For feature importance analysis in Ridge Regression, we used bootstrapping in order to get a distribution of values for each coefficient corresponding to each feature. Then, we used these bootstrapped coefficients to create a confidence interval for the true value of this coefficient. We reported the final top 10 predictors most important to the final prediction in the full feature set in Figure 12a, determining importance by the mean coefficient value for the values. The final top 10 predictors in the demographic-only Ridge Regression model is shown in Figure 13a. A variable that has a positive coefficient denotes an important contributor specifically for an elected Republican for that district, and a negative coefficient denotes an important contributor for an elected Democrat.
 
#### Neural Network
 
For the feature importance determination in the Neural Network model, we fit the full training set on the multilayer perceptron architecture described in the Model Fitting and Comparison section. We used the predicted values for the output of the Neural Network as the target variable in a decision tree, and we use the same features as input to the decision tree. Then, we look at which variables were the most important in the decision tree to predict the output of the Neural Network, which described which variables were most important to the Neural Network’s output. The results on the full feature set model are shown in Figure 12b, and the results on the demographic-only feature set model are shown in Figure 13b. All values are positive, because the decision tree reports the relative importance of each feature.
 
#### LASSO
 
For feature importance analysis in LASSO, we fit the model on the full training set. Because LASSO performs a type of feature selection by forcing non-important predictors to 0, we directly looked at the coefficients of the variables to determine feature importance. The results of the most important features in the full feature set are shown in Figure 12c, and the demographic-only LASSO model results are shown in Figure 13c. A variable that has a positive coefficient denotes an important contributor specifically for an elected Republican for that district, and a negative coefficient denotes an important contributor for an elected Democrat.
 
### Results:
 
The results of the feature importance for all three full feature set models are shown in Figure 12 (a, b, c). We see that the majority of the most important features are determined by previous election data across all three models. In specific, the most important previous election data include the party of the incumbent, the voting differential in the U.S. House of Representatives, and the voting differential in the U.S. Presidential Election (see section about Exploratory Data Analysis for a discussion about why we included variables that we have seen that are highly correlated, even though this may skew our feature selection analysis). We see that among the demographic variables within this analysis, we see that the percentage of the district that is white and the proportion of the district’s industry that is within professional services both appear among the most important features at least two of the different models. Other important features that show up in one of the models’ feature analysis include percent of the population that is Latino or Hispanic, proportion of the industry in manufacturing, percent of industry in arts and entertainment, percent of industry in service, and percent of the population with health insurance coverage.
 
The demographic-only feature importance results are shown in Figure 13 (a, b, c). We see that the most important racial variables are the percent of the district population that is White, and the percent that is Hispanic and Latino. These two features persist as close to the top features in all three models. We see a variety of other features that are important in terms of the industry that the district is involved in, including percent in service occupations topping this category across all three models. We also notice that percent within the labor force is an important feature for two of the models as well. Finally, we see that there are a couple of percent of population within certain age categories that are deemed important across, although which age category appears does not seem to be very consistent across models.
 
## Predicting the 2018 Midterm Election (Page 6 of website)
 
### Objective:
 
TODO (Chenevey)
 
### Methods and Results:
 
TODO (Chenevey)
 

