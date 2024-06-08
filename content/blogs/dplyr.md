---
date: "2023-12-02T22:53:58+05:30"
draft: false
hideLastModified: true
summary: dplyr package is an R package for data manipulation and data transformation. This package enables many operations used for data analysis to be done quickly and easily. dplyr package is very popular in the R community and is widely used by many users. In particular, users working on large datasets appreciate the importance of the dplyr package, which allows data processing operations to be done quickly. Since it is a very helpful package, in this article, I will explain each function in dplyr in detail.
tags:
- R
title: Data Manipulation with dplyr
---

`dplyr` package is an R package for data manipulation and data transformation. This package enables many operations used for data analysis to be done quickly and easily. `dplyr` package is very popular in the R community and is widely used by many users. In particular, users working on large datasets appreciate the importance of the dplyr package, which allows data processing operations to be done quickly. Since it is a very helpful package, in this article, I will explain each function in `dplyr` in detail.

`dplyr` package includes the following basic functions that I will explain in this article:

-   filter() --- selects rows that meet a given condition,

-   select() --- selects specific columns,

-   mutate() --- creates a new column or modifies an existing column,

-   summarize() --- creates a summary of the data,

-   arrange() --- sorts data by a given column,

-   group_by(): groups by a specific column and allows group-based operations when used in conjunction with other dplyr functions,

-   distinct(): removes repeated rows.

To use `dplyr` package, it must first be installed in R. If not, it can be installed using the code below:

```         
install.packages("dplyr")
```

After installing the package, you need to install the package using the following code to be able to use it in R code:

```         
library(dplyr)
```

This code will indicate that the dplyr package is installed in your code and you can use all the functions included in the package.

------------------------------------------------------------------------

### filter()

filter() is a function used to select rows that satisfy a certain condition. This function is used to create a subset of the data set. Consider the famous Iris dataset as an example. Suppose we want to observe the data of the cetosa species in the Iris dataset. We can use the filter() function for this.

filter() function is used as follows:

```         
filter(data, condition)
```

-   \"data\" argument must be a data frame containing the data set to be subsetted.

-   \"condition\" argument is a logical expression that specifies the conditions that determine which rows to select.

Here is the example I mentioned:

```         
filter(iris, # data          
Species == "setosa" # condition 
)
```

Assume that we have a data of students with columns age, income, gender etc. For explaining the other arguments that can be used for filter function, I will use this data.

Other arguments that can be used in filter() are:

-   ***\"&\" and \"\|\" operators***: Used to combine multiple conditions. \"&\" indicates that all conditions must be true, while \"\|\" indicates that at least one condition must be true.

-   ***! operator***: Takes the inverse of the condition. That is, rows that do not satisfy the condition are selected.

-   ***any_vars()*** and ***all_vars()*** functions: Used to specify conditions for all columns. For example, \"any_vars(. == \'Yes\')\" selects rows where the value in all columns is \"Yes\", while \"all_vars(. == \'Yes\')\" selects rows where the value in all columns is \"Yes\".

-   ***between()*** function: Used to select values that are within a certain range. For example, \"between(age, 18, 25)\" It selects students between 18 and 25 years of age.

-   ***across()***: Used to apply a specific condition to a specific set of columns. For example, \"filter(data, across(starts_with(\'age\')), \> 18)\" selects all columns titled \"age\" in the dataset and selects those that are older than 18.

-   ***everything()***: Used to select all columns.

-   ***matches()***: Used to select columns that match a specific pattern. For example, \"filter(data, matches(\'\^age\_\'))\" Selects all columns starting with \"age\_\".

-   ***num_range()***: Used to select columns with a specific range of numbers. For example, \"filter(data, num_range(\'age\', 1:3))\" Selects the columns \"age1\", \"age2\" and \"age3\".

-   ***one_of()***: Used to select columns with a specific set of columns. For example, \"filter(data, one_of(c(\'age\', \'gender\', \'income\')))\" selects the columns \"age\", \"gender\" and \"income\".

------------------------------------------------------------------------

### select()

select() function is used to select or remove columns from data frames. In addition to selecting columns in data frames, the select() function can also be used to rename columns or create new columns.

select() function accepts the following arguments:

-   ***data***: The data frame to select.

-   ***starts_with()***: Selects all columns starting with a specified prefix.

-   ***ends_with()***: Selects all columns ending with a given prefix.

-   ***contains()***: Selects all columns that contain a specified string.

-   ***matches()***: Selects all columns that match a given pattern.

-   ***num_range()***: Selects columns with a specified number range.

-   ***all_of()***: Selects all columns in a specified column list.

For example, the code below specifies the columns to select and the select() function selects them:

```         
selected_data <- select(data, column1, column2, column3)
```

Also, the code below selects all columns starting with \"name\":

```         
selected_data <- select(data, starts_with("name"))
```

In addition to selecting columns in data frames, the select() function can also be used to rename columns or create new columns. For example, the following code renames the column \"column1\" to \"new_column\":

```         
selected_data <- select(data, new_column = column1)
```

or the following code selects the columns \"column1\" and \"column2\" and creates a new column called \"sum\" which is the sum of these columns:

```         
selected_data <- select(data, column1, column2, sum = column1 + column2)
```

------------------------------------------------------------------------

### mutate()

mutate() is used to perform calculations on the columns of an existing dataset and to add new columns. This function can be used to perform various data manipulation operations on columns in the dataset, such as performing mathematical operations, merging a column with other columns, performing logical or character-based operations.

