```python
from bs4 import BeautifulSoup
import requests
import csv
import cfscrape
import cloudscraper
```


```python
csv_file = open('imovelweb_centro_aluguel.csv','w', encoding='utf-8')
csv_writer= csv.writer(csv_file)
csv_writer.writerow(['titulo','preço','localizaçao','inf','info'])
```




    35




```python
scraper = cloudscraper.create_scraper()
url = "https://www.imovelweb.com.br/imoveis-aluguel-centro-rio-de-janeiro.html"
r = scraper.get(url)
soup = BeautifulSoup(r.content,'html.parser')
conteudo = soup.find_all('h2',class_='postingCardTitle')

todos_links =[]
acesso = []
caminho = 'https://www.imovelweb.com.br'

num = list(range(1, 87))
converted_num = []

for y in num:
    y = str(y)
    converted_num.append(y)
    
for x in range(0,86):
    url='https://www.imovelweb.com.br/imoveis-aluguel-centro-rio-de-janeiro-pagina-'+converted_num[x]+'.html'
    print(url)
    r = scraper.get(url)
    soup = BeautifulSoup(r.content,'html.parser')
    conteudo = soup.find_all('h2',class_='postingCardTitle')
    
    for link in conteudo:
        acesso = link.find('a')['href']
        acesso = caminho + acesso
        todos_links.append(acesso)
        print(acesso)

for i in todos_links:
    source = i
    r = scraper.get(source)
    soup = BeautifulSoup(r.content,'html.parser')
    content = soup.find_all('div',id="main-container")
    
    for a in content:
        data=[]
        dados = [b.get_text() for b in soup.find_all('li',class_='icon-feature')]
        for s in dados:
            s = s.replace('\n', '')
            s = s.replace('\t', '')
            data.append(s)
        info=data    
        
        dat=[]
        dado = [b.get_text() for b in soup.find_all('span',class_='data')]
        for s in dado:
            s = s.replace('\n', '')
            s = s.replace('\t', '')
            data.append(s)
        inf=dat   
        
        try:
            titulo = a.find('h1').text
        except:
            titulo = None
            
        try:    
            preço = a.find('span',class_='data-price').text
        except:
            preço = None
        
        if preço == None:
            try:    
                preço = a.find('div',class_='price-items').text 
            except:
                preço = None
        
        try:    
            descriçao = a.find('div',id='reactDescription').text
        except:
            descriçao = None
            
        try:    
            localizaçao = a.find('div',class_='section-location').text
        except:
            localizaçao = None

        print(titulo,preço,localizaçao,inf,info)
        csv_writer.writerow([titulo,preço,localizaçao,inf,info])
 
```python
    csv_file.close()
```
