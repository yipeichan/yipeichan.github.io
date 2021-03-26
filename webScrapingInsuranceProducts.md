---
layout: posts
---
<br>

# [_Web Scraping Insurance Products_](./index.html)
<i>Feb 28, 2018</i>

<a href="https://github.com/yipeichan/Insurance-Product-Lists-with-Web-Scraping"><b>Link to complete code on Github</b></a>

## Introduction
<div class="f"><font color="black">
This program was written because I have to do insurance market investigation weekly at work. Information such as products discontinued, new products being launched, coverage of the newly launched policies, and so on need to be recorded and later be generated as a report. In Taiwan, it is regulated by law that the clause, loading of certain ages, and exception clauses should be disclosed publicly on the internet. While large insurance companies in Taiwan often provide 100 to 200 insurance contracts, it is not efficient to go through webpages manually to find new products or discontinued ones. I thus wrote this program to automatically generate reports weekly to track newly launched/ discontinued products in the insurance market.<br><br></font></div>

## Algorithm
<div class="f"><font color="black">
The program can mainly be divided into two parts as follows,<br>
<br>
<b>1. Extracting information from the web</b><br>
The program extracts all the names of products available from the site of the targeted insurance company; it then exports the information into separated CSV files according to the category of insurance (ex. life, health, personal injury, annuities, group insurance, etc) with the inputted date added at the end of the name of the CSV files. <br><br></font></div>

```python

	def open(filename):						####read csv
		with open(os.path.join(myPath, filename), 'rU') as csvfile:
			readCSV=csv.reader(csvfile, delimiter=',')
			insurances=[]
			p_final=[]
			for insurance in readCSV:
				insurances.append(" ".join(insurance))
			for word in insurances:
				insurance=word.replace(" ", "")
				p_final.append(insurance.replace(u'\ufeff', ''))
			return p_final 
	def compare(new,previous):			####compare products in two csvs
		print("Newly Launched:\n",list(set(new)-set(previous)),"\n")
		print("Discontinued:\n",list(set(previous)-set(new)),"\n")
	def request(filename,page):			###write page content into csv
		csv_file = open(os.path.join(myPath, filename),'a', newline='',encoding='utf-8-sig')
		csv_writer = csv.writer(csv_file)
		csv_writer.writerow([" ".join(date.split())]) ###leave out blank spaces in the name
		res=requests.get(page)
		#res.raise_for_status()
		#res.encoding='CJK'
		soup=bs4.BeautifulSoup(res.text,'lxml')
		for i in soup.select('.panel-header'):
			insurance =i.text
			insurance=" ".join(insurance.split())
			#print(" ".join(insurance.split()))
			csv_writer.writerow([insurance.replace(u'\ufeff', '')])
		csv_file.close()
	def setdate():
		date=input("set the date in the file name: ")
		return date

```

<div class="f"><font color="black">
<b>2. Comparing CSV lists</b><br>
The program can compare product lists of two designated dates(ex. all types of insurances of 20180716 vs those of 20180709 ) and produce outcomes of new products that had been launched (i.e newly posted on the site)and what had been discontinued (i.e no longer on the site) within the specified period. <br><br></font></div>

```python

renew=input("to compare all lists, please input: 1 \nto compare only two lists, please input: 2\nyour input: ")
if renew=="1":
	new_file=input("Enter the date of the new file: ")
	old_file=input("Enter the date of the previous file: ")
	for i in product_type:
		a=report.open(i+new_file+'.csv')
		b=report.open(i+old_file+'.csv')
		print("\n",i)
		report.compare(a,b)
		print("\n")


elif renew=="2":
	new_file=input("Enter the name of the new file: ")
	old_file=input("Enter the name of the previous file: ")
	a=report.open(new_file)
	b=report.open(old_file)
	report.compare(a,b)

else:
	print("wrong input")


```

<br>

## Complete Code
The complete code for this progam is as following.

