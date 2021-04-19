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
csv_file = open('olx_centro_aluguel.csv','w', encoding='utf-8')
csv_writer= csv.writer(csv_file)
csv_writer.writerow(['titulo','preço','info','postagem'])
scraper = cfscrape.create_scraper()
```


```python
oi =int(1246/50) + (1246 % 50 > 0)
print(oi)
```

    25



```python
driver = webdriver.Safari()

converted_num = []
converted_pag = []
num = list(range(1, 55))
pag = list(range(1,26))

todos_links =[]

for y in num:
    y = str(y)
    converted_num.append(y)

for k in pag: 
    k = str(k)
    converted_pag.append(k)

for w in range(0,25):    
    url='https://rj.olx.com.br/rio-de-janeiro-e-regiao/centro/imoveis/aluguel?o'+converted_pag[w]
    driver.get(url)
    timeout = 30

    for x in range(0,54):
        try:
            links = driver.find_element_by_xpath('//*[@id="ad-list"]/li['+converted_num[x]+']/a').get_attribute('href')
        except:
            links=None
        if links != None:
            todos_links.append(links)
        try: 
            link = driver.find_element_by_xpath()
        except:
            link = None
            
    
driver.close()        
```


```python
for i in todos_links:
    source = i
    r = scraper.get(source)
    soup = BeautifulSoup(r.content,'html.parser')
    content = soup.find_all("div",class_="sc-bdVaJa h3us20-1 h3us20-0 gvtffP")

    for imovel in content:
        titulo = imovel.find('h1').text
        try:
            preço = imovel.find('h2').text
        except:
            preço=None
                 
        try:
            postagem = imovel.find('span',class_='sc-1oq8jzc-0 jvuXUB sc-ifAKCX fizSrB').text
        except:
            postagem=None        
        try:
            logradouro = imovel.find('dd',class_='sc-1f2ug0x-1 ljYeKO sc-ifAKCX kaNiaQ').text
        except:
            logradouro = None
            
        info=[]
        dado = [b.get_text() for b in soup.find_all('div',class_='sc-hmzhuo sc-1f2ug0x-3 ONRJp sc-jTzLTM iwtnNi')]
    
        for t in dado:
            t=t.replace('\n', '')
            info.append(t)    

        print(titulo,preço,info,postagem)
        csv_writer.writerow([titulo,preço,info,postagem])
```

 
```python
csv_file.close()
```


```python

```
