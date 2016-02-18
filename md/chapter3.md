# T-test and ANOVA
---

### Importing data
```
insurance <- read.csv("https://raw.githubusercontent.com/rebekz/Machine-Learning-with-R-datasets/master/insurance_with_bmi.csv")
drp_paired <- read.csv("https://raw.githubusercontent.com/rebekz/Machine-Learning-with-R-datasets/master/drp_paired.csv")
```
### T-test
The ```t.test()``` function used for T-test

```
Usage
t.test(x, ...)

## Default method:
t.test(x, y = NULL,
       alternative = c("two.sided", "less", "greater"),
       mu = 0, paired = FALSE, var.equal = FALSE,
       conf.level = 0.95, ...)

default of alternative = “two.sided”

```

#### One Sample

```
> t.test(insurance$charges, mu = 12000)

	One Sample t-test

data:  charges_male$charges
t = 3.9222, df = 675, p-value = 9.67e-05
alternative hypothesis: true mean is not equal to 12000
95 percent confidence interval:
 12977.20 14936.31
sample estimates:
mean of x 
 13956.75
```

```mu ``` is the the mean of current population

#### Two Independent Sample

```
> t.test(insurance$charges ~ insurance$sex)

	Welch Two Sample t-test

data:  insurance$charges by insurance$sex
t = -2.1009, df = 1313.4, p-value = 0.03584
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -2682.48932   -91.85535
sample estimates:
mean in group female   mean in group male 
            12569.58             13956.75 
```
#### Pre & Post 
```
> t.test(drp_paired$Treated, drp_paired$Control, paired = T)

Paired t-testdata:  
drp_paired$Treated and drp_paired$Control
t = 1.9568, df = 20, p-value = 0.06448
alternative hypothesis: true difference in means is not equal to 0
95 percent
confidence interval: -0.6349369 19.8730321
sample estimates:
mean of the differences                
9.619048

```
### Analysis of Variance (ANOVA)

```aov()``` is used for compute ANOVA. ```oneway.test()``` is used for oneway test.

#### One way Test

```
> oneway.test(weight ~ group, data = PlantGrowth) 
One-way analysis of means (not assuming equal variances) 

data: weight and group 
F = 5.181, num df = 2.000, denom df = 17.128, p-value = 0.01739 
```

#### Two way Test

```
> summary(aov(charges ~ bmi_type + smoker + bmi_type * smoker, data = insurance))

 Df Sum Sq Mean Sq F value Pr(>F) 
bmi_type 2 4.525e+09 2.263e+09 52.06 <2e-16 *** 
smoker 1 1.219e+11 1.219e+11 2804.21 <2e-16 *** bmi_type:smoker 2 1.178e+10 5.891e+09 135.54 <2e-16 *** Residuals 1332 5.789e+10 4.346e+07 
--- Signif. codes: 0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```

#### Tukey Honestly Significant Difference Test

```
> plant.aov <- aov(weight ~ group, data = PlantGrowth) 
> TukeyHSD(plant.aov) 
Tukey multiple comparisons of means 
95% family-wise confidence level 
Fit: aov(formula = weight ~ group, data = PlantGrowth) 

$group diff lwr upr p adj 
trt1-ctrl -0.371 -1.0622161 0.3202161 0.3908711
trt2-ctrl 0.494 -0.1972161 1.1852161 0.1979960 
trt2-trt1 0.865 0.1737839 1.5562161 0.0120064
```

#### Homegeneity of Variance Test

```
> bartlett.test(PlantGrowth$weight ~ PlantGrowth$group) 
Bartlett test of homogeneity of variances 
data: PlantGrowth$weight by PlantGrowth$group Bartlett's K-squared = 2.8786, df = 2, p-value = 0.2371
```