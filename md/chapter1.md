# Descriptive Analysis
---

#### Importing data
```
usedcars <- read.csv("https://github.com/rebekz/statistical_analysis_course/blob/master/data/usedcars.csv")
```

#### Exploring the structure of data
The ```str()``` function used for displaying the structure of a data. For example:
``` 
> str(usedcars) 
'data.frame':	150 obs. of 6 variables:
 $ year        : int  2011 2011 2011 2011 ...
 $ model       : chr  "SEL" "SEL" "SEL" "SEL" ...
 $ price       : int  21992 20995 19995 17809 ...
 $ mileage     : int  7413 10926 7351 11613 ...
 $ color       : chr  "Yellow" "Gray" "Silver" "Gray" ...
 $ transmission: chr  "AUTO" "AUTO" "AUTO" "AUTO" ...
```
#### Exploring numeric variables
The ```summary()``` function used for displaying several common numerical statistic features
```
> summary(usedcars[c("price", "mileage")])
     price           mileage     
 Min.   : 3800   Min.   :  4867  
 1st Qu.:10995   1st Qu.: 27200  
 Median :13592   Median : 36385  
 Mean   :12962   Mean   : 44261  
 3rd Qu.:14904   3rd Qu.: 55125  
 Max.   :21992   Max.   :151479
```
#### Measuring the central tendency – mean and median
```mean()``` is used for calculate the mean for a vector of numbers:
```
mean(usedcars$price)
[1] 12961.93333
```
```median()``` is used for calculate the median for a vector of numbers:
```
median(usedcars$price)
[1] 13591.5
```
#### Measuring spread - quartiles and five-number summary
```range()``` function return both the minimum and maximum value
```
> range(usedcars$price)
[1]  3800 21992
> diff(range(usedcars$price))
[1] 18192
```
The difference between Q1 and Q3 is known as the interquartile range (IQR), can be calculated with the ```IQR()``` function:
```
> IQR(usedcars$price)
[1] 3909.5
```
The ```quantile() ``` function provides tool for identifying quantiles. By default it returns the five-number summary
```
> quantile(usedcars$price)
     0%     25%     50%     75%    100% 
 3800.0 10995.0 13591.5 14904.5 21992.0
```

#### Visualizing numeric variables - boxplots
A common visualization of the five-number summary is a boxplot or box-and-whiskers plot
```
> boxplot(usedcars$price, main="Boxplot of Used Car Prices",ylab="Price ($)")
```
#### Visualizing numeric variables - histograms
A histogram is another way to graphically depict the spread of a numeric variables based on predefined number of portions (bins) that act as containers for values.
```
> hist(usedcars$price, main = "Histogram of Used Car Prices", xlab = "Price ($)")
```
#### Measuring spread – variance and standard deviation
To obtain the variance and standard deviation in R, the ```var()``` and ```sd()``` functions can be used
```
> var(usedcars$price)
[1] 9749892
> sd(usedcars$price)
[1] 3122.482
```
When interpreting the variance, larger numbers indicate that the data are spread more widely around the mean. The standard deviation indicates, on average, how much each value differs from the mean.
#### Exploring categorical variables
A table that presents a single categorical variable is known as a ***one-way table***. the ```table()``` function can be used to generate one-way tables:
```
> table(usedcars$model)
 SE SEL SES 
 78  23  49
> prop.table(table(usedcars$model)) * 100
     SE         SEL         SES 
52.00000000 15.33333333 32.66666667 
 ```
#### Visualizing relationships - scatterplots
A scatterplot is a diagram that visualizes a bivariate relationship

```
> plot(x = usedcars$mileage, y = usedcars$price,
     main = "Scatterplot of Price vs. Mileage",
     xlab = "Used Car Odometer (mi.)",
     ylab = "Used Car Price ($)")
```
#### Examining relationships - two way table

```
table(usedcars$model, usedcars$conservative)
        FALSE TRUE
  SE     27   51
  SEL     7   16
  SES    17   32
```

