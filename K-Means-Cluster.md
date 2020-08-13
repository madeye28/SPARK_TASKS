TASK 3 K-Means Cluster
================

# Objective

  - So the objective of cluster or group datas which are similar in
    nature using K-Means cluster Algorithm .This Clustering comes under
    Uusuperwised Machine learning Models.

# Loading Dataset

  - We will be usign *iris* dataset, which is an in build dataset in R
    language. We will have a look at it column names and sampel of top 5
    entries.

<!-- end list -->

``` r
names(iris)
```

    ## [1] "Sepal.Length" "Sepal.Width"  "Petal.Length" "Petal.Width"  "Species"

``` r
head(iris)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.1         3.5          1.4         0.2  setosa
    ## 2          4.9         3.0          1.4         0.2  setosa
    ## 3          4.7         3.2          1.3         0.2  setosa
    ## 4          4.6         3.1          1.5         0.2  setosa
    ## 5          5.0         3.6          1.4         0.2  setosa
    ## 6          5.4         3.9          1.7         0.4  setosa

# Loading Necesasry Library

``` r
library(Amelia)
library(factoextra)
library(NbClust)
require(cluster)
library(tidyverse)
```

# Check for Missing value.

``` r
missmap(iris)
```

![](K-Means-Cluster_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

  - We can see that there is no missing data. so we can proceed furture.

# Removing the dependent variable from the dataset.

  - since our iris dataset consist of the dependent variable (Species),
    it should be removed before creating out cluster model.

<!-- end list -->

``` r
df <- iris[,-5]
```

  - now with our independent variable removed, we will have to decide
    the number of clusted, for our dataset.

  - SO inoreder to find the optimum Cluster value there are various
    methords we are using the classic *Elbow Methord*

<!-- end list -->

``` r
fviz_nbclust(df, kmeans, method = "wss") +
  geom_vline(xintercept = 3, linetype = 2)+
  labs(subtitle = "Elbow method")
```

![](K-Means-Cluster_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

  - From the above Graph we can clearly see that, number of clusters
    should be 3. where which the average within sum of squares are
    starting to reduce.

*Number of Clusters = 3*

# Model Building

  - We will be creating a K-Meand Cluster algorithm wiht out *iris*
    dataset.

<!-- end list -->

``` r
k_means <- kmeans(df, 3, nstart = 25)
```

  - So We have created a model with 3 cluster, and now we want to see
    the number of entries comes into each cluster

<!-- end list -->

``` r
clust <- k_means$cluster
as.data.frame(clust) %>% 
  group_by(clust) %>%
  count()
```

    ## # A tibble: 3 x 2
    ## # Groups:   clust [3]
    ##   clust     n
    ##   <int> <int>
    ## 1     1    50
    ## 2     2    62
    ## 3     3    38

We can see

  - 62 entries are clustered into cluster 1
  - 50 entries are clustered into cluster 2
  - 38 entries are clustered into cluster 3

# Visual Representation.

  - Now we will have a visual representation of each cluster

<!-- end list -->

``` r
fviz_cluster(k_means, df, geom = "point")
```

![](K-Means-Cluster_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

# Thank You