The arguments of the mutate() function are:

-   ***data***: specifies the dataset on which to perform the operation.

-   ***...***: arguments for multiple operations together, used to create new columns. The operation name, the name of the new column and the operation itself are separated by commas between these arguments.

For example, the following code adds a new column using the mutate() function on an existing dataset \"iris\":

```         
mutate(iris, new_col = Sepal.Length + Sepal.Width)
```

This sample script collects the \"Sepal.Length\" and \"Sepal.Width\" columns from the \"iris\" dataset and saves them as a new column \"new_col\".

Another example can be used to convert values from one column in an existing dataset to another column. The following example converts the values in the \"mpg\" column in the \"mtcars\" dataset into a new column named \"km_per_liters\":

```         
mutate(mtcars, km_per_liters = mpg * 0.425144)
```

------------------------------------------------------------------------

### summarize()

summarize() is used to summarize observations in a dataset. This function can calculate a number of statistical summarizations such as sum, mean, highest/lowest value, standard deviation, median.

The arguments of summarize() are:

-   ***data***: specifies the data set on which to perform the operation.

-   ***...***: arguments for multiple operations together, used to create a new summary column. The operation name, the name of the new summary column and the operation itself are separated by commas between these arguments.

For example, the following code uses the summarize() function to calculate the mean and standard deviation for the \"Sepal.Length\" and \"Sepal.Width\" columns in the \"iris\" dataset:

```         
summarize(iris, # data           avg_sepal_length = mean(Sepal.Length), # mean,            avg_sepal_width = mean(Sepal.Width), # mean,            sd_sepal_length = sd(Sepal.Length), # standard deviation           sd_sepal_width = sd(Sepal.Width) # standard deviation           )
```

This sample code calculates the mean and standard deviation for the \"Sepal.Length\" and \"Sepal.Width\" columns in the \"iris\" dataset and creates a new summary column.

summarize() function can be used to apply statistical operations to any numeric column in the dataset. For example, it is possible to calculate the total purchase amount for the \"purchase amount\" column in a customer dataset, calculate the average sales for the \"product sales\" column in a product dataset, or calculate the lowest and highest salary for the \"salary\" column in an employee dataset.

------------------------------------------------------------------------

### arrange()

arrange() is used to sort columns in a dataset in a specific order. The function sorts in ascending order by default, but the desc() function can be used for reverse sorting.

The arguments of the arrange() function are:

-   ***data***: specifies the data set on which to perform the operation.

-   ***...***: arguments containing the name of one or more columns used for sorting. Each argument determines the sort priority. Sorting is done starting from the prioritized columns.

For example, the following script can be used to sort by the \"mpg\" column in the \"mtcars\" dataset:

```         
arrange(mtcars, mpg)
```

Here, the arrange() function sorts all observations in the \"mtcars\" dataset in ascending order by the \"mpg\" column.

Furthermore, the sort type of each column in the sort order can be specified. For example, the following code can be used to sort the \"mpg\" column in descending order, and then the \"wt\" column in ascending order:

```         
arrange(mtcars, desc(mpg), wt)
```

Here, desc() sorts the \"mpg\" column in descending order and sorts the \"wt\" column in ascending order.

------------------------------------------------------------------------

### group_by()

group_by() is used to group a dataset by one or more columns. The group_by() function is used in conjunction with summarize(), count(), mutate() and many other `dplyr` functions to perform grouping operations.

The arguments of the group_by() function are:

-   ***dat***a: specifies the dataset on which to perform the operation.

-   ***...***: arguments containing the name of one or more columns used to group the dataset. When more than one column is given, grouping is done between columns.

For example, the following code can be used to group by the \"cyl\" column in the \"mtcars\" dataset:

```         
group_by(mtcars, cyl)
```

Here, the group_by() function groups all observations in the \"mtcars\" dataset by the \"cyl\" column. This creates as many groups as the number of unique values in the \"cyl\" column.

It is also possible to perform grouping operations using the summarize() function in combination with the group_by() function. For example, the following code can be used to calculate the average mpg values corresponding to each number of cylinders in the \"mtcars\" dataset:

```         
group_by(mtcars, cyl) %>% summarize(avg_mpg = mean(mpg))
```

Here, the group_by() function groups the \"mtcars\" dataset by the \"cyl\" column. Then the summarize() function calculates the average mpg value for each group and creates a new column named \"avg_mpg\".

> pipe operator (%\>%) is an operator used in packages such as dplyr and magrittr in the R programming language. The pipe operator is used to use the result of one operation as input to another operation. This improves the readability of the code and makes it easier to write chains of operations.

------------------------------------------------------------------------

### distinct()

distinct() is a function used to find unique values in a data set. This function can return unique values in specific columns or unique values in all columns.

The arguments of the function are:

-   ***data***: the data set for which we want to find unique values.

-   ***...***: variable arguments used to specify the columns we want to use to find unique values. For example, distinct(data, column1, column2).

For example, suppose we want to find only unique cars in the mtcars dataset. The following code demonstrates the use of the distinct() function:

```         
unique_cars <- distinct(mtcars, c("mpg", "cyl", "gear"))
```

------------------------------------------------------------------------

I studied the book [R for Data Science](https://r4ds.had.co.nz/) to write this article. You can check [Posit Cloud](https://posit.cloud/learn/primers/2) to practice the functions in this article.

That was the end of this post. Just like always:

\"In case I don\'t see ya, good afternoon, good evening, and good night!\"
