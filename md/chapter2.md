# Correlation and Regression
---

#### Importing data
```
usedcars <- read.csv("https://raw.githubusercontent.com/rebekz/statistical_analysis_course/master/data/usedcars.csv")
insurance <- read.csv("https://raw.githubusercontent.com/rebekz/Machine-Learning-with-R-datasets/master/insurance.csv")
```

#### Correlation
The ```cor()``` function used for displaying correlation price and mileage:
```
cov(usedcars$mileage, usedcars$price) / (sd(usedcars$mileage) * sd(usedcars$price))
[1] -0.8061494

cor(usedcars$mileage, usedcars$price)
[1] -0.8061494
```
We can do correlation multiple variable by creating correlation matrix
```
cor(ins[c("age", "bmi", "children", "charges")])
               age       bmi   children    charges
age      1.0000000 0.1092719 0.04246900 0.29900819
bmi      0.1092719 1.0000000 0.01275890 0.19834097
children 0.0424690 0.0127589 1.00000000 0.06799823
charges  0.2990082 0.1983410 0.06799823 1.00000000
```
To check if the correlation is statistical significant, we can used ```cor.test()``` function
```
cor.test(usedcars$mileage, usedcars$price)

	Pearson's product-moment correlation

data:  usedcars$mileage and usedcars$price
t = -16.574, df = 148, p-value < 2.2e-16
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 -0.8558408 -0.7417133
sample estimates:
       cor 
-0.8061494 
```
#### Univariate Linear Regression
```lm()``` is used for creating linear model of the data
```
(price_mil_model <- lm(price ~ mileage, data = usedcars))
Call:
lm(formula = price ~ mileage, data = usedcars)

Coefficients:
(Intercept)      mileage  
  1.709e+04   -9.329e-02  
```
```price``` is the dependent (response) variable and the ```mileage``` is the independent (predictor) variable. In the univariate linear regression, we only used 1 independent variable.
To evaluate our model or find detailed information about that model we can used ```summary()```
```
summary(price_mil_model)
Call:
lm(formula = price ~ mileage, data = usedcars)

Residuals:
    Min      1Q  Median      3Q     Max 
-5830.9 -1113.7    40.5   992.6  7782.4 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)    
(Intercept)  1.709e+04  2.915e+02   58.63   <2e-16 ***
mileage     -9.329e-02  5.629e-03  -16.57   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 1854 on 148 degrees of freedom
Multiple R-squared:  0.6499,	Adjusted R-squared:  0.6475 
F-statistic: 274.7 on 1 and 148 DF,  p-value: < 2.2e-16
```
#### Multivariate Linear Regression
To do multivariate linear regression we only add more than 1 independent variable in the ```lm()``` function
```
(ins_model <- lm(charges ~ age + sex + bmi + children + smoker + region, data = insurance))
Call:
lm(formula = charges ~ age + sex + bmi + children + smoker + 
    region, data = insurance)

Coefficients:
    (Intercept)              age          sexmale              bmi         children  
       -11938.5            256.9           -131.3            339.2            475.5  
      smokeryes  regionnorthwest  regionsoutheast  regionsouthwest  
        23848.5           -353.0          -1035.0           -960.1 
```
or we just add ```.``` it means add all variables except to dependent variable that we choose.
```
Call:
lm(formula = charges ~ ., data = insurance)

Coefficients:
    (Intercept)              age          sexmale              bmi         children  
       -11938.5            256.9           -131.3            339.2            475.5  
      smokeryes  regionnorthwest  regionsoutheast  regionsouthwest  
        23848.5           -353.0          -1035.0           -960.1  
```
To show detailed information of our model then ```summary()``` used
```
> summary(insurance_model)

Call:
lm(formula = charges ~ ., data = insurance)

Residuals:
     Min       1Q   Median       3Q      Max 
-11304.9  -2848.1   -982.1   1393.9  29992.8 

Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
(Intercept)     -11938.5      987.8 -12.086  < 2e-16 ***
age                256.9       11.9  21.587  < 2e-16 ***
sexmale           -131.3      332.9  -0.394 0.693348    
bmi                339.2       28.6  11.860  < 2e-16 ***
children           475.5      137.8   3.451 0.000577 ***
smokeryes        23848.5      413.1  57.723  < 2e-16 ***
regionnorthwest   -353.0      476.3  -0.741 0.458769    
regionsoutheast  -1035.0      478.7  -2.162 0.030782 *  
regionsouthwest   -960.0      477.9  -2.009 0.044765 *  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 6062 on 1329 degrees of freedom
Multiple R-squared:  0.7509,	Adjusted R-squared:  0.7494 
F-statistic: 500.8 on 8 and 1329 DF,  p-value: < 2.2e-16
```
#### Adding Interaction Effects
We can combined certain features to add impact on dependent variable. When two features have a combined effect, this known as an Interaction. The ```*``` operator is shorthand that instructs R to model interaction.
```
ins_model <- lm(charges ~ age + children + bmi + sex + bmi30*smoker + region, data = insurance)
summary(ins_model)

Call:
lm(formula = charges ~ age + children + bmi + sex + bmi30 * smoker + 
    region, data = insurance)

Residuals:
     Min       1Q   Median       3Q      Max 
-18234.3  -1826.1  -1251.6   -447.5  24803.9 

Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
(Intercept)     -4745.546    959.685  -4.945 8.59e-07 ***
age               263.242      8.805  29.897  < 2e-16 ***
children          520.402    101.958   5.104 3.81e-07 ***
bmi               115.035     34.560   3.329 0.000897 ***
sexmale          -491.179    246.563  -1.992 0.046565 *  
bmi30            -865.057    425.775  -2.032 0.042381 *  
smokeryes       13402.363    443.910  30.192  < 2e-16 ***
regionnorthwest  -266.836    352.410  -0.757 0.449079    
regionsoutheast  -825.000    354.800  -2.325 0.020209 *  
regionsouthwest -1224.315    353.684  -3.462 0.000554 ***
bmi30:smokeryes 19794.852    610.092  32.446  < 2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 4485 on 1327 degrees of freedom
Multiple R-squared:  0.8639,	Adjusted R-squared:  0.8628 
F-statistic: 842.1 on 10 and 1327 DF,  p-value: < 2.2e-16
```