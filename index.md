---
theme: jekyll-theme-cayman
title: Project Overview
---
Authors: Michael Chen, Michael Chenevey, Leopold Bottinger

Group 27

## Problem Statement

Our overall project goal is to use demographic and previous election data to accurately predict the party winner (Democrat or Republic) of the 435 U.S. House of Representatives district. Through these individual district-level predictions, we aim to predict whether the U.S. House of Representatives will have a Democrat or Republican majority in 2018. 

## Motivation

Because it is difficult to determine who will have the majority in the U.S. House of Representatives even though we have gone through many rounds of elections (and the polls will still often get it wrong), this is a difficult problem that also has far-reaching consequences with the productivity and direction of Congress.
 
## Overview of Analysis
 
1)	We first scrape the social and economic demographic data of the respective congressional districts from the American Community Survey (ACS) for 2016 and 2017. Then we scrape the previous election and incumbency data from the Daily Kos, an American news website. 
 
2)	We format our final feature set that includes previous election data, comprising both presidential and U.S. House of Representatives election results data, and demographic data. The training set is composed of demographic and previous election data from 2016 and before, with the labels being the U.S. House of Representatives election results in 2016. The testing set contains demographic data from 2018 and previous election data with the aim of predicting the labels for the U.S. House of Representatives election results in 2018. We collected the ground truth labels for 2018 for the purposes of measuring accuracy generalization (but never used to fit any models).
 
3)	We conduct an exploratory data analysis to examine which features within the training set show promise in separating the election results in the 2016 U.S. House of Representatives election. We also conduct a number of other analyses to explore the feature set.
 
4)	We fit the following predictive models: LASSO, Ridge Regression, Neural Network, Random Forest, Decision Tree, and k-NN classifiers. We fit the appropriate hyperparameter(s) for each of the models through cross-validation to maximize the accuracy. We also compare the models to a “very simple” model, which looks solely at the last 3 midterm election results and takes a mode of these results.
 
5)	We compare the best performing model of each model type using cross-validation, reporting the training and validation accuracies.
 
6)	For the highest performing models, we perform feature selection to determine which features were most important for the accuracy of the models. This provides us a measure of which features “swing” the results of our highest-performing predictive models.
 
7)	We fit the highest performing predictive models on only the demographic data and report the training and validation accuracies for these models. We perform feature selection on the demographic-only models to determine which demographic features were most important.
 
8)	We fit the most promising models (including the demographic-only models) on the training set and predict on the test set: the 2018 midterm election feature data. We report the independent test accuracy of these models.
