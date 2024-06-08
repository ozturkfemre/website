---
date: "2024-02-02T22:53:58+05:30"
draft: false
hideLastModified: true
summary: purrr package is a tool for the R programming language and an interface designed for data exploration and data analysis. In particular, this package aims to facilitate basic data processing functions such as exploring, summarizing, visualizing and cleaning data sets. It can be used with other popular R packages for data processing and analysis. For example, by using it with packages like dplyrand ggplot2, you can further enhance the data analysis process.
tags:
- R
title: Purrr in R, a powerful tool for iteration
---

# **Purrr in R: A powerful tool for iteration**

`purrr` package is a tool for the R programming language and an interface designed for data exploration and data analysis. In particular, this package aims to facilitate basic data processing functions such as exploring, summarizing, visualizing and cleaning data sets. It can be used with other popular R packages for data processing and analysis. For example, by using it with packages like [`dplyr`](https://medium.com/@ozturkfemre/data-manipulation-with-dplyr-5a3ded3768b3)and `ggplot2`, you can further enhance the data analysis process.

`purrr` package and *apply* family (apply(), sapply(), lapply(), etc.) provide similar but different tools. Both provide common functions used for data manipulation and analysis in R. However, *apply()* family is more commonly used to apply functions on multidimensional data structures such as matrices or arrays, while the purrr package is usually applied to one-dimensional data structures such as lists or data frames for data processing, exploration and summarization. Also, *apply()* family can only apply a single function to every element in a data structure, while the purrr package can apply a range of functions to every element in a data structure through functions such as map() or map2(). Therefore, the purrr package can provide more flexibility and powerful functionality than *apply()* family.

In this post, I will go through all the functions in `purrr`package, the arguments in these functions in detail, and then I will make an example for each function. I hope it will be a purrrfect resource for those who want to learn `purrr`package.

# **map()**

map() function applies the specified function to each element in a data structure and returns the results as a list. This function is useful for performing repeated operations for each element in a data structure.

The map() function takes the following arguments:

-   .x: The data structure to which the function to be applied will be applied (for example, a vector or a list).

-   .f: The function to apply.

-   ...: Additional arguments required by the function.

For an example use case, let\'s consider the iris dataset.

```         
library(purrr) # call the purrr library  df <- iris[1:4] # selecting only numerical values means <- map(df, # data set              mean # function to apply each column) print(means)
```

```         
$Sepal.Length [1] 5.843333  $Sepal.Width [1] 3.057333  $Petal.Length [1] 3.758  $Petal.Width [1] 1.199333
```

In this example, we used the map() function to calculate the average of each variable in the iris dataset. This can be used as a common example for data exploration and summarization.

# **map2()**

map2() function is similar to map(), but applies the specified function for each pair of items in the two data structures and returns the results as a list. This function is useful in situations where mappings between two data structures are made (for example, mapping similar properties in two different data sets).

map2() takes the following arguments:

-   .x: The first data structure (for example, a vector or a list).

-   .y: The second data structure.

-   .f: The function to apply.

-   ...: Additional arguments required by the function.

For an example use case, let\'s multiply Sepal.Length and Sepal.Width variables in the iris dataset.

```         
# lets create two vectors vec1 <- iris$Sepal.Length vec2 <- iris$Sepal.Width  # multiplying two vectors element by element with the map2 function and return the result as a vector result <- map2(vec1, vec2, ~ .x * .y)  # printing the first result print(result[[1]])
```

```         
[1] 17.85
```

# **map_df()**

map_df() function is an iteration function like the map() function, but combines the results into a data frame while map() combines the results into a list.

map_df() function has similar arguments to map(). The first argument is the function. The second argument is the list (.x) to which the function will be applied. The third argument is the parameters of the function (...). In addition, map_df() has a few more optional arguments, but these optional arguments are usually not used.

When the results of the function are data of the same length, the map_df() function is very useful because the results are concatenated. In the following example, I will use the map_df() function to calculate the average Sepal.Length and Sepal.Width of different flower types in the iris dataset. This time, I will combine it with a `dplyr`function called split.

```         
iris %>%   split(.$Species) %>%   map_df(~ summarise(.x, mean_sepal_length = mean(Sepal.Length), mean_sepal_width = mean(Sepal.Width)))
```

```         
  mean_sepal_length mean_sepal_width 1             5.006            3.428 2             5.936            2.770 3             6.588            2.974
```

# **pmap()**

pmap() (parallel map) function is used to execute a function on multiple arguments in parallel. This function executes a function on elements in a data.frame or list and combines the results into a single data structure.

The arguments required to use the pmap() function are as follows:

-   .l: Elements in a list or data frame (data.frame). These elements represent the different arguments of the function.

-   .f: The function to be applied.

-   ...: Additional arguments to the function.

The following is an example of using the pmap() function:

```         
# creating a dataframe my_data <- data.frame(x = c(1, 2, 3), y = c(4, 5, 6), z = c(7, 8, 9))  # calculating the sums between columns using the pmap() function my_sum <- pmap(my_data, sum)  print(my_sum)
```

```         
[[1]] [1] 12  [[2]] [1] 15  [[3]] [1] 18
```

# **reduce()**

reduce() function produces a final output value by sequentially processing the elements in a given list, vector or data frame using a given function. This function reduces the use of loops, especially in large datasets, making the code more readable and performance.

The arguments of the reduce() function are:

-   .f: The function that will perform the operations.

-   .init: Initial value to use before starting the first operation. By default it is NULL and the operation starts with the first element.

-   .x: The list, vector or data frame to be processed.

An example of the reduce() function is as follows:

```         
# finding the sum of the values in the Sepal.Length column total_sepal_length <- reduce(iris$Sepal.Length, `+`) print(total_sepal_length)
```

```         
[1] 876.5
```

# **accumulate()**

accumulate() function sequentially processes the elements in a given list, vector or data frame, returning the result of each step as a vector. This function is similar to reduce(), but also keeps the intermediate results of the operations.

The arguments to accumulate() are:

-   .f: The function that will perform the operations.

-   .init: The initial value to use before starting the first operation. By default it is NULL and the operation starts with the first element.

-   .x: The list, vector or data frame to be processed.

An example of accumulate() function is as follows:

```         
# finding the sum by accumulating the values in the Sepal.Length column acc_sepal_length <- accumulate(iris$Sepal.Length, `+`) print(acc_sepal_length)
```

```         
  [1]   5.1  10.0  14.7  19.3  24.3  29.7  34.3  39.3  43.7  48.6  54.0  58.8  63.6  67.9  73.7  79.4  84.8  89.9  95.6 100.7 106.1 111.2 115.8 120.9  [25] 125.7 130.7 135.7 140.9 146.1 150.8 155.6 161.0 166.2 171.7 176.6 181.6 187.1 192.0 196.4 201.5 206.5 211.0 215.4 220.4 225.5 230.3 235.4 240.0  [49] 245.3 250.3 257.3 263.7 270.6 276.1 282.6 288.3 294.6 299.5 306.1 311.3 316.3 322.2 328.2 334.3 339.9 346.6 352.2 358.0 364.2 369.8 375.7 381.8  [73] 388.1 394.2 400.6 407.2 414.0 420.7 426.7 432.4 437.9 443.4 449.2 455.2 460.6 466.6 473.3 479.6 485.2 490.7 496.2 502.3 508.1 513.1 518.7 524.4  [97] 530.1 536.3 541.4 547.1 553.4 559.2 566.3 572.6 579.1 586.7 591.6 598.9 605.6 612.8 619.3 625.7 632.5 638.2 644.0 650.4 656.9 664.6 672.3 678.3 [121] 685.2 690.8 698.5 704.8 711.5 718.7 724.9 731.0 737.4 744.6 752.0 759.9 766.3 772.6 778.7 786.4 792.7 799.1 805.1 812.0 818.7 825.6 831.4 838.2 [145] 844.9 851.6 857.9 864.4 870.6 876.5
```

# **transpose()**

transpose() is a function used to convert columns of data frames into rows. This function reverses the pivot operation used in data frames.

Arguments of the function:

-   x: The data frame to transpose.

-   ...: Other arguments. Optional.

Example usage:

```         
# subseting first two observations of iris data set iris_subset <- iris[1:3,]  # transposing iris_subset  transposed_iris_subset <- transpose(iris_subset)  transposed_iris_subset
```

```         
[[1]] [[1]]$Sepal.Length [1] 5.1  [[1]]$Sepal.Width [1] 3.5  [[1]]$Petal.Length [1] 1.4  [[1]]$Petal.Width [1] 0.2  [[1]]$Species [1] 1   [[2]] [[2]]$Sepal.Length [1] 4.9  [[2]]$Sepal.Width [1] 3  [[2]]$Petal.Length [1] 1.4  [[2]]$Petal.Width [1] 0.2  [[2]]$Species [1] 1   [[3]] [[3]]$Sepal.Length [1] 4.7  [[3]]$Sepal.Width [1] 3.2  [[3]]$Petal.Length [1] 1.3  [[3]]$Petal.Width [1] 0.2  [[3]]$Species [1] 1
```

The original iris_subset:

```         
iris_subset
```

```         
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species 1          5.1         3.5          1.4         0.2  setosa 2          4.9         3.0          1.4         0.2  setosa 3          4.7         3.2          1.3         0.2  setosa
```

I studied the book [R for Data Science](https://r4ds.had.co.nz/) to write this article. You can check [Posit Cloud](https://posit.cloud/learn/primers/5) to practice the functions in this article.

That was the end of this post. Just like always:

\"In case I don\'t see ya, good afternoon, good evening, and good night!\"
