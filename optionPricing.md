---
layout: posts
---
<br>

# [_Option Pricing_](./index.html)
<i>May 25, 2018</i>

<a href="https://github.com/yipeichan/Lookback-Option-Pricing"><b>Link to complete code on Github</b></a>
<br>
## Introduction
<div class="f">
This program was written in June 2016 when I took the course: Financial Computation in National Taiwan University. Unlike normal optins, lookback options are path dependent and its strike price is determined at maturity. The payoff rather than be calculated according to a fixed strike price; the strike price equals to the maximum or minimum price of underlying assets over the life of the option. Therefore, the pay off of an European lookback option can be written as:<br><br> 
<font color="black"><b>1. Call: </b><br></font>
c<sub>t</sub> = max(S<sub>t</sub>-m<sub>t</sub>,0), m<sub>t</sub> = min{S<sub>u</sub>|0<=u<=t}
<br><br>
<font color="black"><b>2. Put: </b><br></font>
p<sub>t</sub> = max(m<sub>t</sub>-S<sub>t</sub>,0), m<sub>t</sub>= max{S<sub>u</sub>|0<=u<=t}
<br></div>

## Pricing Algorithm-- Monte Carlo Simulation
<div class="f">
The pricing algorithm can be sepreated into process as follows:
1. Generate a uniformly distributed random variable between 0 and 1, and compute the value under normal distribution using the inverse cummulative distribution function. The inverse cummulative distribution function can be written in different ways which is often discussed in the course of Numerical Analysis.</div>

```python
#  Generate a uniformly distributed random variable

		u=rand()/(double)RAND_MAX;
		normInv = NormalCDFInverse(u);
		normInv=normInv*standardDev-mean;				
		stockPrice[i]=stockPrice[i]*exp(normInv);
		smax=max(smax,stockPrice[i]);

```
<div class="f">
2. Recall that if Z ~ N(0,1), a lognormal stock price can be written <br>
<font size="large">S<sub>T</sub> = S<sub>0</sub>*e<sup> (&alpha; - &delta; - 0.5 * &sigma; * &sigma; ) * T+ &sigma; * sqrt(T) *Z </sup> <br></font>
Therefore, we can derive the price as follow, and later find averages of payoffs with numerous times of simulation.</div>

```python

	//European lookback put
	stockPrice[i]=max(smax-stockPrice[i],0)*exp(-iRate*tOption);
	average1= average1+stockPrice[i];

``` 
 
  
<br><br>

## [Back](./)
