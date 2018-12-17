---
layout: posts
---

<br>
# [_Pricing Whole-life Insurance_](./index.html)
<i>Mar 2, 2018</i>
<br>
<br>
<a href="https://github.com/yipeichan/Life-Insurance-with-Annuity"><b>Link to complete code on Github</b></a>
<br>
## Introduction
<div class="f">
This program was modified from one of the insurance products that I devised. It launched market on November 30<sup>th</sup> 2017, and had pretty good sales record. The insurance contract has premium payment peiord of 20 years and provides benefits as follows,<br><br>
     
<font color="black"><b>1. Death/ Total disability benefit:</b></font><br>
during the premium payment peroid (<=the 20th policy year):<br>
max(policy value, 1.06 times total premium paid, 3 times of amount insured)<br>
after the premium payment period (>=the 21st policy year):<br>
max(policy value, 1.06 times total premium paid, 1 time of amount insured)<br><br>

<font color="black"><b>2. Life annuity:</b></font><br>
payable annually <br>
during the premium payment peroid ( before the 20th policy year):<br>
5% of the premium<br>
after the premium payment period ( after the 20th policy year):<br>
50% of the premium<br><br>

<font color="black"><b>3. Endowment:</b></font><br>
When the policy holder reaches age 105, the endowment is paid as 1.06 times the total premium paid<br><br>

The motality rate was based on the Fifth Life Experience Table of Taiwan Life Insurance Industry and proveided as a csv file in the github project link page. 
</div>
<br>
## An Insurance Policy Catered to Human Life Cycle
<div class="f">
The main target client group of this contract are people aged between 20 to 55. People in such age range are often those who bring home the backon; they go out to work, on business trevels frequently, which exposed them to higher risks on streets or abroad. Once accidents strike, he/she may lose the ability to work, affecting financial situation of entire family. Therefore during the premium payment period, which is 20 years, the policy provides high leverage of death coverage compared to the amount of premium paid. After 20 years, it would be the time of retirment, and the policy provides 50% of the annual premium until the insured reaches age 105. The annuity helps policy beneficiaries prevent money shortage in face of prolonged life expectancy.<br><br></div>

