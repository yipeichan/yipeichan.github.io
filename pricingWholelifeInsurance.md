---
layout: default
---
<br>
# [_Pricing Whole-life Insurance_](./index.html)
<i>Mar 2, 2018</i>
<br>
<br>
<a href="https://github.com/yipeichan/Life-Insurance-with-Annuity"><b>See complete code on Github</b></a>
<br>
## Introduction
<div class="f">
This program was modified from one of the insurance products that I devised. It launched market on November 30th, and had pretty good sales record. The insurance contract provides both annuity and death coverage. </div>
<br>
## An Insurance Policy Catered to Human Life Cycle
<div class="f">
The main target client group of this contract are people aged between 20 to 55. For people in such age range are often those who bring home the backon; they go out to work, on business trevels frequently, which exposed them to higher risks on streets or abroad. Once accidents strike, he/she may lose the ability to work, affecting financial situation of entire family.<br> Therefore during the premium payment period, which is 20 years, the policy provides high leverage of death coverage compared to the amount of premium paid. After 20 years, it would be the time of retirment, and the policy provides 50% of the annual premium until the insured reaches age 105. The annuity helps policy beneficiaries prevent money shortage in face of prolonged life expectancy.</div>
<br>
## Pricing Algorithm
<div class="f">
The pricing program is mainly devided into two parts: the benefit and the discounting process.<br>
<font color="black"><b> Benefits</b></font><br>
The benefit part is where I set the amnount of coverage should death or total disability occur, and the amount of annuity to give out to the beneficiary upon the existence of the insured. The benefit part is written ias following,<br>
```python
// benefit of death/ total disability coverage and annuity payment 
     termpB[pt-1]= 1.06*np.ceil(GP*unit)/unit*ppp    
     for i in range(0,pt):
          if i>0:
               pricingVs[i]=pricingV[i]+termpB[i-1]+survB[i-1]  #pricing, policy value with annuity amount included
               pricingV[i]=max((deathPVlist[i]+termPlist[i]+survPlist[i])-aDuelist[i]*p2,0)
               if i<=ppp-1:deathBV[i]=(pricingV[i]+pricingVs[i+1]+p2)/2
               else: deathBV[i]=(pricingV[i]+pricingVs[i+1])/2
               #else: deathBV[i]=(pricingV[i]+survB[i]+termpB[i])/2
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
<br>
<font color="black"><b> Discounting the Insurance Benefits</b></font><br>
Using backwards recursion, the program can generate the expected present value of the benefit outgo, which is the expected present value of the net premium income.
<br>
```python
// discounting the expected value of death/ total disability coverage and annuity payment 
     for i in range(pt-1,-1,-1):
          survP= (survB[i]*(popSurv[i]-popDeath[i])*v+survPlist[i+1]*popSurv[i+1]*v)/popSurv[i]
          termP=(termpB[i]*(popSurv[i]-popDeath[i])*v+termPlist[i+1]*popSurv[i+1]*v)/popSurv[i] 
          if i>=ppp: aDue=0
          else: aDue=(popSurv[i]+aDue*popSurv[i+1]*v)/popSurv[i]
          aDuelist[i]=aDue
          termPlist[i]=termP
          survPlist[i]=survP     
          deathPV= (deathB[i]*popDeath[i]*v**0.5+deathPVlist[i+1]*popSurv[i+1]*v)/popSurv[i]  ##pricing death value of the policy   
          deathPVlist[i]=deathPV
```







[Back](./)
