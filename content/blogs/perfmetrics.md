---
date: "2024-05-02T22:53:58+05:30"
draft: false
hideLastModified: true
summary: A good regression model can more accurately predict the values of the dependent variable we want to predict. Performance evaluation helps us to understand how well the model can predict. Moreover, when choosing between regression models, performance evaluation helps us to identify which of the different models performs better. By comparing between models, we can choose or improve the best model. Performance evaluation also helps us to identify the weaknesses of the model. By identifying areas with incorrect predictions or high errors, we can make changes to improve the model. 
tags:
- R
title: Demystifying Regression Evaluation Metrics
---

# **Demystifying Regression Evaluation Metrics: Understanding SSR, MSE, R², and Adjusted R²**

Regression performance evaluation is a set of statistical measures used to evaluate the accuracy and efficiency of regression analyses. In this post of this series, (previous posts were [how to fit a line](https://medium.com/@ozturkfemre/supervised-learning-in-r-how-to-fit-a-line-cd7d047d1751) and [how to interpret regression output](https://medium.com/@ozturkfemre/supervised-learning-in-r-how-to-interpret-linear-regression-output-8917f6ee832f)) I will try to explain Regression Evaluation Metrics (SSR, MSE, and R² and Adjusted R²).

A good regression model can more accurately predict the values of the dependent variable we want to predict. Performance evaluation helps us to understand how well the model can predict. Moreover, when choosing between regression models, performance evaluation helps us to identify which of the different models performs better. By comparing between models, we can choose or improve the best model. Performance evaluation also helps us to identify the weaknesses of the model. By identifying areas with incorrect predictions or high errors, we can make changes to improve the model. For example, it may be that the wrong features are used or anomalies in the dataset need to be corrected. All things considered, the performance of the model should be evaluated.

# **Sum of Squared Residuals**

First way to evaluate regression model\'s performance is to calculate Sum of Squared Residuals(SSR). In the first step of SSR calculation, we need to calculate residuals. Residual is calculated as follows:

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/0*rPm2TAwhLw_tFbwK.png)

With this formula, we can calculate residual for an observation. Smaller residual means better model. Thus, summing residuals of each observation might seem a good way to evaluate regression model\'s performance. However, summing the residuals below would cancel the residuals above.

Therefore, squaring residuals before summing them which is the SSR is better. The following formula shows how SSR is calculated:

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/0*CP8gtwEfoeS2fofA.png)

where n is the total observation number.

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*n14u8Q8As7PIgN6FKfuAAQ.png)

NOTE: We calculate vertical distance to the line.

SSR is a good way to evaluate a regression model\'s performance, however, it depends on the observation number in the data set. Since we sum of all squared differences between the observed and the predicted values, more residual will increase SSR. In other words, model with more observation will have more Residuals. Thus, we might come up with a interpretation that model with more observation is worse. This might not be the case.

# **Mean Squared Error**

As I stated, model with more observations will have more Residuals. Is there a way to deal with this problem? Of course! We need to calculate Mean Squared Error(MSE). MSE is simply the average of SSR. The following formula shows how MSE is calculated:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/0*75RqOrEr110DI7MO.png)

or

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/0*giSRGZlhcDRSV7aJ.png)

As I stated before, SSR increases when there are more observation in the model. However, MSE can increase or decrease depending only on average residual. Therefore, it is better to evaluate model\'s performance.

However, there are some issues about MSE. Firstly, MSE heavily penalizes large errors due to its squared term. This makes it sensitive to outliers, as even a single outlier can significantly inflate the overall error. In situations where outliers are present, MSE may not accurately reflect the model\'s performance. Also, squaring the errors in MSE amplifies the impact of large errors on the overall metric. This means that the model\'s performance is heavily influenced by a few observations with substantial deviations, which may not be desirable in certain scenarios.

# **R²**

If there is a problem; there is or will be a solution for it. This is for sure. R squared is a solution to both SSR and MSE\'s problems. It does not depend on the size or scale of the data set.

In basic explanation, R squared is calculated by comparing the SSR or MSE around the mean of the dependent variable. Thus we need mean of the dependent variable. The following illustration shows it:

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*I3jD2MGaF0k4mwU-rY_wMA.png)

Just like the illustration, as a first step, we calculate SSR or MSE around the blue line(mean of the spending). In the second step, we calculate SSE or MSE around the model. Then we compare these two. In this way, R square shows us how much our prediction is better than the average of the dependent variable. The following formula shows how R² is calculated:

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/0*JplrCKy91U4V2BPG.png)

However, there are some problems with \$R²\$. First of all, R squared is sensitive to the sample used for model estimation. Different samples may produce different R-squared values, making it difficult to generalize the performance of the model to new data. Also, R squared is unable to distinguish between models with linear relationships and models with non-linear relationships. Even if a model has a relatively high R-squared value, it does not guarantee that the model captures the true underlying functional form of the data. Lastly, R squared tends to increase as the number of independent variables(predictors) in the model increases, even if those predictors do not have any meaningful relationship with the dependent variable. This can be misleading, as adding irrelevant predictors can artificially inflate the R squared value, giving a false sense of model performance.

# **Adjusted R²**

As mentioned earlier, R-squared always increases with increasing number of independent variables and this may reflect the problem of overfitting. To avoid such a situation, a correction factor is added to correct for overfitting while taking into account the actual increase in the explanatory power of the model. This is called Adjusted R square. The following formula shows how Adjusted \$R²\$ is calculated:

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/0*NztV0IXIIv1oir1L.png)

where,\
R² is the standard R² value,\
n is the observation number in the model,\
k is the predictors of the model.

Adjusted R-squared may decrease if more independent variables are added to the model, indicating that the model is less explanatory. Therefore, Adjusted R-square is used to better assess the explanatory power of the model, taking into account model complexity and overfitting. Also, when comparing between two or more models (models with different predictors), Adjusted R square is a more accurate metric than R square.

Just like always:

\"In case I don\'t see ya, good afternoon, good evening, and good night!\"