![financial-plan](https://user-images.githubusercontent.com/24948460/49664603-4e8d0e80-fa8d-11e8-8305-201c7a5ae0c7.png)<font size="xx-small">(photo from omtatsat.tk)</font>

<br>
## Pricing Algorithm
<div class="f">
In addition to reading the mortality rate from csv at the beginning, the pricing program can be mainly devided into two parts: the benefit and the present value discounting process.
<br>
<br>
<font color="black"><b>1. Benefits</b></font><br>
The benefit part is where I set the amount of coverage should death or total disability occur, and the amount of annuity to give out to the beneficiary upon the existence of the insured. The benefit part is written as follows,<br><br></div>
     
```python
# benefit of death/ total disability coverage and annuity payment 
  
  termpB[pt-1]= 1.06*np.ceil(GP*unit)/unit*ppp 
  
  for i in range(0,pt):
       if i>0:
            pricingVs[i]=pricingV[i]+termpB[i-1]+survB[i-1] #pricing, policy value with annuity amount included
            pricingV[i]=max((deathPVlist[i]+termPlist[i]+survPlist[i])-aDuelist[i]*p2,0)
            if i<=ppp-1:deathBV[i]=(pricingV[i]+pricingVs[i+1]+p2)/2
            else: deathBV[i]=(pricingV[i]+pricingVs[i+1])/2
            
       else: #i=0
            pricingV[i]=max((deathPVlist[i]+termPlist[i]+survPlist[i])-aDuelist[i]*NP,0)
            deathBV[i]=(pricingV[i]+pricingVs[i+1]+p1)/2
            
       if i<=ppp-1:  ###death benefit with premium included to take max.
            deathB[i]=max(deathBV[i],1.06*np.ceil(GP*unit)/unit*(i+1),3)
            survB[i]=np.ceil(GP*unit*0.05)/unit
            
       else:
            deathB[i]=max(deathBV[i],1.06*np.ceil(GP*unit)/unit*ppp,1)
            survB[i]=np.ceil(GP*unit*0.5)/unit
            
  deathBV[pt-1]=(pricingV[pt-1]+termpB[pt-1]+survB[pt-1])/2  
```
<div class="f">   
<font color="black"><b>2. Discounting the Insurance Benefits</b></font><br>
Using backwards recursion, the program can generate the expected present value of the benefit outgo, which is the expected present value of the net premium income.<br><br></div>

```python
# discounting the expected value of death/ total disability coverage and annuity payment 
  for i in range(pt-1,-1,-1):
       survP= (survB[i]*(popSurv[i]-popDeath[i])*v+survPlist[i+1]*popSurv[i+1]*v)/popSurv[i]
       termP=(termpB[i]*(popSurv[i]-popDeath[i])*v+termPlist[i+1]*popSurv[i+1]*v)/popSurv[i] 
       if i>=ppp: aDue=0
       else: aDue=(popSurv[i]+aDue*popSurv[i+1]*v)/popSurv[i]
       aDuelist[i]=aDue
       termPlist[i]=termP
       survPlist[i]=survP     
       deathPV= (deathB[i]*popDeath[i]*v**0.5+deathPVlist[i+1]*popSurv[i+1]*v)/popSurv[i]  
       ##pricing death value of the policy   
       deathPVlist[i]=deathPV
```

<br>
## Mathematical Statement
<div class="f">Writing the expected present values of the benefits provided in this policy in mathematical equations would be as follows,<br>
n: premium payment period<br> 
i: assumed interest rate<br> 
x: age insured<br>
<br>
</div>
<font color="black"><b>1. Death/ Total Disability Benefit<br></b></font>
<br>
<img width="552" alt="screen shot 2018-12-07 at 11 31 20 pm" src="https://user-images.githubusercontent.com/24948460/49688365-c457af80-fb4b-11e8-9343-29a1eb99e8cc.png">
<br>
<br>
<font color="black"><b>2. Annuity<br></b></font>
<br>
<img width="429" alt="screen shot 2018-12-07 at 11 31 43 pm" src="https://user-images.githubusercontent.com/24948460/49688364-c457af80-fb4b-11e8-91ef-5ee1914725cc.png">
<br>
<br>
<font color="black"><b>3. Endowment<br></b></font>
<br>
<img width="354" alt="screen shot 2018-12-07 at 11 31 50 pm" src="https://user-images.githubusercontent.com/24948460/49688362-c3bf1900-fb4b-11e8-8bc7-f75646e7e786.png">
<br>
<br>
<font color="black"><b>4. Insurance Premium <br></b></font>
<br>
<img width="322" alt="screen shot 2018-12-07 at 11 31 55 pm" src="https://user-images.githubusercontent.com/24948460/49688361-c3bf1900-fb4b-11e8-9716-5c14b67d0a8d.png">
<br>
<br>

## Pricing Program Applications
<div class="f">
The program starts with asking you to enter information about the age, loading and the sex you want to test. The loading is the markup of net premium, which is one source of the profits that insurance companies earn, and most of the time the source of agent commissions. After entering the information you want to know, the program would demonstrate the asymptotic process and generate the result if the premium converges under the conditions you entered. 
<br>
<br>
For example, to price the insured who is
<br>
<br>
<font color="black"><b>1. male, aged 35, and the loading set to be 10% </b></font>
<br>
<br>
<img width="945" alt="screen shot 2018-12-08 at 12 08 48 am" src="https://user-images.githubusercontent.com/24948460/49659079-61e4ad80-fa7e-11e8-8da2-9278f7d3bf67.png">
<br>
<br>
<font color="black"><b>2. female, aged 62, and the loading set to be 9.3%</b></font>
<br>
<br>
<img width="675" alt="screen shot 2018-12-16 at 8 24 43 pm" src="https://user-images.githubusercontent.com/24948460/50053470-c4ba0100-0170-11e9-9ace-9bebf310c363.png">

</div>

<br>
<br>


## [Back](./)
