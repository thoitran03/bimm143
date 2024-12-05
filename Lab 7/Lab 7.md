# Lab 7 Machine Learning 1
Thoi Tran (A17035545)

Today we are going to laern how to apply different machine learning
methods begining with clustering:

The goal hear is to find group/clusters in your input data.

First I will make up some data with clear groups. For this I will use
the `rnorm()` function.

``` r
rnorm(10)
```

     [1]  1.3031350  0.1829918 -2.2356709  0.4485581  0.8899974 -0.1519381
     [7]  1.1117487 -0.9072862  0.8753756  0.1561582

``` r
hist(rnorm(10000, mean = 3))
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-2-1.png)

``` r
x1 <- c(rnorm(10000, mean = 3),
       rnorm(10000, mean = -3))
hist(x1)
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-3-1.png)

``` r
x <- c(rnorm(30, mean = 3),
       rnorm(30, mean = -3))
x
```

     [1]  4.2278112  2.7447312  3.3179575  3.2702071  2.2408141  2.3323495
     [7]  3.9410802  4.7427029  3.5410927  2.5980870  2.5451975  3.8022653
    [13]  1.8353653  3.2898598  1.6251216  3.8927142  2.8555645  4.0633307
    [19]  1.0736831  3.0411718  3.0974292  4.3619650  3.6899850  2.9087505
    [25]  2.7872532  2.3303398  2.3939669  3.3822485  1.4312774  2.7862029
    [31] -2.5880280 -5.1543334 -3.0894379 -2.8919705 -3.4928441 -2.8598825
    [37] -4.4318687 -1.9551301 -2.9439594 -0.6628304 -3.1990259 -2.7491876
    [43] -1.6402066 -0.9899786 -1.1983476 -3.0445173 -2.9107896 -2.7620322
    [49] -3.8030695 -3.2061630 -2.3324431 -2.4145753 -2.9182262 -3.3523836
    [55] -3.8248165 -1.3410387 -2.4061099 -2.7915733 -3.2075886 -2.8507597

``` r
y <- rev(x)
y
```

     [1] -2.8507597 -3.2075886 -2.7915733 -2.4061099 -1.3410387 -3.8248165
     [7] -3.3523836 -2.9182262 -2.4145753 -2.3324431 -3.2061630 -3.8030695
    [13] -2.7620322 -2.9107896 -3.0445173 -1.1983476 -0.9899786 -1.6402066
    [19] -2.7491876 -3.1990259 -0.6628304 -2.9439594 -1.9551301 -4.4318687
    [25] -2.8598825 -3.4928441 -2.8919705 -3.0894379 -5.1543334 -2.5880280
    [31]  2.7862029  1.4312774  3.3822485  2.3939669  2.3303398  2.7872532
    [37]  2.9087505  3.6899850  4.3619650  3.0974292  3.0411718  1.0736831
    [43]  4.0633307  2.8555645  3.8927142  1.6251216  3.2898598  1.8353653
    [49]  3.8022653  2.5451975  2.5980870  3.5410927  4.7427029  3.9410802
    [55]  2.3323495  2.2408141  3.2702071  3.3179575  2.7447312  4.2278112

``` r
z <- cbind(x, y)
head(z)
```

                x         y
    [1,] 4.227811 -2.850760
    [2,] 2.744731 -3.207589
    [3,] 3.317958 -2.791573
    [4,] 3.270207 -2.406110
    [5,] 2.240814 -1.341039
    [6,] 2.332350 -3.824816

``` r
plot(z)
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-7-1.png)

## K_means Clustering

Use `kmeans()` funciton setting k to 2 and nstart = 10

Inspect/print the results

> Q. How many points are in each cluster?

``` r
km <- kmeans(z, centers = 2)
km
```

    K-means clustering with 2 clusters of sizes 30, 30

    Cluster means:
              x         y
    1 -2.767104  3.005018
    2  3.005018 -2.767104

    Clustering vector:
     [1] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1
    [39] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

    Within cluster sum of squares by cluster:
    [1] 49.72793 49.72793
     (between_SS / total_SS =  91.0 %)

    Available components:

    [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    [6] "betweenss"    "size"         "iter"         "ifault"      

Results in kmeans object `km`.

``` r
attributes(km)
```

    $names
    [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    [6] "betweenss"    "size"         "iter"         "ifault"      

    $class
    [1] "kmeans"

> Q. What component of your result object details? - Cluster size? -
> Cluster assignment/membership? - Cluster center?

Cluster size?

``` r
km$size
```

    [1] 30 30

Cluster assignment/membership?

``` r
km$cluster
```

     [1] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1
    [39] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

Cluster center?

``` r
km$centers
```

              x         y
    1 -2.767104  3.005018
    2  3.005018 -2.767104

> Q. Plot z colored by the kmeans cluster assignment and add cluster
> centers as blue points.

R will recycle shorter color vectore to be the same length as the longer
(number of data points) in z.

``` r
plot(z, col = c("red", "blue"))
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-13-1.png)

