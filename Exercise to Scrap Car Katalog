#IMPORT CHROMEDRIVER(FOR REQUEST WEB), SELENIUM (SCRAPING) AND PANDAS (MANIPULATION DATA)
import selenium
from selenium import webdriver
import pandas as pd

#MAKING AN SERVICE TO GET WEB'S URL
#IMPORT KEYS
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.service import Service
import os
import time
import csv
import re

#GET URL
ser = Service("C:\\Users\chromedriver\chromedriver.exe")

#MAKE VARIABLE "OPTION"
option = webdriver.ChromeOptions()
option.add_argument("--incognito")
option.add_argument('--ignore-certificate-errors')

#OPEN BROWSER WITH WHITE PAGE (OPTION MODE)
browser = webdriver.Chrome(service=ser, options=option)

#DEFINE THE URL AND ACCESS IT
url = "https://www.autoscout24.com/lst/volkswagen/golf-(all)?sort=price&desc=0&ustate=N%2CU&kmto=50000&fregfrom=2016&atype=C&ac=0"
browser.get(url)
time.sleep(2)

#FIRST ITERATION AND MAKE URL LIST
i = 2
url_list = []

#APPEND FIRST URL TO URL_LIST
url_list.append(url)

#ITERATE AND APPEND TO URL_LIST
while i < 21:
    url_to_add = "https://www.autoscout24.com/lst/volkswagen/golf-(all)?sort=price&desc=0&ustate=N%2CU&size=20&page="+str(i)+"&kmto=50000&fregfrom=2016&atype=C&ac=0&"
    url_list.append(url_to_add)
    i += 1

#Print the resulting list(JUST CHECK THE FUNCTION OF URL_LIST)
#IF YOU WANT, YOU CAN DELETE THE HASHTAG

#print(url_list)

#IMPORT BEAUTIFULSOUP TO SCRAP THE WEB, BECAUSE IN MY PYTHON CAN'T USED SELENIUM ANYMORE
from bs4 import BeautifulSoup
import requests
results = []

#ITERATION TO SCRAPE EVERY CAR SPESIFICATION
no = 1
#ITERATION EVERY PAGE, THERE ARE ABOUT 20 CARS PER PAGE
for webpage in url_list:
    #REQUEST THE PAGE
    web = requests.get(webpage)
    
    #SOUP THE WEB
    soup = BeautifulSoup(web.content, "html.parser")
    results = soup.find_all("div", class_="cl-list-element cl-list-element-gap")
    #results = soup.body
    #print(len(results))
    #results.append(result)
    
    #ITERATION TO SCRAP DETAILS CAR SPESIFICATION
    for item_element in results:
        
        #MAKING LIST OF SPESIFICATION
        title_element = []
        price_element = []
        mileage_element = []
        spec_element = []
        
        #SCRAP THE (TEXT) WHETHER WE WANT
        title_element = item_element.find_all("h2","cldt-summary-version sc-ellipsis")
        price_element = item_element.find_all("div","cldt-summary-payment")
        #spec_element = item_element.find("ul")
        spec_element = item_element.find_all("li")
        
        #CLEANING THE RESULT OF SCRAPING
        for title in title_element:
            title = title.text.strip()
        for price in price_element:
            price = price.text.strip()
        
        
        #PRINT THE RESULT UNTIL - THE END - 
        op = 1
        print(no,end='|')
        no += 1
        for spec in spec_element:
            if op == 1:
                print(title+'|'+price, end = '')
                op = 0
            print('|',end = spec.text.strip())
        print()
