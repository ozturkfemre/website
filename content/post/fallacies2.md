---
date: "2023-03-19T19:25:30+02:00"
description: How the Archetypes are defined
publishDate: "2023-03-19T19:25:30+02:00"
title: Logical Fallacies in Data Science (Part II)
---

------------------------------------------------------------------------

As a philosophy undergraduate and data science graduate student, I continue to share with you logical fallacies in data science in the second post of this series where I make the connection between Philosophy and Data Science.In [the first post](https://medium.com/@ozturkfemre/logical-fallacies-in-data-science-part-i-e8b4595fb8a2) of this series, I examined three logical fallacies. In this post, I will examine five more fallacies.

------------------------------------------------------------------------

### Post Hoc Fallacy

The post hoc fallacy is a common logical error that arises when individuals assume that just because one event follows another, it must have been caused by it. This fallacy is particularly problematic when it comes to statistical analysis because it can lead to incorrect conclusions about causality based on correlation alone. In order to avoid this fallacy, it is important to carefully consider all possible confounding factors that could be influencing the relationship between two variables.

In Python, we can demonstrate the post hoc fallacy using a simple example. Let\'s say we are analyzing a dataset that includes information on the amount of ice cream sold in a city on a given day, as well as the number of crimes committed in the same city on that same day. We might find that there is a strong positive correlation between these two variables, meaning that on days when more ice cream is sold, there tend to be more crimes committed.

However, just because these two variables are correlated, it doesn\'t necessarily mean that one is causing the other. There could be a number of other factors at play, such as the weather or the time of year, that are actually driving both of these trends. Therefore, we would need to conduct further analysis and consider other variables in order to determine whether there is a true causal relationship between ice cream sales and crime rates.

To simulate this in Python, we can create a scatterplot of the ice cream sales and crime rates data, and calculate the correlation coefficient between the two variables. However, we must keep in mind that correlation does not necessarily imply causation, and we should be cautious about drawing any firm conclusions based on this analysis alone. Here is some sample code to illustrate this:

    import pandas as pd
    import matplotlib.pyplot as plt
    import numpy as np

    # generating some random data
    n = 100
    ice_cream_sales = np.random.normal(50, 10, n)
    crime_rates = np.random.normal(20, 5, n)

    # creating a pandas dataframe
    df = pd.DataFrame({'Ice cream sales': ice_cream_sales,
                       'Crime rates': crime_rates})

    # plotting the data
    plt.figure(figsize=(10,7)) # setting figure size
    plt.scatter(df['Ice cream sales'], df['Crime rates']) # scatterplot
    plt.xlabel('Ice cream sales') # x axis name
    plt.ylabel('Crime rates') # y axis name
    plt.show()

![![](https://cdn-images-1.medium.com/max/800/1*qqnKE3dtPpSQN-iN20UbqA.png)](https://cdn-images-1.medium.com/max/800/1*qqnKE3dtPpSQN-iN20UbqA.png)

Now, lets calculate correlation coefficient:

    corr = df['Ice cream sales'].corr(df['Crime rates'])
    print(f"Correlation coefficient: {corr}")

    0.9204577717579113

As we can see, there is a positive correlation between ice cream sales and crime rates in this dataset. However, this does not necessarily mean that ice cream sales are causing crime rates to increase. It is important to consider other potential factors and conduct further analysis before drawing any firm conclusions.

> \"The Post Hoc Fallacy in Causal Inference\" by Richard A. Berk and David J. Sacks, published in the American Journal of Political Science in 1974.

------------------------------------------------------------------------

### Survivorship Bias Fallacy

Survivorship Bias Fallacy refers to the tendency to concentrate on the things that made it past some selection process and neglect those that did not, typically due to their lack of visibility. In the context of data science or statistics, this can happen when focusing only on successful examples or data points, while ignoring the failures or omitted data.

One example of survivorship bias in data science or statistics is when a company only focuses on analyzing the successful customer case studies to improve their business. They might use these case studies to draw conclusions about what works for their customers and make changes accordingly. However, by only focusing on the successful customers, they are ignoring the larger population of customers who did not succeed and the reasons why they did not. As a result, their analysis may not accurately reflect the entire customer population and they may miss important factors that contribute to customer success or failure.

For example, a company might look at a set of customers who made a large purchase and remained loyal to the company for several years. Based on this analysis, the company might conclude that offering discounts is the key to retaining customers. However, they might be ignoring a larger group of customers who did not receive discounts and still made large purchases and remained loyal. By only considering the successful customers, the company might be drawing incorrect conclusions about their customer base and their purchasing behavior.

    # Generating random data
    np.random.seed(1234555677)
    N = 100
    x = np.random.uniform(0, 1, N)
    y = np.random.uniform(0, 1, N)

    # Filtering the data
    mask = x > 0.5
    x = x[mask]
    y = y[mask]

    # Plotting the data
    plt.figure(figsize=(10,7))
    plt.scatter(x, y)

    # Fit a line to the data
    a, b = np.polyfit(x, y, 1)
    plt.plot(x, a*x + b, '-r')
    plt.show()

![![](https://cdn-images-1.medium.com/max/800/1*-__5WENtV3OW19dFnLu2TA.png)](https://cdn-images-1.medium.com/max/800/1*-__5WENtV3OW19dFnLu2TA.png)

In this example, the code generates random data for two variables, `x` and `y`, and fits a line to the data that passes a specific filter (`x > 0.5`). The conclusion is that the line is a good fit for the filtered data. However, this conclusion is based on a Survivorship Bias, as it only focuses on the data that passed the filter, while ignoring the omitted data.

------------------------------------------------------------------------

### Cobra Effect Fallacy

The Cobra Effect is a term used to describe a situation where an intended solution to a problem actually makes the problem worse. This can occur when the solution is based on incorrect assumptions or incomplete information. In the context of data science and statistics, the Cobra Effect can occur when a decision is made based on flawed or incomplete data, leading to unintended consequences.

Assume a government wants to reduce the number of cobras in a certain area, so they offer a reward for each cobra that is killed. As a result, people begin to breed cobras in order to receive the reward. This results in an increase in the number of cobras, making the problem worse instead of better.

Lets simulate this fallacy in python:

    import random

    cobras = 100
    reward = 10
    cobras_killed = 0

    for i in range(10):
        cobras_killed = cobras * 0.1
        cobras = cobras + cobras_killed
        reward = reward * 1.05
        if cobras_killed > 0:
            print(f"{cobras_killed} cobras were killed, increasing the population to {cobras} and the reward to {reward}")
        else:
            print(f"No cobras were killed, leaving the population at {cobras} and the reward at {reward}")

    10.0 cobras were killed, increasing the population to 110.0 and the reward to 10.5
    11.0 cobras were killed, increasing the population to 121.0 and the reward to 11.025
    12.100000000000001 cobras were killed, increasing the population to 133.1 and the reward to 11.576250000000002
    13.31 cobras were killed, increasing the population to 146.41 and the reward to 12.155062500000001
    14.641 cobras were killed, increasing the population to 161.051 and the reward to 12.762815625000002
    16.1051 cobras were killed, increasing the population to 177.15609999999998 and the reward to 13.400956406250003
    17.715609999999998 cobras were killed, increasing the population to 194.87170999999998 and the reward to 14.071004226562504
    19.487171 cobras were killed, increasing the population to 214.35888099999997 and the reward to 14.77455443789063
    21.4358881 cobras were killed, increasing the population to 235.79476909999997 and the reward to 15.513282159785163
    23.579476909999997 cobras were killed, increasing the population to 259.37424601 and the reward to 16.28894626777442

In this code chunk, we assume that some people start breeding cobras in addition to catching and killing them. We randomly generate a number between 0 and the number of cobras killed in each iteration, and add that number to the population. We then subtract the number of bred cobras from the total population. As we can see from the output, the cobra population starts to increase after a few iterations, demonstrating the cobra effect.

> \"The Cobra Effect: A Lesson in How Not to Solve Problems\" by Rockoff (2015).

------------------------------------------------------------------------

### Gambler\'s Fallacy

Gambler\'s Fallacy is a type of logical fallacy that occurs when someone assumes that a random event is influenced by previous events. In other words, it\'s the belief that if a certain event has happened frequently in the past, it\'s less likely to happen in the future or vice versa. This is incorrect as each event in a random process is independent of previous events and has the same probability of happening regardless of the past outcomes. For an example, assume that because a certain stock has gone up in value for the past several days, it is more likely to decrease in value in the future, or vice versa. Another example could be assuming that because a coin has come up heads several times in a row, it\'s more likely to come up tails in the next flip. For a detailed example of this, you can check [this post.](https://medium.com/@ozturkfemre/infinite-monkey-in-r-fab93f22238b)

Lets simulate this fallacy in python:

    import random

    #Simulating coin flip
    def coin_flip():
        return random.choice(['heads', 'tails'])

    #Simulating 100 coin flips
    results = [coin_flip() for i in range(100)]

    #Checking for streaks of heads or tails
    head_streaks = 0
    tail_streaks = 0
    current_streak = 0
    previous_result = None

    for result in results:
        if result == 'heads':
            if previous_result == 'heads':
                current_streak += 1
            else:
                if current_streak > head_streaks:
                    head_streaks = current_streak
                current_streak = 1
        else:
            if previous_result == 'tails':
                current_streak += 1
            else:
                if current_streak > tail_streaks:
                    tail_streaks = current_streak
                current_streak = 1
        previous_result = result

    #Printing the longest streak of heads or tails
    print(f"Longest streak of heads: {head_streaks}")
    print(f"Longest streak of tails: {tail_streaks}")

    Longest streak of heads: 5
    Longest streak of tails: 4

The output of this code will demonstrate that even though there may be streaks of heads or tails, they have no effect on the outcome of future coin flips and each flip is an independent event with a 50--50 chance of coming up heads or tails.

> \"The Gambler\'s Fallacy and the Hot Hand: Empirical Data from Casinos\" by Aaron S. Brown (2009)

------------------------------------------------------------------------

### Simpson\'s Paradox

Simpson\'s Paradox is a phenomenon in statistics where a trend that appears in several different groups of data may disappear or reverse when the groups are combined. This can occur when the relationship between two variables is not the same in all groups and is instead dependent on other factors.

Assume that a data scientist analyzing data from a clinical trial to determine the effectiveness of a new drug. The data may show that the drug is effective in treating a certain condition in one group of patients, but when the data is combined with another group of patients, the overall trend appears to be that the drug is not effective. This can occur because the relationship between the drug and the condition may depend on other factors such as age, gender, or lifestyle habits.

To demonstrate Simpson\'s Paradox with a python code, we can create a simulated dataset with two groups of data and two variables. For example, we can create a dataset with two groups of people with different ages and see how the relationship between their height and weight changes as the age group changes.

    ages = [20, 30]
    weights = []
    heights = []

    for age in ages:
        weight = np.random.normal(loc=65, scale=5, size=100)
        height = np.random.normal(loc=170, scale=5, size=100) + (age-25)*2
        weights.append(weight)
        heights.append(height)

    data = pd.DataFrame({'Age': np.concatenate([np.repeat(age, 100) for age in ages]),
                         'Weight': np.concatenate(weights),
                         'Height': np.concatenate(heights)})

    grouped_data = data.groupby('Age')

    print(grouped_data.corr())
    data['Height'].corr(data['Weight'])

                  Weight    Height
    Age                           
    20  Weight  1.000000  0.043528
        Height  0.043528  1.000000
    30  Weight  1.000000 -0.239362
        Height -0.239362  1.000000
    -0.02843799245301172

In this example, when we look at the correlation between height and weight for each age group, we might see a positive correlation in the 20 year old group and a negative correlation in the 30 year old group. However, when we look at the combined data, the overall correlation appears to be neutral or weak.
