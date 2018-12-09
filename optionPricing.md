---
layout: posts
---
<br>

# [_Option Pricing_](./index.html)
<i>May 25, 2018</i>

<a href="https://github.com/yipeichan/Lookback-Option-Pricing">Link to complete code on Github</a>
<br>
## Introduction
<div class="f">
This program was written in June 2016 when I took the course: Financial Computation in National Taiwan University. Unlike normal optins, lookback options are path dependent and its strike price is only determined at maturity. The payoff rather than be calculated according to a fixed strike price; the strike price equals to the maximum or minimum price of underlying assets over the life of the option.
<br>
 Therefore, the pay off of an European lookback option can be written as:<br> 
 1. call: <br>
 c<sub>t</sub>=max(S<sub>t</sub>-m<sup>t</sup><sub>0</sub>,0), m<sup>t</sup><sub>0</sub> = min{S<sub>u</sub>|0<=u<=t}
 <br>
 2. put:<br>
 p<sub>t</sub>=max(m<sup>t</sup><sub>0</sub>-S<sub>t</sub>,0), m<sup>t</sup><sub>0</sub>= max{S<sub>u</sub>|0<=u<=t}

 
  
<br><br></div>

## [Back](./)