```python
######for Tracking Products of China Life Insurance Group  

import requests
import os
import bs4
import csv


class report:
	def __init__(self, new, previous, date):
		self.new=new
		self.previous=previous
		self.date=date
	def set_path():						#set the path of the directory
		global myPath
		myPath=input("Enter the path of the directory: ")
		return myPath
	def open(filename):						####read csv
		with open(os.path.join(myPath, filename), 'rU') as csvfile:
			readCSV=csv.reader(csvfile, delimiter=',')
			insurances=[]
			p_final=[]
			for insurance in readCSV:
				insurances.append(" ".join(insurance))
			for word in insurances:
				insurance=word.replace(" ", "")
				p_final.append(insurance.replace(u'\ufeff', ''))
			return p_final 
	def compare(new,previous):			####compare products in two csvs
		print("Newly Launched:\n",list(set(new)-set(previous)),"\n")
		print("Discontinued:\n",list(set(previous)-set(new)),"\n")
	def request(filename,page):			###write page content into csv
		csv_file = open(os.path.join(myPath, filename),'a', newline='',encoding='utf-8-sig')
		csv_writer = csv.writer(csv_file)
		csv_writer.writerow([" ".join(date.split())]) ###leave out blank spaces in the name
		res=requests.get(page)
		#res.raise_for_status()
		#res.encoding='CJK'
		soup=bs4.BeautifulSoup(res.text,'lxml')
		for i in soup.select('.panel-header'):
			insurance =i.text
			insurance=" ".join(insurance.split())
			#print(" ".join(insurance.split()))
			csv_writer.writerow([insurance.replace(u'\ufeff', '')])
		csv_file.close()
	def setdate():
		date=input("set the date in the file name: ")
		return date

print("\n===============================")
product_type=['Life_Insurance','Annuity_Insurance','Health_Insurance','Travel_Accident_Insurance']
report.set_path()
renew=input("Renew the product lists? y/n: ")

if renew=="n":
	print("process moves to list comparison")

elif renew=="y":
	#date=input("set the date in the file name: ")
	date=report.setdate()
	print("the progam is exporting product lists from the web")	
	report.request(product_type[0]+date+'.csv','https://www.chinalife.com.tw/wps/portal/chinalife/product-overview/personal/life-refund')	
	report.request(product_type[1]+date+'.csv','https://www.chinalife.com.tw/wps/portal/chinalife/product-overview/personal/annuity-assurance')
	report.request(product_type[2]+date+'.csv','https://www.chinalife.com.tw/wps/portal/chinalife/product-overview/personal/health')
	report.request(product_type[3]+date+'.csv','https://www.chinalife.com.tw/wps/portal/chinalife/product-overview/personal/travel')

	print("product lists are prepared\n")

else:
	print("wrong input")

print("===============================")
renew=input("to compare all lists, please input: 1 \nto compare only two lists, please input: 2\nyour input: ")
if renew=="1":
	new_file=input("Enter the date of the new file: ")
	old_file=input("Enter the date of the previous file: ")
	for i in product_type:
		a=report.open(i+new_file+'.csv')
		b=report.open(i+old_file+'.csv')
		print("\n",i)
		report.compare(a,b)
		print("\n")


elif renew=="2":
	new_file=input("Enter the name of the new file: ")
	old_file=input("Enter the name of the previous file: ")
	a=report.open(new_file)
	b=report.open(old_file)
	report.compare(a,b)

else:
	print("wrong input")

```

<br>

## Program Instructions <br>
<div class="f"><font color="black">
<font color="black"><b>1. Enter the path of the directory of your files:</b></font><br><br>
<img width="1226" alt="demo1" src="https://user-images.githubusercontent.com/24948460/46902893-ada42c00-ceff-11e8-92b2-a18f776b0391.png">
<br>
<br>
<font color="black"><b>2. If you want to obtain the updated product lists, enter y, otherwise n (see point 4)<br>
After entering y, input the date, and the date will automatically be added to CSV files (CSV files be separated according to the category of insurances)</b><br><br></font>
<img width="1099" alt="demo2" src="https://user-images.githubusercontent.com/24948460/46902904-e2b07e80-ceff-11e8-81c5-735ece2ffca6.png">
<br>
<br>
<font color="black"><b>3. Enter the dates of the files to be compared, and the result would display the products newly launched/ discontinued or sales channel changes within the period. From the example below, there was no product newly launched or discontinued within 2018.10.13 and 2018.10.03. </b><br><br></font>
<img width="851" alt="demo3" src="https://user-images.githubusercontent.com/24948460/46902908-ea702300-ceff-11e8-9dcc-f5ac2eb5bf00.png">
<br>
<br>
<font color="black"><b>4. (continued with point 2) Users can directly compare lists of two dates or simply two CSV files without renewing product lists.<br>
To compare all lists (i.e all kinds of insurance) of two dates, enter 1  <br>
To compare only two CSV files, enter 2 (see point 6) </b><br><br></font>
<img width="1138" alt="demo4" src="https://user-images.githubusercontent.com/24948460/46902909-ea702300-ceff-11e8-9c3f-d35bd38c2eee.png">
<br>
<br>
<font color="black"><b>5. The result of the comparison would be displayed. From the example below, we can know that there were 1 product newly launched and 1 product discontinued within 2018.07.16 and 2018.07.09.</b><br><br></font>
<img width="1131" alt="demo5" src="https://user-images.githubusercontent.com/24948460/46902910-eb08b980-ceff-11e8-93f3-9022ab6e2a61.png">
<br>
<br>
<font color="black"><b>6. (continued with point 4) Enter the two file names to be compared, and the result of the comparison would be displayed </b></font><br><br>
<img width="1076" alt="demo6" src="https://user-images.githubusercontent.com/24948460/46902966-d37e0080-cf00-11e8-8fc5-846aafc5cd93.png">
</font>
</div>	
<br>
<br>




## [Back](./)
