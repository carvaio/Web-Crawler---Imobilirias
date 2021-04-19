```python
import os
import time
import re
import json
from datetime import datetime
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from collections import Counter as cnt
from bs4 import BeautifulSoup
import requests
import csv
import cfscrape
```


```python
oi =int(1048/20) + (1048 % 20 > 0)
print(oi)
```


```python
csv_file = open('casamineira_centro_aluguel.csv','w', encoding='utf-8')
csv_writer= csv.writer(csv_file)
csv_writer.writerow(['titulo','preço','condominio','iptu','area','quarto','suite','banheiro','vaga','elevador'])
scraper = cfscrape.create_scraper()
```


```python
scraper = cfscrape.create_scraper()
driver = webdriver.Safari()

converted_num = []
converted_pag = []
num = list(range(1,21))
pag = list(range(1,54))

todos_links =[]

for y in num:
    y = str(y)
    converted_num.append(y)

for k in pag: 
    k = str(k)
    converted_pag.append(k)

for w in range(0,53):
    url='https://www.casamineira.com.br/aluguel/imovel/centro_rio-de-janeiro_rj?pagina='+converted_pag[w]
    driver.get(url)
    timeout = 30

    for x in range(0,20):
        try:
            links = driver.find_element_by_xpath('//*[@id="content-area"]/div[4]/div[1]/div/div['+converted_num[x]+']/div/div/div[2]/h2/a[1]').get_attribute('href')
        except:
            links=None
        if links != None:
            todos_links.append(links)
            print(links)

driver.close()        
    
```


```python
for i in todos_links:
    driver = webdriver.Safari()
    driver.get(i)

    try:
        titulo = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[1]/div[1]/h1/text()').text
    except:
        titulo= None
    try:
        preço = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[2]/div[1]/div[1]/text()').text
    except:
        preço=None
    try:
        condominio = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[2]/div[1]/div[2]/text()').text
    except:
        condominio = None
    
    try:    
        iptu = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[2]/div[1]/div[3]/text()').text
    except:
        iptu = None
    try:    
        area = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[1]/div[2]/ul/li[1]/span').text
    except:
        area= None
    try:
        quarto = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[1]/div[2]/ul/li[2]/span').text
    except:
        quarto = None
    try:    
        suite = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[1]/div[2]/ul/li[3]/span').text
    except:
        suite = None
    try:    
        banheiro = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[1]/div[2]/ul/li[4]/span').text
    except:
        banheiro = None
    try:    
        vaga = driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[1]/div[2]/ul/li[5]/span').text
    except:
        vaga = None
    try:
        elevador =driver.find_element_by_xpath('//*[@id="root"]/section/section[2]/div[1]/div/div[1]/div[2]/ul/li[6]/span').text
    except:
        elevador = None

    print(titulo,preço,condominio,iptu,area,quarto,suite,banheiro,vaga,elevador)
    csv_writer.writerow([titulo,preço,condominio,iptu,area,quarto,suite,banheiro,vaga,elevador])
    driver.close()
```


```python
csv_file.close()
```


```python
print(len(todos_links))
```

    1049



```python

```
