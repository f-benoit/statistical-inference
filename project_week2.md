---
title: "Statistic Inference Week 2"
author: "Benoit Fedit"
date: "29 June 2017"
---
## Week 2 Assignement statistical-inference 
#### Provided by COursera (johns hopkins university)


#### Question 1
What is the variance of the distribution of the average an IID draw of n observations from
a population with mean ?? and variance ??2.

#### Answer:
??2/n


#### Question 2:
Suppose that diastolic blood pressures (DBPs) for men aged 35-44 are normally distributed with 
a mean of 80 (mm Hg) and a standard deviation of 10. About what is the probability that a random
35-44 year old has a DBP less than 70?

#### Answer:

```r
pnorm(70, mean = 80, sd = 10, lower.tail = TRUE, log.p = FALSE)
```

```
## [1] 0.1586553
```

```r
#If lower.tail is set to True then pnorm returns the integral of -infinite to q of the probalityt density function
#If lower.tail is set to False then pnorm returns the integral of q to +infinite of the probalityt density function
#Hence 1-pnorm (...lower.tail=False) should return same result as above
```

#### Question 3:
Brain volume for adult women is normally distributed with a mean of about 1,100 cc for women with
a standard deviation of 75 cc. What brain volume represents the 95th percentile?

#### Answer:
qnorm gives the Z-score of percentile th of the normal distribution


```r
qnorm(0.95, mean = 1100, sd = 75, lower.tail = TRUE, log.p = FALSE)
```

```
## [1] 1223.364
```


#### Question 4:
Refer to the previous question. Brain volume for adult women is about 1,100 cc for women with a 
standard deviation of 75 cc. Consider the sample mean of 100 random adult women from this population.
What is the 95th percentile of the distribution of that sample mean?

#### Answer
Remember that std error is givent by SD/sqr*N

```r
SE<-75/sqrt(100)
qnorm(0.95, mean = 1100, sd = SE, lower.tail = TRUE, log.p = FALSE)
```

```
## [1] 1112.336
```

#### Question 5:
You flip a fair coin 5 times, about what's the probability of getting 4 or 5 heads?

#### Answer

```r
n<-5
p<-0.5
sum(dbinom(4:5, size=n, prob=p))
```

```
## [1] 0.1875
```

Or alternatively we can do the math
Binomial distribution formula: 
C(n,x) * p^x * q^(n-x) = (n!/(x! (n-x)!)) * p^x * q^(n-x)


```r
n<-5   #number of time we flip the fair coin
p<-0.5 #prob success
q<-0.5 #prob failure
probX<-0 #result
for (x in 5:4) {  # probability of getting 5 or 4
  p_powerX<-p^x
  q_powerN_minusX<-q^(n-x)
  probX<-probX + factorial(n)/(factorial(n-x)*factorial(x))*p_powerX*q_powerN_minusX  
}
probX
```

```
## [1] 0.1875
```

#### Question 6:
The respiratory disturbance index (RDI), a measure of sleep disturbance, for a specific population has
a mean of 15 (sleep events per hour) and a standard deviation of 10. They are not normally distributed.
Give your best estimate of the probability that a sample mean RDI of 100 people is between 14 and 16 events per hour?

#### Answer

```r
mu<-15
SD<-10
n<-100
SE<-SD/sqrt(n)
SE
```

```
## [1] 1
```
The range 14 to 16 is exactly equal to 1 standard deviation away from the mean hence we know 
from the empirical rule that about 68% of values drawn from a normal distribution are within 
one standard deviation ?? away from the mean.


```r
#We can use the pnorm function
#We need first to exclude all the data that are more than one SD from the mean
#Let's find the lower and upper limit
lowerLim<-pnorm(14-mu)/SE
upperLim<-pnorm(16-mu)/SE
result<-upperLim-lowerLim
result
```

```
## [1] 0.6826895
```
The instruction mentioned that the population is not normally distributed but remember
that the central limit theorem states that given a sufficiently large sample size from 
a population, the mean of all samples from the same population will be normally distributed.


#### Question 7:
Consider a standard uniform density. The mean for this density is .5 and the variance is 1 / 12. 
You sample 1,000 observations from this distribution and take the sample mean, what value would you expect it to be near?

#### Answer
We'll generate 1000 random numbers following this normal distribution mean=0.5 and SD=1/12 and then get the mean 

```r
mu<-0.5
var<-1/12
n<-1000
mean(rnorm(n, mean = mu, sd = sqrt(var)))
```

```
## [1] 0.5166301
```

As the variance was very small we could've expected the sample mean to be close to the population mean as
it is a uniform distribution with a very small SD and and a large sample size

#### Question 8:
The number of people showing up at a bus stop is assumed to be
Poisson with a mean of 5 people per hour. You watch the bus
stop for 3 hours. About what's the probability of viewing 10 or fewer people?

#### Answer

```r
q<-10
lambda<- 3*5 # mean 5 per hour times 3
ppois(q, lambda)
```

```
## [1] 0.1184644
```



```r
# Create .md, .html, and .pdf files
#knit("project_week2.Rmd")
#markdownToHTML('project_week2.md', 'My_Analysis.html', options=c("use_xhml"))
#system("pandoc -s My_Analysis.html -o My_Analysis.pdf")
```
