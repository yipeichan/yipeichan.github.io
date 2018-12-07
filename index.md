title: <p>    <br></p>
logo: /assets/logo.png
description: <div class="e"><font color="#a9cba3", font size="4.7"><b><i>Welcome to my homepage! </i></b></font></div><br><b><i><font size="4">YI-PEI CHAN</font> is an actuary specializes in life insurance. She earned her Bachelor's Degree in Economics and Biological Statistics Program from National Taiwan University. She is enthusiastic about math, programming, entrepreneurship and civic engagement.</i></b> 
show_downloads: false
google_analytics: UA-123794012-1
theme: jekyll-theme-minimal

################################################################
_layouts
################################################################

<!DOCTYPE html>
<html lang="{{ site.lang | default: "en-US" }}">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href='http://fontsforweb.com/font/getcss?id=411&apikey=80b2ae5f5b82b4f270c9dcff5f332901' rel='stylesheet' type='text/css'>

{% seo %}
    <link rel="stylesheet" href="{{ "/assets/css/style.css?v=" | append: site.github.build_revision | relative_url }}">
    <!--[if lt IE 9]>
    <script src="//cdnjs.cloudflare.com/ajax/libs/html5shiv/3.7.3/html5shiv.min.js"></script>
    <![endif]-->
    <style>
div.a {
    line-height: 10px;
}

div.b {
    line-height: 30px;
}

div.c {
    line-height: 5cm;
}

div.d {
    line-height: 1cm;
}
@font-face {
   font-family: 'Cedarville Cursive', cursive;
   src: local('Cedarville Cursive'), local('ChanceryCursive'),
       url('./fonts/Cedarville-Cursive.woff2') format('woff2'),
       url('/fonts/Cedarville-Cursive.ttf') format('ttf'),
       url('/fonts/Cedarville-Cursive.eot') format('eot'),
       url('./fonts/Cedarville-Cursive.woff') format('woff');
}

@font-face {
   font-family: cursive;
   src: url(http://fontsforweb.com/font/getcss?id=411&apikey=80b2ae5f5b82b4f270c9dcff5f332901);
   font-weight: bold;
}

div.e {
   font-family:'Cedarville Cursive', cursive,'Trebuchet MS' ;
   font-weight: 500;
}
      
p.ex1 {
    margin: -10px;
}

            
</style>
    
<style>
body {
    background: #ffe7e1;
}
</style>
<style>
  hr { 
    width: 100%;
    height: 1.5px;
    margin-left: auto;
    margin-right: auto;
    background-color:#b3b3b3;
    color:#b3b3b3;
    border: 0 none;
    }   
</style>
    
  </head>
  <body>
    <div class="wrapper">
      <header>
        <h1><a href="{{ "/" | absolute_url }}">{{ site.title | default:site.github.repository_name}}</a></h1>
        
        {% if site.logo %}
          <img src="{{site.logo | relative_url}}" alt="Logo" />
        {% endif %}

        <p>{{ site.description | default: site.github.project_tagline }}</p>

        {% if site.github.is_project_page %}
        <p class="view"><a href="{{ site.github.repository_url }}">View the Project on GitHub <small>{{ site.github.repository_nwo }}</small></a></p>
        {% endif %}

        {% if site.github.is_user_page %}
        <p class="view"><a href="{{ site.github.owner_url }}">View My GitHub Profile</a></p>
        {% endif %}

        {% if site.show_downloads %}
        <ul class="downloads">
          <li><a href="{{ site.github.zip_url }}">Download <strong>ZIP File</strong></a></li>
          <li><a href="{{ site.github.tar_url }}">Download <strong>TAR Ball</strong></a></li>
          <li><a href="{{ site.github.repository_url }}">View On <strong>GitHub</strong></a></li>
        </ul>
        {% endif %}
      </header>
      <section>

      {{ content }}

      </section>
      <footer>
        {% if site.github.is_project_page %}
        <p>This project is maintained by <a href="{{ site.github.owner_url }}">{{ site.github.owner_name }}</a></p>
        {% endif %}
      </footer>
    </div>
    <script src="{{ "/assets/js/scale.fix.js" | relative_url }}"></script>
    {% if site.google_analytics %}
    <script>
      (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
      (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
      m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
      })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');
      ga('create', '{{ site.google_analytics }}', 'auto');
      ga('send', 'pageview');
    </script>
    {% endif %}
  </body>
</html>


################################################################
index.md
################################################################

---
layout: default
---
<div class="d"><div class="e"><font color="#a9cba3"><font size="5"><b><i> A Blog Sharing YI-PEI's Projects</i></b></font></font></div></div>
<br>
<div class="d"><i>May 25, 2018</i></div>
# [_Option Pricing_](./optionPricing.html)   
<div class="d"></div>
This article shares an option pricing program with Monte Carlo Simulation method and binomial tree framework.<br>
<br>
<br>
<br>
<br>
<hr>
<br>
<div class="d"><i>Mar 2, 2018</i></div>
# [_Pricing Whole-life Insurance_](./pricingWholelifeInsurance.html)   
<div class="d"></div>
This article shares a pricing program for an insurance contract whose premiums are payable annually for 20 years and provides an endowment, whole-life annuity benefit and Death/ Total Permanent Disability coverage.<br>
<br>
<br>
<br>
<br>
<hr>
<br>
<div class="d"><i>Feb 28, 2018</i></div>
# [_Web Scraping Insurance Products_](./webScrapingInsuranceProducts.html)   
<div class="d"></div>
This article shares a program that can be run weekly to generate lists to track newly launched/ discontinued products in the insurance market.<br>
<br>
<br>
<br>
<br>
<hr>
<br>
<div class="d"><i>Jan 25, 2018</i></div>
# [_Statistical Learning_](./statisticalLearning.html)   
<div class="d"></div>
This article shares code scripts and learning notes of the Statistical Learning Course I took on the Stanford online open course.<br>
<br>
<br>
<br>
<br>
<hr>
<br>
<div class="d"><i>Jul 2, 2016</i></div>
# [_Oil Price and Consumption Expenditure_](./oilPriceandConsumptionExpenditure.html)   
<div class="d"></div>
This article shares the code script and the thesis I wrote in 2016, discussing the relationship between oil price and consumption expenditure.<br>
<br>
<br>
<br>
<br>
<hr>
<br>
Hosted on GitHub &mdash; Theme modified from <a href="https://github.com/orderedlist">orderedlist</a>
<br>
© YI-PEI CHAN
