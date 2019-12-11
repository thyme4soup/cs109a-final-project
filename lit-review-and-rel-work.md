---
nav_include: 1
title: Literature Review and Related Work
---

## Overview

We based our modeling approach on “The Theory of Political Coalitions” by William Riker. It basically posits that a rational politician attempts to form a coalition that is big enough to win, but not bigger. Although the individual candidates for Congress develop their own platforms in order to match their constituencies, these are tethered by the broader platforms developed by the Democratic and Republican parties as they are attempting to win a majority within Congress. Our models seek to encapsulate what groups the parties are building within their respective coalitions.

The primary piece of literature we used was FiveThirtyEight’s models to predict the midterm election. The comparable model to the ones we were building was the “Fundamentals Only” one, which utilizes non-polling factors to predict the races. The other major aspect of the FiveThirtyEight models was the use of polling, which provided a marginal (~1% improvement in accuracy) on their test set of House elections from 1998 to 2016. 

For the purposes of training a set of models on the 2016 house election data and utilizing it to predict the 2018 house elections, we decided it would be best to not include polling data in the feature set. The fundamental issue with polling data, especially in the case of the 2016 election, is that it has a significant amount of missing data; both explicitly in terms of the number of districts polled and, in the case of the 2016 election, representation of Trump voters within the polls. FiveThirtyEight utilizes multivariate imputation for the missing data across all of the elections, but for the 2016 election the missing mechanism is unknown making the procedure invalid. Kennedy et al. describe this and further elaborate on the flaws of the 2016 polling data. 

## Sources

Riker, William (1962). The Theory of Political Coalitions. New Haven and London: Yale University. 

Silver, Nate. “How FiveThirtyEight's House, Senate And Governor Models Work.” FiveThirtyEight, FiveThirtyEight, 12 Sept. 2018, fivethirtyeight.com/methodology/how-fivethirtyeights-house-and-senate-models-work/.

Courtney Kennedy, Mark Blumenthal, Scott Clement, Joshua D Clinton, Claire Durand, Charles Franklin, Kyley McGeeney, Lee Miringoff, Kristen Olson, Douglas Rivers, Lydia Saad, G Evans Witt, Christopher Wlezien, An Evaluation of the 2016 Election Polls in the United States, Public Opinion Quarterly, Volume 82, Issue 1, Spring 2018, Pages 1–33, https://doi.org/10.1093/poq/nfx047
