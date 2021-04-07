```python
from bs4 import BeautifulSoup
import requests
import csv
import cfscrape
```


```python
csv_file = open('vivareal_aluguel.csv','w', encoding='utf-8')
csv_writer= csv.writer(csv_file)
csv_writer.writerow(['titulo','preço','condominio','iptu','descriçao','localizaçao','metros','quartos','banheiro','vaga'])
```


```python
scraper = cfscrape.create_scraper()
url = "https://www.vivareal.com.br/aluguel/rj/rio-de-janeiro/?pagina=1"
r = scraper.get(url)
soup = BeautifulSoup(r.content,'html.parser')
content = soup.find_all('article', class_='property-card__container js-property-card')

todos_links =[]
acesso = []
produtos =[]

caminho = 'https://www.vivareal.com.br'

num = list(range(1, 278))
converted_num = []

for y in num:
    y = str(y)
    converted_num.append(y)

for x in range(0,277):
    url='https://www.vivareal.com.br/aluguel/rj/rio-de-janeiro/?pagina='+converted_num[x]
    print(url)
    r = scraper.get(url)
    soup = BeautifulSoup(r.content,'html.parser')
    content = soup.find_all('article',class_='property-card__container js-property-card')  

    for link in content:
        acesso = link.find('a')['href']
        acesso = caminho + acesso
        todos_links.append(acesso)  

for i in todos_links:
    source = i
    r = scraper.get(source)
    soup = BeautifulSoup(r.content,'html.parser')
    content = soup.find_all('div',class_='main-container')
    
    for a in content:
        try:
            titulo = a.find('h1').text
        except:
            titulo = None
        try:    
            preço = a.find('h3', class_='price__price-info js-price-sale').text
        except:
            preço = None
        try:
            condominio = a.find('span',class_='price__list-value condominium js-condominium').text
        except:
            condominio = None
        try:
            iptu = a.find('span',class_='price__list-value iptu js-iptu').text
        except:
            iptu = None
        try:    
            descriçao = a.find('p', class_='description__tex').text
        except:
            descriçao = None
        try:    
            localizaçao = a.find('p', class_='title__address js-address').text
        except:
            localizaçao = None
        try:    
            metros = a.find('li',class_="features__item features__item--area js-area").text
        except:
            metros = None
        try:
            quartos = a.find('li',class_='features__item features__item--bedroom js-bedrooms').text
        except:
            quartos = None
        try:    
            banheiro = a.find('li',class_="features__item features__item--bathroom js-bathrooms").text
        except:
            banheiro = None
        try:   
            vaga = a.find('li',class_="features__item features__item--parking js-parking").text
        except:
            vaga = None
        print(titulo,preço,condominio,iptu,descriçao,localizaçao,metros,quartos,banheiro,vaga)
        csv_writer.writerow([titulo,preço,condominio,iptu,descriçao,localizaçao,metros,quartos,banheiro,vaga])        


```

```python
csv_file.close()
```
