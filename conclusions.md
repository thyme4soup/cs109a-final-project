---
nav_include: 6
title: Conclusions and Future Work
---

## Conclusion

### Review

We were able to successfully build models from demographic and previous election data to accurately predict the results of the elections at the district level for the U.S. House of Representatives. We built baseline models that only included demographic information or (a very simple model) that only included previous election data, and we saw that by a combination of these two kinds of data, we were able to achieve high predictive performance through cross-validation and on the 2018 midterm election data (as an independent test set). We saw that the previous election data features tended to be among the most highly important features to the predictive accuracy of the models, but we saw that the demographic-only models were still able to achieve a high-performing baseline.

### Future Work

One major shortcoming of our result was that we were not able to incorporate a high amount of demographic data into our analysis. Because we wanted to maintain the distinction between the training/cross-validation data and the independent test set data, we collected independent demographic data for 2016 and 2018. This meant that many of the sources of demographic data that we looked at were not feasible for our experimental design, so we had to use a limited amount of information. In addition, because we did not want to use data that was too far back in elections (when trends of demographic data and outcome party are no longer reliable to predict the current landscape of elections), we were limited in using data from too far in the past. However, in terms of future directions, we would like to investigate if some incorporation of outdated data is still useful, and if so, in what capacity. We would also test more types of demographic data that we were not able to test in this research project.
