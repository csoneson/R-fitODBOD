R-fitODBOD
================

[![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version-last-release/fitODBOD)](https://cran.r-project.org/package=fitODBOD)
[![packageversion](https://img.shields.io/badge/Package%20version-1.4.0-orange.svg?style=flat-square)](commits/master)
[![Rdoc](http://www.rdocumentation.org/badges/version/fitODBOD)](http://www.rdocumentation.org/packages/fitODBOD)

![downloads](http://cranlogs.r-pkg.org/badges/grand-total/fitODBOD)
![downloads](https://cranlogs.r-pkg.org/badges/fitODBOD)
![downloads](http://cranlogs.r-pkg.org/badges/last-week/fitODBOD)

[![Licence](https://img.shields.io/badge/licence-GPL--2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html)
[![GitHub
license](https://img.shields.io/github/license/Amalan-ConStat/R-fitODBOD.svg?style=popout)](https://github.com/Amalan-ConStat/R-fitODBOD/blob/master/LICENSE)

[![Project Status: Active - The project has reached a stable, usable
state and is being actively
developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![GitHub
issues](https://img.shields.io/github/issues/Amalan-ConStat/R-fitODBOD.svg?style=popout)](https://github.com/Amalan-ConStat/R-fitODBOD/issues)

[![rpackages.io
rank](http://www.rpackages.io/badge/fitODBOD.svg)](http://www.rpackages.io/package/fitODBOD)

[![Travis build
status](https://travis-ci.org/Amalan-ConStat/R-fitODBOD.svg?branch=master)](https://travis-ci.org/Amalan-ConStat/R-fitODBOD)
[![AppVeyor build
status](https://ci.appveyor.com/api/projects/status/github/Amalan-ConStat/R-fitODBOD?branch=master&svg=true)](https://ci.appveyor.com/project/Amalan-ConStat/R-fitODBOD)
[![Codecov test
coverage](https://codecov.io/gh/Amalan-ConStat/R-fitODBOD/branch/master/graph/badge.svg)](https://codecov.io/gh/Amalan-ConStat/R-fitODBOD?branch=master)

[![status](http://joss.theoj.org/papers/388fc2f4d7c1e0ae83cf0de13ac038a4/status.svg)](http://joss.theoj.org/papers/388fc2f4d7c1e0ae83cf0de13ac038a4)
[![cran
checks](https://cranchecks.info/badges/summary/fitODBOD)](https://cranchecks.info/pkgs/fitODBOD)

# fitODBOD <img src="man/figures/logo.png" align="right" alt="" width="150" />

## How to engage with “fitODBOD” the first time ?

``` r
## Installing the package from GitHub
devtools::install_github("Amalan-ConStat/R-fitODBOD")

## Installing the package from CRAN
install.packages("fitODBOD")
```

## Key Phrases

  - BOD (Binomial Outcome Data)
  - Over Dispersion
  - Under Dispersion
  - BMD (Binomial Mixture Distributions)
  - ABD (Alternate Binomial Distributions)
  - PMF (Probability Mass Function)
  - CPMF (Cumulative Probability Mass Function)

## What does “fitODBOD” ?

You can understand BMD & ABD with PMF & CPMF. Further, BOD can be
modeled using these Distributions

## Distributions

| Alternate Binomial Distributions                | Binomial Mixture Distributions                                   |
| :---------------------------------------------- | :--------------------------------------------------------------- |
| 1.Additive Binomial Distribution                | 1.Uniform Binomial Distribution                                  |
| 2.Beta-Correlated Binomial Distribution         | 2.Triangular Binomial Distribution                               |
| 3.COM Poisson Binomial Distribution             | 3.Beta-Binomial Distribution                                     |
| 4.Correlated Binomial Distribution              | 4.Kumaraswamy Binomial Distribution                              |
| 5.Multiplicative Binomial Distribution          | 5.Gaussian Hypergeometric Generalized Beta-Binomial Distribution |
| 6.Lovinson Multiplicative Binomial Distribution | 6.McDonald Generalized Beta-Binomial Distribution                |
|                                                 | 7.Gamma Binomial Distribution                                    |
|                                                 | 8.Grassia II Binomial Distribution                               |

## Modelling

To demonstrate the process the Alcohol Consumption Data, which is the
most commonly used dataset by the researchers to explain Over-dispersion
will be taken {lemmens1988}. In this dataset, the number of alcohol
consumption days in two reference weeks is separately self-reported by a
randomly selected sample of \(399\) respondents from the Netherlands in
\(1983\). Here, the number of days a given individual consumes alcohol
out of seven days a week can be treated as a Binomial variable. The
collection of all such variables from all respondents would be defined
as “Binomial Outcome Data”.

### Step 1

The Alcohol consumption data is already in the necessary format to apply
steps \(2\) to \(5\) and hence, step \(1\) can be avoided. The steps
\(2\) to \(5\) can be applied only if the dataset is in the form of a
frequency table as follows.

``` r
library("fitODBOD")   #Loading packages
# Hello, This is Amalan. For more details refer --> https://amalan-constat.github.io/R-fitODBOD/index.html
print(Alcohol_data)     #print the alcohol consumption data set
#   Days week1 week2
# 1    0    47    42
# 2    1    54    47
# 3    2    43    54
# 4    3    40    40
# 5    4    40    49
# 6    5    41    40
# 7    6    39    43
# 8    7    95    84
sum(Alcohol_data$week1) #No of respondents or N
# [1] 399
Alcohol_data$Days       #Binomial random variables or x 
# [1] 0 1 2 3 4 5 6 7
```

Suppose your dataset is not a frequency table as shown in the following
dataset called `datapoints`. Then the function `BODextract` can be used
to prepare the appropriate format as follows.

``` r
datapoints <- sample(0:7, 340, replace = TRUE) #creating a set of raw BOD 
head(datapoints)  #first few observations of datapoints dataset
# [1] 7 1 7 3 6 7
    
#extracting and printing BOD in a usable way for the package
new_data <- BODextract(datapoints)
matrix(c(new_data$RV, new_data$Freq), ncol=2, byrow = FALSE)
#      [,1] [,2]
# [1,]    0   34
# [2,]    1   39
# [3,]    2   37
# [4,]    3   41
# [5,]    4   42
# [6,]    5   45
# [7,]    6   50
# [8,]    7   52
```

### Step 2

As in the second step we test whether the Alcohol Consumption data
follows the Binomial distribution based on the hypothesis given below:

Null Hypothesis : The data follows Binomial Distribution.

Alternate Hypothesis : The data does not follow Binomial Distribution.

Alcohol Consumption data consists of frequency information for two weeks
but only the first week is considered for computation. By doing so the
researcher can verify if the results acquired from the functions are
similar to the results acquired from previous researchers work.

``` r
BinFreq<-fitBin(Alcohol_data$Days, Alcohol_data$week1)
# Warning in fitBin(Alcohol_data$Days, Alcohol_data$week1): Chi-squared
# approximation may be doubtful because expected frequency is less than 5
print(BinFreq)
# Call: 
# fitBin(x = Alcohol_data$Days, obs.freq = Alcohol_data$week1)
# 
# Chi-squared test for Binomial Distribution 
#   
#       Observed Frequency :  47 54 43 40 40 41 39 95 
#   
#       expected Frequency :  1.59 13.41 48.3 96.68 116.11 83.66 33.49 5.75 
#   
#       estimated probability value : 0.5456498 
#   
#       X-squared : 2911.434   ,df : 6   ,p-value : 0
```

Looking at the p-value it is clear that null hypothesis is rejected at
\(5\%\) significance level. This indicates that data doesn’t fit the
Binomial distribution. The reason for a Warning message is that one of
the expected frequencies in the results is less than five. Now we
compare the actual and the fitted Binomial variances.

``` r
#Actual variance of observed frequencies
var(rep(Alcohol_data$Days, times = Alcohol_data$week1))
# [1] 6.253788
#Calculated variance for frequencies of  fitted Binomial distribution 
var(rep(BinFreq$bin.ran.var, times = fitted(BinFreq)))
# [1] 1.696035
```

The variance of observed frequencies and the variance of fitted
frequencies are \(6.253788\) and \(1.696035\) respectively, which
indicates Over-dispersion.

### Step 3 and 4

Since the Over-dispersion exists in the data now it is necessary to fit
the Binomial Mixture distributions Triangular Binomial, Beta-Binomial,
Kumaraswamy Binomial, Gamma Binomial, Grassia II Binomial, GHGBB and
McGBB using the package, and select the best-fitted distribution using
Negative Log likelihood value, p-value and by comparing observed and
expected frequencies. Modelling these distributions are given in the
next sub-sections.

#### a) Triangular Binomial distribution.

The estimation of the mode parameter \(c\) can be done by using the
`EstMLETriBin` function, and then the estimated value has to be applied
to `fitTriBin` function to check whether the data fit the Triangular
Binomial distribution.

``` r
#estimating the mode
modeTB <- EstMLETriBin(Alcohol_data$Days, Alcohol_data$week1) 
coef(modeTB)  #printing the estimated mode
#  mode 
#  0.944444

#printing the Negative log likelihood value which is minimized
NegLLTriBin(Alcohol_data$Days, Alcohol_data$week1,modeTB$mode)
# [1] 880.6167
```

To fit the Triangular Binomial distribution for estimated mode parameter
the following hypothesis is used

Null Hypothesis :\&The data follows Triangular Binomial Distribution.

Alternate Hypothesis:& The data does not follow Triangular Binomial
Distribution.

``` r
#fitting the Triangular Binomial Distribution for the estimated mode value
fitTriBin(Alcohol_data$Days, Alcohol_data$week1, modeTB$mode)
# Call: 
# fitTriBin(x = Alcohol_data$Days, obs.freq = Alcohol_data$week1, 
#     mode = modeTB$mode)
# 
# Chi-squared test for Triangular Binomial Distribution 
#   
#       Observed Frequency :  47 54 43 40 40 41 39 95 
#   
#       expected Frequency :  11.74 23.47 35.21 46.94 58.66 70.2 79.57 73.21 
#   
#       estimated Mode value: 0.944444 
#   
#       X-squared : 193.6159   ,df : 6   ,p-value : 0 
#   
#       over dispersion : 0.2308269
```

Since the \(p-value\) is \(0\) which is less than \(0.05\) it is clear
that the null hypothesis is rejected, and the estimated Over-dispersion
is \(0.2308269\). Therefore, it is necessary to fit a better flexible
distribution than the Triangular Binomial distribution.

#### b) Beta-Binomial distribution.

#### c) Kumaraswamy Binomial distribution.

#### d) Gamma Binomial distribution.

#### e) Grassia II Binomial distribution.

#### f) GHGBB distribution.

#### g) McGBB distribution.

### Step 5

#### Thank You

[![Twitter](https://img.shields.io/twitter/url/https/github.com/Amalan-ConStat/R-fitODBOD.svg?style=social)](https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2FAmalan-ConStat%2FR-fitODBOD)

[![](https://img.shields.io/badge/LinkedIn-Amalan%20Mahendran-black.svg?style=flat)](https://www.linkedin.com/in/amalan-mahendran-72b86b37/)
[![](https://img.shields.io/badge/Research%20Gate-Amalan%20Mahendran-black.svg?style=flat)](https://www.researchgate.net/profile/Amalan_Mahendran)