``` r
plot(z, col = km$cluster)
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-14-1.png)

We can use the `points()` funciton to add new points to an exsiting
plot, like the cluster centers.

``` r
plot(z, col = km$cluster)
points(km$centers, col = "blue", pch = 15, cex = 3)
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-15-1.png)

> Q. Can you run kmeans and ask for 4 clusters and plot the results?

``` r
km_1 <- kmeans(z, centers = 4)
```

``` r
plot(z, col = km_1$cluster)
points(km_1$centers, col = "purple", pch = 15)
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-17-1.png)

## Hierarchical Clustering

Let’s take our same data `z` and see how `hclust` works.

First we need a distance matrix of our data to be clustered

``` r
d <- dist(z)
hc <- hclust(d)
hc
```


    Call:
    hclust(d = d)

    Cluster method   : complete 
    Distance         : euclidean 
    Number of objects: 60 

``` r
plot(hc)
abline(h = 8, col = "red")
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-19-1.png)

I can get my cluster membership vector by “cutting the tree” with the
`cutree()` function.

``` r
grps <- cutree(hc, h = 8)
grps
```

     [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

> Q. Can you plot z colored by our hclust results?

``` r
plot(z, col = grps)
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-21-1.png)

## PCA of UK food Data

Read data from the UK on food consumption in different parts of the UK.

``` r
url <- "https://tinyurl.com/UK-foods"
x <- read.csv(url, row.names = 1)
head(x)
```

                   England Wales Scotland N.Ireland
    Cheese             105   103      103        66
    Carcass_meat       245   227      242       267
    Other_meat         685   803      750       586
    Fish               147   160      122        93
    Fats_and_oils      193   235      184       209
    Sugars             156   175      147       139

``` r
barplot(as.matrix(x), beside=T, col=rainbow(nrow(x)))
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-23-1.png)

``` r
barplot(as.matrix(x), beside=F, col=rainbow(nrow(x)))
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-24-1.png)

A so-called “Pairs” plot can be usefull for small datasets like this.

``` r
pairs(x, col=rainbow(10), pch=16)
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-25-1.png)

It’s hard to see structure and trends in even this small dataset. How
will we ever do this when we have big datasets with 1,000s or 10s of
thousands of things we are measuring.

### PCA to the rescue

Let’s see how PCA deals with this dataset. So the main funciton in base
R to do PCA is called `prcomp()`.

``` r
pca <- prcomp(t(x))
summary(pca)
```

    Importance of components:
                                PC1      PC2      PC3       PC4
    Standard deviation     324.1502 212.7478 73.87622 3.176e-14
    Proportion of Variance   0.6744   0.2905  0.03503 0.000e+00
    Cumulative Proportion    0.6744   0.9650  1.00000 1.000e+00

Let’s see what is inside this `pca` objecct that we created from running
`prcomp()`.

``` r
attributes(pca)
```

    $names
    [1] "sdev"     "rotation" "center"   "scale"    "x"       

    $class
    [1] "prcomp"

``` r
pca$x
```

                     PC1         PC2        PC3           PC4
    England   -144.99315   -2.532999 105.768945 -4.894696e-14
    Wales     -240.52915 -224.646925 -56.475555  5.700024e-13
    Scotland   -91.86934  286.081786 -44.415495 -7.460785e-13
    N.Ireland  477.39164  -58.901862  -4.877895  2.321303e-13

``` r
plot(pca$x[,1],pca$x[,2], col = c("black", "red", "blue", "darkgreen"),
     pch = 16, xlab = "PC1 (67.4%)", ylab = "PC2 (29.0%")
text(pca$x[,1], pca$x[,2], colnames(x), col = c("black", "red", "blue", "darkgreen"))
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-29-1.png)

### Digging deeper (variable loadings)

``` r
par(mar=c(10, 3, 0.35, 0))
barplot( pca$rotation[,1], las=2 )
```

![](Lab-7_files/figure-commonmark/unnamed-chunk-30-1.png)
