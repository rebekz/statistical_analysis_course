# Chi Square, Fisher Exact, McNemar Test
---

### Importing data
```
cars_survey <- read.delim(file = "http://www.statsci.org/data/oz/carprefs.txt")
```
### Chi Square
```
Description

chisq.test performs chi-squared contingency table tests and goodness-of-fit tests.

Usage

chisq.test(x, y = NULL, correct = TRUE,
           p = rep(1/length(x), length(x)), rescale.p = FALSE,
           simulate.p.value = FALSE, B = 2000)
```
The ```chisq.test()``` is used for chi square Test

```
> chisq.test(table(cars_survey$Sex, cars_survey$Reason))

	Pearson's Chi-squared test

data:  table(cars_survey$Sex, cars_survey$Reason)
X-squared = 24.034, df = 5, p-value = 0.0002139
```
### Fisher Exact test
```
Description

Performs Fisher's exact test for testing the null of independence of rows and columns in a contingency table with fixed marginals.

Usage

fisher.test(x, y = NULL, workspace = 200000, hybrid = FALSE,
            control = list(), or = 1, alternative = "two.sided",
            conf.int = TRUE, conf.level = 0.95,
            simulate.p.value = FALSE, B = 2000)
```
The ```fisher.test()``` is used for fisher test

```
> table_safety <- table(cars_survey$Kids6, cars_survey$Safety)
> fisher.test(table_safety)

	Fisher's Exact Test for Count Data

data:  table_safety
p-value = 0.7506
alternative hypothesis: two.sided
```
### McNemar Test
```
Description

Performs McNemar's chi-squared test for symmetry of rows and columns in a two-dimensional contingency table.

Usage

mcnemar.test(x, y = NULL, correct = TRUE)
```
The ```mcnemar.test()``` is used for McNemar Test

```
data <- matrix(c(6, 2, 8, 4), ncol=2, byrow=T)
mcnemar.test(data)

McNemar's Chi-squared test with continuity correction

data:  data 
McNemar's chi-squared = 2.5, df = 1, p-value = 0.1138
```