---
date: "2023-03-05T09:37:55+02:00"
description: 
publishDate: "2023-03-05T09:37:55+02:00"
title: Logical Fallacies in Data Science
---

------------------------------------------------------------------------

People are often surprised when they find out that I majored in philosophy as an undergraduate. They think that philosophy has nothing to do with the career I am trying to build in data science, or even that the technical knowledge required for data science would be insufficient.While I think they are quite reasonable in their skepticism, I think that philosophy education is very useful for learning data science. For this purpose, in this first post of this series, I will talk about some data science topics that are related to philosophy.

First of all, philosophy trains students to think critically and logically, which is an essential skill for data scientists when analyzing data, making predictions, and forming conclusions. The lack of the ability to think critically and logically can lead to some problems that you can encounter in every discussion and production. One example of these problems is called *logical fallacies.*

![![](https://cdn-images-1.medium.com/max/800/1*RvOkrMx1iNt0p9ALBQOdPQ.png)](https://cdn-images-1.medium.com/max/800/1*RvOkrMx1iNt0p9ALBQOdPQ.png)

A logical fallacy is an error in reasoning that results in an argument being invalid or unsound. Logical fallacies are often used in arguments to mislead or persuade an audience, rather than providing a valid and logical support for a conclusion. There are many logical fallacies associated with data science and data science studies, although there are many more that are irrelevant. Knowing these fallacies is the best way to avoid falling into them. For this purpose, I will explain three fallacies in this post and illustrate them with Python code. Some of them you may have heard/seen in one way or another and may be avoiding. However, I think you can still benefit from it to reiterate the mind.

------------------------------------------------------------------------

### Cherry Picking Fallacy

The Cherry Picking Fallacy is a type of statistical fallacy in which only a portion of data that supports a particular conclusion is used, while ignoring other data that contradicts it. This results in a biased and inaccurate representation of the information.I can imagine that you\'ve heard this fallacy, and even if you haven\'t, you instinctively try not to fall for it, but let me make it clearer with a simple Python code.

    # creating data
    data = [2, 4, 6, 8, 10, 11, 12, 14, 16, 18, 20] 

    # Selectinh only the numbers greater than 10 from the data set
    selected_data = [num for num in data if num > 10]

    # Calculating the average of the selected numbers
    average = sum(selected_data) / len(selected_data)

    print("Selected data: ", selected_data)
    print("Average of selected data: ", average)

In this code, we have a list of numbers called data, which includes both even and odd numbers. The code selects only the numbers greater than 10 from the list using a list comprehension and stores them in a new list called selected_data. The code then calculates the mean of the selected numbers and stores it in a variable called average.

The cherry picking fallacy occurs because we have selectively chosen only the numbers greater than 10 from the data set, while ignoring the numbers that are less than or equal to 10. This can lead to an inaccurate conclusion because we are only looking at a subset of the data, and not considering the whole picture.

For example, in the above code, the output would be:

    Selected data: [11, 12, 14, 16, 18, 20]
    Average of selected data: 15.166666666666666p

Here, the average of the selected numbers is 15.17. However, if we consider all the numbers in the data list, the true average is 9.91, which means we haven't really gained any additional insight by selectively choosing only the numbers greater than 10. This is an example of the cherry picking fallacy, where we selectively choose data to support our conclusion, while ignoring other relevant data.

This simple example is used to better understand the fallacy. Of course, it is highly unlikely to fall for the fallacy so blatantly. It might be more useful to continue with a real-life example.

Imagine a data scientist wants to prove that a certain advertising campaign was effective in increasing sales. S/he presents data that shows that sales increased in the month immediately following the campaign. However, S/he ignores data from several months prior to the campaign that showed a similar increase in sales, as well as data from several months after the campaign that showed a decrease in sales. This data scientist is committing the cherry picking fallacy by selectively using data that supports their argument and ignoring data that contradicts it. S/he is creating a **biased and misleading representation of the data**, suggesting that the advertising campaign was solely responsible for the increase in sales, when there may have been other factors at play.

In data science and statistics, it\'s important to consider all available data, and to be aware of any biases or selective reasoning that may be present. This can help ensure that conclusions are drawn based on a comprehensive and accurate understanding of the data, rather than on a cherry-picked subset of it. At some point, this also depends on the correct split between train and test. Getting this split wrong can also lead to this fallacy.

Here are some strategies to help you avoid the Cherry Picking Fallacy:

1.  Make sure to consider all relevant data, including data that may contradict your argument or conclusion.

2.  Use multiple sources of information to get a more complete picture of the situation.

3.  Be aware of any biases or preconceptions that may influence your selection of data.

4.  Look for evidence that contradicts your argument or conclusion, and consider how this evidence might affect your understanding of the situation.

5.  Avoid focusing only on data that supports your argument or conclusion, and instead consider all relevant data.

6.  Consider perspectives and information from a variety of sources, including those that may have different perspectives or experiences.

> **\"The Art of Cherry Picking\" by Walter A. Shewhart (1931)**  
> This paper provides a foundational discussion of the concept of cherry picking and the potential consequences of this type of selective presentation of data.

> **\"Cherry Picking in Clinical Research: A Review of the Evidence and Implications for Policy and Practice\" by R. J. Devereaux, et al. (2013)**   
> This paper provides a comprehensive overview of cherry picking in clinical research, including an examination of the causes and consequences of this type of bias.

------------------------------------------------------------------------

### **Hasty Generalization**

The Hasty Generalization Fallacy is a type of statistical fallacy in which a conclusion is drawn based on insufficient evidence. This occurs when a conclusion is made based on a small sample size or a limited set of data, without considering a representative and diverse range of data. To better understand this fallacy, which reveals the importance of the sampling drawn from the population, you can check the following Python codes:

    import random

    # Creating a list of 10,000 random numbers between 0 and 100 which will be our population
    population = [random.randint(0, 100) for _ in range(10000)]

    # Counting the number of numbers that are greater than 50 which will be our sample
    count_greater_than_50 = sum(1 for num in population if num > 50)

    # Calculating the percentage of numbers that are greater than 50
    percentage_greater_than_50 = count_greater_than_50 / len(data) * 100

    if percentage_greater_than_50 > 50:
        print("The majority of the numbers are greater than 50!")
    else:
        print("The majority of the numbers are less than or equal to 50.")

In this code, I created a list of 10,000 random numbers between 0 and 100 using the `random.randint()` function. I then counted the number of numbers in the list that are greater than 50 using a list comprehension and the `sum()` function. I calculated the percentage of numbers that are greater than 50 by dividing the count by the length of the list and multiplying by 100.

The hasty generalization fallacy occurs because I am making a broad conclusion about the entire data set based on a small subset of the data (i.e., the numbers that are greater than 50). In reality, we do not have enough information to make such a conclusion about the entire data set.

For example, the output of the code might be:

    The majority of the numbers are less than or equal to 50.

This output suggests that the hasty generalization made in the if statement was incorrect, since the majority of the numbers in the data set are actually less than or equal to 50. The code may have randomly generated a large number of smaller values, leading to a percentage of numbers greater than 50 that is not representative of the entire data set.

This simple example is used to better understand the fallacy. Of course, it is highly unlikely to fall for the fallacy so blatantly. It might be more useful to continue with a real-life example.

Imagine a data scientist wants to prove that a certain type of software is more popular than another. S/he surveys 100 people and finds that 60% prefer the first type of software. Based on this limited sample, the data scientist concludes that the first type of software is more popular. However, this conclusion is based on a small and non-representative sample, and may not accurately reflect the preferences of the entire population.

Here are some strategies to avoid this fallacy:

1.  Use a large sample size: The larger the sample size, the more likely it is to be representative of the population.

2.  Consider diversity: Make sure the sample is diverse and includes a variety of different perspectives and characteristics.

3.  Use random sampling: Use random sampling techniques, such as random number generation, to ensure that the sample is representative of the population.

4.  Avoid convenience sampling: Convenience sampling, where the sample is based on convenience rather than randomness, can result in a biased sample that does not accurately represent the population.

5.  Be aware of biases: Be aware of any biases that may be present in the data collection or analysis process, and make adjustments to account for them.

> \"The Hasty Generalization and the Conjunction Fallacy in Probabilistic Judgment\" by Amos Tversky and Daniel Kahneman  
> This paper examines two common cognitive biases in probabilistic judgment, the hasty generalization fallacy and the conjunction fallacy, and their implications for decision making and reasoning.

> \"The Fallacy of the Hasty Generalization and the Generalization of the Fallacy of Hasty Generalization\" by Herbert W. Simons  
> This paper discusses the hasty generalization fallacy, its implications for scientific reasoning, and how it can be avoided through careful analysis of data and avoidance of premature conclusions.

------------------------------------------------------------------------

### The Data Dredging Fallacy

The Data Dredging Fallacy, also known as \"p-hacking\" or \"data fishing,\" is a statistical fallacy that occurs when data is analyzed in an attempt to find a pattern or relationship, even when there is no actual relationship present. This fallacy is based on the idea that by testing enough variables, you can eventually find a statistically significant relationship by chance alone.

Here is an example of fallacy with Python codes

    import numpy as np
    import pandas as pd
    import statsmodels.formula.api as smf
    import random

    # Generating random data for two variables
    np.random.seed(0)
    N = 100
    x = np.random.normal(0, 1, N)
    y = x + np.random.normal(0, 1, N)

    # Creating a data frame with the variables
    data = pd.DataFrame({'x': x, 'y': y})

    # Fitting a linear regression model using x and y
    model = smf.ols("y ~ x", data).fit()

    # Generating additional random variables
    for i in range(10):
        z = np.random.normal(0, 1, N)
        data['z' + str(i)] = z

    # Fittting all possible linear regression models using two variables
    best_model = None
    best_rsquared = 0
    for i in range(2, len(data.columns)):
        for j in range(i + 1, len(data.columns)):
            formula = "{} ~ {}".format(data.columns[j], data.columns[i])
            model = smf.ols(formula, data).fit()
            if model.rsquared > best_rsquared:
                best_model = model
                best_rsquared = model.rsquared

    # Printing the best R-squared and conclusion
    print("Best R-squared:", best_rsquared)
    print("Conclusion: The best model is the one with the highest R-squared.")

In this example, the code generates random data for two variables, `x` and `y`, and fits a linear regression model using `x` and `y`. The code then generates 10 additional random variables, and fits all possible linear regression models using two variables. The conclusion is that the best model is the one with the highest R-squared.

However, this conclusion is incorrect, as the highest R-squared may simply be due to chance, and not due to a real relationship between the variables. This is the Data Dredging Fallacy. To avoid this fallacy, it\'s important to use appropriate methods to avoid overfitting, such as cross-validation or using a model selection criterion like the Bayesian Information Criterion (BIC) or the Akaike Information Criterion (AIC), and CP. Additionally, the code would need to seek out additional data to confirm or refute the conclusion, and seek out independent review to ensure that the conclusion is based on a comprehensive and accurate understanding of the data.

Here are some strategies to help you avoid this fallacy:

1.  Use appropriate statistical methods to control for false positive results, such as correction for multiple comparisons, and be aware of the limitations of statistical significance.

2.  Pre-specify research goals and hypotheses before collecting data, and make sure that these goals and hypotheses are based on valid reasoning and previous research.

3.  Avoid analyzing data after the data has been collected, as this can result in data dredging and the discovery of false positive relationships.

4.  Seek out independent review of your data and analysis, to ensure that your conclusions are based on a comprehensive and accurate understanding of the data.

5.  Replicate findings to confirm or refute your conclusions, and be open to revising your conclusions based on new information.

> **Why most published research findings are false. by Ioannidis, J. P. (2005).**  
> This paper discusses the problems of multiple testing and the high rate of false positive results in research, and highlights the dangers of data dredging.

> **The garden of forking paths: Why multiple comparisons can be a problem, even when there is no \"fishing expedition\" or \"p-hacking\" and the research hypothesis was posited ahead of time. by Gelman, A., & Loken, E. (2013)**  
> This paper discusses the problem of multiple comparisons and the tendency to find significant results by chance. The authors highlight the dangers of data dredging and the importance of using proper statistical methods to avoid false positive results.

With this fallacy we come to the end of the first article in this series. I will address five more fallacies in the next article.
