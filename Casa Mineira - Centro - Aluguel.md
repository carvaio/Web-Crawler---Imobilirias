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

    53



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

    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/1279906
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3566485
    https://www.casamineira.com.br/imovel/aluguel/vaga-de-garagem-para-alugar-no-centro-rio-de-janeiro-rj/3558591
    https://www.casamineira.com.br/imovel/aluguel/casa-18-quartos-para-alugar-no-centro-rio-de-janeiro-rj/1328930
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3883166
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/2897129
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3676368
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2116905
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3846477
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3910411
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1912955
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328764
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328617
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328629
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328713
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2337106
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3597141
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328786
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328703
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328618
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897152
    https://www.casamineira.com.br/imovel/aluguel/apartamento-para-alugar-no-centro-rio-de-janeiro-rj/2678199
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1328806
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897413
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328923
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897218
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328728
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328666
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3883188
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897187
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2719738
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328658
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/2897691
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328614
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3956112
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897799
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3914563
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3883202
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3453665
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328616
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328616
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897299
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3294734
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328630
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1905574
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328640
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328657
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328685
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3427024
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897120
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328846
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3861198
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897117
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3814268
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897613
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1808101
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3264214
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3814265
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3821237
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3814270
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3636697
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3636666
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2631212
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328634
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328632
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328677
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328850
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328842
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328844
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2631096
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328838
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328843
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2631082
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328890
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2975397
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897681
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328909
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2630302
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2407982
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808105
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328839
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1805411
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328791
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3827521
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328697
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328877
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897057
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897128
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897262
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897582
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897754
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883143
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897794
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328582
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2219354
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897756
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3479531
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3237007
    https://www.casamineira.com.br/imovel/aluguel/galpao-para-alugar-no-centro-rio-de-janeiro-rj/1328810
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2631109
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897556
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2185714
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3814267
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3872939
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328589
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328782
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328894
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328895
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328896
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328899
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328700
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328840
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328916
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3883118
    https://www.casamineira.com.br/imovel/aluguel/apartamento-para-alugar-no-centro-rio-de-janeiro-rj/3895825
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897315
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897567
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328841
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2507539
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2507540
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2800750
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2800760
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3923135
    https://www.casamineira.com.br/imovel/aluguel/apartamento-para-alugar-no-centro-rio-de-janeiro-rj/3896119
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3921293
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3921294
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3479504
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1788375
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3453663
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3948828
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897332
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897091
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897296
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897434
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897663
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3020776
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328885
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328758
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328794
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328884
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328760
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328914
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897641
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2764097
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897559
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328807
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897378
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2579355
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897088
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897278
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897261
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897783
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328864
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2263663
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328724
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2579356
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897379
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897584
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897474
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328704
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328812
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3955406
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328664
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328584
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2679170
    https://www.casamineira.com.br/imovel/aluguel/apartamento-para-alugar-no-centro-rio-de-janeiro-rj/3896006
    https://www.casamineira.com.br/imovel/aluguel/vaga-de-garagem-para-alugar-no-centro-rio-de-janeiro-rj/1328715
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1905729
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328702
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897215
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328599
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328906
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1615969
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328808
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328919
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328878
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328918
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328815
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2961866
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2480787
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2010374
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2587356
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1788373
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2481775
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3966135
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/561683
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1103055
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3140973
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2943344
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1788379
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897145
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3895843
    https://www.casamineira.com.br/imovel/aluguel/galpao-para-alugar-no-centro-rio-de-janeiro-rj/2716255
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3799968
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3638073
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328628
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328595
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/935648
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3479532
    https://www.casamineira.com.br/imovel/aluguel/apartamento-para-alugar-no-centro-rio-de-janeiro-rj/935487
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3352632
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3127700
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328825
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328920
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1472882
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3738308
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3852154
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1806706
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/561647
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2726658
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2941498
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2981598
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3592168
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3758877
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/919070
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/919071
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1833054
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2296699
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3497531
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3091034
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3883071
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1349351
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/919040
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328693
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1802935
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897163
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/561696
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328903
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/561644
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3778783
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3811249
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3551700
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3653858
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3801021
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1126116
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/933229
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3895784
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3451227
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3452003
    https://www.casamineira.com.br/imovel/aluguel/apartamento-14-quartos-para-alugar-no-centro-rio-de-janeiro-rj/2936147
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897144
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3001199
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3195340
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3567703
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/2933601
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2992956
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631159
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2637613
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3568034
    https://www.casamineira.com.br/imovel/aluguel/cobertura-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3903172
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3951726
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3798845
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3879434
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3862050
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/891113
    https://www.casamineira.com.br/imovel/aluguel/galpao-para-alugar-no-centro-rio-de-janeiro-rj/1328811
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3814266
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897236
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328679
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897727
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/2653650
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897768
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897095
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897214
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3434732
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897549
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/3365610
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897381
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3195588
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3422617
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3581777
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897455
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897238
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897282
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897324
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897437
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897797
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2928752
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883115
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328731
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2411362
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3941684
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3616285
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2447523
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3954500
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328593
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328594
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328627
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328712
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328761
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2780394
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328597
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328645
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328686
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3489420
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2542018
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2939419
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883149
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2634159
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328748
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3895883
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2945481
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/561653
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3846714
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897173
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897773
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328710
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1379945
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1654581
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3664639
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3938654
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3363472
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3762397
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3473078
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3479497
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897712
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2986392
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328590
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328683
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328742
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1808090
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1808092
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1808095
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1808099
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883058
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1397978
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/660241
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328813
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808103
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3801161
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2934091
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3294733
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3862422
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3862462
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2108073
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2993050
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3293652
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/822107
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897199
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897363
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897280
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3616392
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328770
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3237310
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1490519
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897097
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897193
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897529
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897552
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3681702
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3919199
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3664604
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3913327
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1557309
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2981436
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1502915
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2770739
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3680716
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3760098
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3760841
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3763740
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3938747
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3476996
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3581953
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3760234
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3760864
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3760965
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3763395
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3784992
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3833443
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3879012
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3898320
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2209821
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2284787
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2447432
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2966994
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3001210
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2260771
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3759872
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3898448
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3538776
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3760878
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2981427
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1393526
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3621931
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3759397
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3760914
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3954196
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3981664
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3497660
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3759484
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3862504
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/794924
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3552057
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3770214
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3941965
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3851813
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883104
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897467
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897478
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3292771
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3852207
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3903315
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3584918
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3778121
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3801378
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3968248
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/828711
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1394933
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2936280
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2939178
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895994
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897458
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328932
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3943896
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3477252
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3577638
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3653817
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3762249
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3851627
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3877239
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/1507577
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/1862858
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3363588
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895872
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3707929
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3411506
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3627245
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/1888723
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1380109
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2389010
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2936262
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3124770
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3592202
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3622134
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3663975
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3764654
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3811898
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3867732
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3681507
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3692163
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3953969
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3954851
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1097128
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/1462055
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2409594
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3867606
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3941921
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3965207
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3968103
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3224217
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/1819441
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3502411
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3840819
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3877260
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3942149
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328694
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1397976
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3300041
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3819292
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3401153
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3801238
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3851537
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3871892
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3871941
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/551063
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1826548
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3076572
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3363926
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3248879
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3862143
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631058
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631061
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/2226124
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3814394
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3784663
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3178152
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3954344
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2158572
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328860
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3525742
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3835971
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3879212
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3526613
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3966924
    https://www.casamineira.com.br/imovel/aluguel/apartamento-3-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3942241
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3829908
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883101
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897247
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897745
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328644
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328933
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2774156
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3488035
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328726
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897213
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897689
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3864474
    https://www.casamineira.com.br/imovel/aluguel/apartamento-4-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3801132
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3954112
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631073
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631141
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/2897395
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3628999
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631178
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3896093
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897651
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/1328854
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897356
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3542270
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897793
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3913408
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897182
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897376
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897399
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897502
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897527
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897555
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897585
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897595
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897612
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897597
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897065
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897687
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897456
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897445
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328680
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895830
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895878
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896019
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883085
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883116
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897068
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897202
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897203
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897231
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897272
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897330
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897339
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897394
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897411
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897421
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897426
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897432
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897472
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897486
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897504
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897533
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897617
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897683
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897758
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897778
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897786
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897795
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3197063
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3236857
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328609
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328665
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328667
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328819
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328915
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328917
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897347
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897753
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895966
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895971
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895981
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897528
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897677
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897692
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328797
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328924
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897518
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897070
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897082
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897176
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897241
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897242
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897271
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897273
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897285
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897289
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897331
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897350
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897409
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897629
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897652
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897693
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3074280
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883164
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328698
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328857
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328881
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328908
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1556044
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328592
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328656
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896001
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631134
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897056
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897298
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897344
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897798
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897607
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896143
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895776
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3508808
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/3741528
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2226180
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328859
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328747
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3895972
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3942146
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2943612
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/2897801
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328738
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328739
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328740
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328741
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328745
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328746
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/919067
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/919068
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/919076
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1778054
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1778055
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2961898
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/935634
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328851
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2938442
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3552207
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3433119
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3629000
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328880
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328931
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1788378
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2935267
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3236678
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328861
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328862
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328869
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897079
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328934
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3077170
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1397974
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328598
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897387
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897716
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2961903
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3820072
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3872234
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897157
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2961867
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328711
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897678
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/935636
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2933103
    https://www.casamineira.com.br/imovel/aluguel/apartamento-4-quartos-para-alugar-no-centro-rio-de-janeiro-rj/2716621
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808093
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808097
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/878741
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/935630
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3612362
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897342
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896113
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895877
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1398174
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3497014
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3202681
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3001185
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/320350
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3512031
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896005
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3400918
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631039
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631049
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631162
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631176
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631182
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2750202
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897294
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895890
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3914820
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3487570
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2115933
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896137
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1229700
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328624
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328625
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328661
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328662
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328688
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328696
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328734
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328735
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328736
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328737
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328942
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/561682
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631213
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897101
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897112
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897475
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808096
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808098
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328756
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741354
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741418
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2932174
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896085
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2838612
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1349405
    https://www.casamineira.com.br/imovel/aluguel/casa-5-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3387454
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/1962692
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3061457
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3883123
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3487337
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2114245
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3903448
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2225959
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226063
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2365016
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2225976
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/318547
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3422012
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2774157
    https://www.casamineira.com.br/imovel/aluguel/casa-4-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3912452
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897105
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328725
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3867400
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1664123
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895973
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3680846
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328591
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2115481
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2818609
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2518925
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3552132
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3700057
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897219
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897382
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897554
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328814
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3218116
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2423133
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/3671112
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897361
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897602
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/3025301
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897276
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3798671
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883191
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328612
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328714
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1548552
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1548553
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897075
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897119
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897131
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897200
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897234
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897235
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897257
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897313
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897371
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897384
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897408
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897435
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897487
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897550
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897592
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897603
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897633
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897760
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897767
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3056773
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3056775
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897428
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3741360
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3237361
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328718
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808089
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897425
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897451
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897063
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897081
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897133
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897143
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897217
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897297
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897302
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897326
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897340
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897355
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897470
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897520
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897578
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897625
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897626
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897697
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897733
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897789
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2956220
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328690
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328709
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328855
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1548554
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1788380
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1788381
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897706
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897250
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328633
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328727
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328944
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3387938
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226034
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741381
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2114313
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631221
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3760294
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226148
    https://www.casamineira.com.br/imovel/aluguel/casa-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/3777497
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2493772
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226071
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3243730
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2225968
    https://www.casamineira.com.br/imovel/aluguel/vaga-de-garagem-para-alugar-no-centro-rio-de-janeiro-rj/2226018
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328635
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328636
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328638
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3402745
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2774186
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3234343
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3353928
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226182
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3304482
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3852175
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3224300
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3762899
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3351978
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741635
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1824592
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1844374
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328708
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328853
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1788374
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808091
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1808094
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3236688
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3237010
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3402257
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226005
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3551681
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3069230
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/3896082
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/3896069
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2936659
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631180
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895832
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3405849
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226152
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631137
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2225994
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895960
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896022
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328701
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896055
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3418824
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226199
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3407001
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1583538
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3234041
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3291961
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741580
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2774210
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226193
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226072
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2493746
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226089
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2449765
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741456
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2491769
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3234564
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3434753
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2774170
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3977650
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3359999
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3580372
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3082287
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3234085
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741559
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3421791
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631111
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631224
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631090
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3380974
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2116380
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2226094
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2225964
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2225966
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2774197
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883531
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3749252
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3959695
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2225975
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3053222
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3381127
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3381885
    https://www.casamineira.com.br/imovel/aluguel/predio-para-alugar-no-centro-rio-de-janeiro-rj/3671111
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3381913
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3708735
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3819510
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3780865
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3052743
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3744639
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3381802
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3376941
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3381342
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3353933
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3380642
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3380730
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2934319
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3188358
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3360792
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3895888
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3980926
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631052
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631207
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2631226
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631241
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2897155
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328695
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328699
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/1328845
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3453664
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328883
    https://www.casamineira.com.br/imovel/aluguel/casa-para-alugar-no-centro-rio-de-janeiro-rj/2631187
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328897
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328901
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/2507541
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2961868
    https://www.casamineira.com.br/imovel/aluguel/apartamento-2-quartos-para-alugar-no-centro-rio-de-janeiro-rj/2115975
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328904
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328817
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328596
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328652
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328653
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328687
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3427023
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1669253
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1654582
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3759809
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3762446
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897709
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3400561
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328876
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328863
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3633633
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631179
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897244
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897729
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3895896
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3895983
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3896091
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3896176
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883157
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883169
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328610
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328611
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328613
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897094
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897365
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897406
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897448
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897538
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897574
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897622
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897649
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897672
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897759
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328925
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328926
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328927
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328928
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883051
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883158
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3883203
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897354
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897422
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897561
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897587
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631266
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3895937
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3896155
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2946173
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/935639
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328874
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328875
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328868
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328921
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328922
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/935635
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631197
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631225
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2631230
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741372
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897353
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897724
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741404
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741558
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741612
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741369
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741636
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741593
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897270
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328729
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328943
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1548555
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897360
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897418
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897460
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897471
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897480
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897721
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897772
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897461
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897630
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2897698
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328647
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3831210
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3025304
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/2820199
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3926595
    https://www.casamineira.com.br/imovel/aluguel/vaga-de-garagem-para-alugar-no-centro-rio-de-janeiro-rj/2226067
    https://www.casamineira.com.br/imovel/aluguel/vaga-de-garagem-para-alugar-no-centro-rio-de-janeiro-rj/2226083
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328637
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3741595
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328777
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328778
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/1328779
    https://www.casamineira.com.br/imovel/aluguel/apartamento-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3069615
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3376943
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3381638
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3381656
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/2969944
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/3896033
    https://www.casamineira.com.br/imovel/aluguel/sala-andar-para-alugar-no-centro-rio-de-janeiro-rj/3987715
    https://www.casamineira.com.br/imovel/aluguel/loja-para-alugar-no-centro-rio-de-janeiro-rj/3987716
    https://www.casamineira.com.br/imovel/aluguel/casa-1-quarto-para-alugar-no-centro-rio-de-janeiro-rj/1669254



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

    Casa de 0 quartos, 785m² para alugar no Centro R$54.984 R$19.786 R$3.203 785 m² 0 quartos 0 suítes 4 banheiros 2 vagas Tem elevador
    Apartamento de 1 quarto, 39m² para alugar no Centro R$1.300 R$170 R$73 39 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Vaga de Garagem de 19m² para alugar no Centro R$150 R$395 R$92 19 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Casa de 18 quartos, 1.206m² para alugar no Centro R$10.000 Não informado R$4.257 1206 m² 18 quartos 0 suítes 6 banheiros 0 vagas None
    Apartamento de 1 quarto, 25m² para alugar no Centro R$1.490 R$390 R$23 25 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 2 quartos, 53m² para alugar no Centro R$1.500 R$540 R$50 53 m² 2 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 62m² para alugar no Centro R$1.400 R$561 R$72 62 m² 1 quarto 0 suítes 2 banheiros 1 vaga Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$700 R$590 R$164 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 43m² para alugar no Centro R$2.100 R$600 R$105 43 m² 1 quarto 0 suítes 1 banheiro 1 vaga None
    Apartamento de 1 quarto, 25m² para alugar no Centro R$1.700 R$400 Não informado 25 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Prédio de 3.583m² para alugar no Centro R$250.837 Não informado Não informado 3583 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 413m² para alugar no Centro R$12.500 R$3.406 R$15.883 413 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 324m² para alugar no Centro R$19.356 R$4.200 R$2.886 324 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Prédio de 4.835m² para alugar no Centro R$230.000 R$60.000 R$21.552 4835 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 360m² para alugar no Centro R$10.000 R$7.813 R$4.826 360 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 141m² para alugar no Centro R$20.000 Não informado Não informado 141 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Loja de 100m² para alugar no Centro R$3.000 R$1.011 R$543 100 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Prédio de 3.565m² para alugar no Centro R$6.000 Não informado R$3.312 3565 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 290m² para alugar no Centro R$35.000 Não informado R$1.100 290 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 320m² para alugar no Centro R$19.356 R$4.200 R$2.851 320 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Loja de 483m² para alugar no Centro R$19.356 R$4.200 R$2.851 483 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Apartamento de 0 quartos, 25m² para alugar no Centro R$700 R$300 Não informado 25 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 20m² para alugar no Centro R$800 R$338 R$20 20 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Loja de 111m² para alugar no Centro R$4.000 Não informado R$357 111 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 50m² para alugar no Centro R$5.500 Não informado R$462 50 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 2.650m² para alugar no Centro R$85.000 Não informado Não informado 2650 m² 0 quartos 0 suítes 8 banheiros 0 vagas Tem elevador
    Prédio de 1.500m² para alugar no Centro R$7.500 Não informado R$4.166 1500 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 250m² para alugar no Centro R$4.000 Não informado Não informado 250 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 165m² para alugar no Centro R$4.000 Não informado R$1.292 165 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 94m² para alugar no Centro R$4.500 R$2.000 R$746 94 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Prédio de 2.000m² para alugar no Centro R$60.000 Não informado R$11.000 2000 m² 0 quartos 0 suítes 12 banheiros 6 vagas Tem elevador
    Prédio de 1.981m² para alugar no Centro R$60.000 Não informado R$11.000 1981 m² 0 quartos 0 suítes 10 banheiros 6 vagas None
    Loja de 1.042m² para alugar no Centro R$15.000 R$8.600 R$2.500 1042 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Loja de 177m² para alugar no Centro R$8.000 R$1.468 R$1.235 177 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 200m² para alugar no Centro R$10.000 Não informado R$1.092 200 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 1.300m² para alugar no Centro R$60.000 Não informado R$11.274 1300 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Loja de 384m² para alugar no Centro R$12.000 Não informado R$1.800 384 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 154m² para alugar no Centro R$30.000 Não informado R$93 154 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 262m² para alugar no Centro R$10.480 R$5.220 R$1.511 262 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Loja de 262m² para alugar no Centro R$10.480 R$5.220 R$1.511 262 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Loja de 727m² para alugar no Centro R$50.000 R$4.800 R$7.335 727 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Loja de 491m² para alugar no Centro R$9.000 Não informado R$93 491 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 722m² para alugar no Centro R$20.000 Não informado R$5.820 722 m² 0 quartos 0 suítes 5 banheiros 0 vagas None
    Sala-andar de 45m² para alugar no Centro R$1.050 R$900 R$220 45 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 887m² para alugar no Centro R$45.000 Não informado R$81.208 887 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Prédio de 3.000m² para alugar no Centro R$130.000 R$38.156 R$13.090 3000 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Prédio de 4.000m² para alugar no Centro R$80.000 Não informado R$4.325 4000 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 226m² para alugar no Centro R$16.500 Não informado R$667 226 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 486m² para alugar no Centro R$50.000 Não informado R$631 486 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 91m² para alugar no Centro R$20.000 Não informado R$1.323 91 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 29m² para alugar no Centro R$350 R$560 R$168 29 m² 0 quartos 0 suítes 1 banheiro 1 vaga None
    Loja de 1.500m² para alugar no Centro R$100.000 Não informado Não informado 1500 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Apartamento de 3 quartos, 93m² para alugar no Centro R$1.300 R$1.030 R$445 93 m² 3 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 577m² para alugar no Centro R$19.000 Não informado Não informado 577 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Loja de 537m² para alugar no Centro R$18.000 Não informado R$1.600 537 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Apartamento de 2 quartos, 70m² para alugar no Centro R$1.600 R$759 R$341 70 m² 2 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 60m² para alugar no Centro R$1.100 R$692 R$296 60 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 70m² para alugar no Centro R$1.100 R$840 R$230 70 m² 1 quarto 0 suítes 0 banheiros 0 vagas None
    Apartamento de 1 quarto, 60m² para alugar no Centro R$1.150 R$692 R$296 60 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 35m² para alugar no Centro R$1.000 R$400 Não informado 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 38m² para alugar no Centro R$1.400 R$322 Não informado 38 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Casa de 0 quartos, 95m² para alugar no Centro R$2.390 R$1.649 R$713 95 m² 0 quartos 0 suítes 3 banheiros 1 vaga None
    Prédio de 650m² para alugar no Centro R$30.000 Não informado Não informado 650 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Prédio de 675m² para alugar no Centro R$35.000 Não informado Não informado 675 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Prédio de 800m² para alugar no Centro R$25.000 Não informado R$971 800 m² 0 quartos 0 suítes 8 banheiros 0 vagas Tem elevador
    Prédio de 1.000m² para alugar no Centro R$26.000 Não informado Não informado 1000 m² 0 quartos 0 suítes 12 banheiros 0 vagas Tem elevador
    Loja de 11m² para alugar no Centro R$4.500 Não informado R$171 11 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 10m² para alugar no Centro R$4.500 Não informado R$124 10 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Casa de 0 quartos, 580m² para alugar no Centro R$32.000 R$16.000 R$3.296 580 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Loja de 28m² para alugar no Centro R$6.500 Não informado R$224 28 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 17m² para alugar no Centro R$5.500 Não informado R$124 17 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Casa de 0 quartos, 258m² para alugar no Centro R$6.500 R$4.139 R$1.175 258 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Loja de 42m² para alugar no Centro R$8.500 R$2.555 R$522 42 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 30m² para alugar no Centro R$450 R$590 R$151 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 30m² para alugar no Centro R$500 R$572 R$78 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 40m² para alugar no Centro R$500 R$410 R$140 40 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 130m² para alugar no Centro R$3.350 R$2.500 R$720 130 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Casa de 0 quartos, 30m² para alugar no Centro R$500 R$680 Não informado 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 36m² para alugar no Centro R$500 R$1.178 R$216 36 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 37m² para alugar no Centro R$7.500 Não informado R$852 37 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    None None None None None None None None None None
    Sala-andar de 23m² para alugar no Centro R$700 R$108 R$89 23 m² 0 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 30m² para alugar no Centro R$500 R$600 R$227 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 150m² para alugar no Centro R$10.000 Não informado R$54 150 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 64m² para alugar no Centro R$1.200 R$1.148 R$302 64 m² 0 quartos 0 suítes 2 banheiros 1 vaga Tem elevador
    Sala-andar de 30m² para alugar no Centro R$700 R$580 R$113 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 32m² para alugar no Centro R$700 R$550 R$180 32 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 30m² para alugar no Centro R$600 R$308 R$201 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 38m² para alugar no Centro R$700 R$639 R$126 38 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 40m² para alugar no Centro R$700 R$680 R$218 40 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    None None None None None None None None None None
    Sala-andar de 56m² para alugar no Centro R$700 R$700 R$222 56 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 37m² para alugar no Centro R$750 R$1.694 R$269 37 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 34m² para alugar no Centro R$800 R$524 R$232 34 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 71m² para alugar no Centro R$1.250 R$3.150 R$289 71 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 126m² para alugar no Centro R$3.800 R$1.375 Não informado 126 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 27m² para alugar no Centro R$750 R$1.300 R$157 27 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Galpão de 3.000m² para alugar no Centro R$180.000 Não informado R$800 3000 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Casa de 0 quartos, 406m² para alugar no Centro R$8.900 R$8.526 Não informado 406 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 52m² para alugar no Centro R$1.200 R$750 R$280 52 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 70m² para alugar no Centro R$2.000 R$600 R$900 70 m² 1 quarto 0 suítes 2 banheiros 0 vagas Tem elevador
    Loja de 44m² para alugar no Centro R$3.500 R$800 R$234 44 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 86m² para alugar no Centro R$1.300 R$1.187 R$412 86 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 61m² para alugar no Centro R$1.300 R$1.064 R$240 61 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 28m² para alugar no Centro R$500 R$555 R$101 28 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 37m² para alugar no Centro R$500 R$746 R$116 37 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 40m² para alugar no Centro R$500 R$754 R$121 40 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 29m² para alugar no Centro R$500 R$538 R$103 29 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 36m² para alugar no Centro R$1.200 R$1.294 R$83 36 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Prédio de 9.200m² para alugar no Centro R$476.000 Não informado R$45.151 9200 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 79m² para alugar no Centro R$18.000 Não informado R$1.124 79 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 37m² para alugar no Centro R$500 R$1.326 R$282 37 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 70m² para alugar no Centro R$9.000 Não informado R$767 70 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 0 quartos, 20m² para alugar no Centro R$500 R$261 Não informado 20 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 50m² para alugar no Centro R$1.400 R$990 R$310 50 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 28m² para alugar no Centro R$1.400 R$489 R$238 28 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 37m² para alugar no Centro R$8.000 Não informado R$297 37 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 57m² para alugar no Centro R$8.500 R$1.793 R$748 57 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 38m² para alugar no Centro R$8.500 R$1.827 R$463 38 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 36m² para alugar no Centro R$600 R$550 Não informado 36 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 56m² para alugar no Centro R$600 R$680 Não informado 56 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 1.198m² para alugar no Centro R$35.000 Não informado R$8.278 1198 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Apartamento de 0 quartos, 18m² para alugar no Centro R$500 R$511 Não informado 18 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 638m² para alugar no Centro R$20.400 Não informado R$4.418 638 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 560m² para alugar no Centro R$16.800 Não informado R$3.860 560 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 320m² para alugar no Centro R$12.000 R$2.300 Não informado 320 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 40m² para alugar no Centro R$800 R$430 R$136 40 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 95m² para alugar no Centro R$1.100 Não informado R$220 95 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Apartamento de 1 quarto, 38m² para alugar no Centro R$1.550 R$500 Não informado 38 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 120m² para alugar no Centro R$1.500 R$3.800 R$724 120 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 81m² para alugar no Centro R$2.900 R$3.290 R$704 81 m² 0 quartos 0 suítes 3 banheiros 2 vagas None
    Sala-andar de 72m² para alugar no Centro R$1.500 R$1.200 R$394 72 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 154m² para alugar no Centro R$1.500 R$5.100 R$559 154 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 70m² para alugar no Centro R$1.600 R$1.950 R$580 70 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 84m² para alugar no Centro R$2.300 R$2.132 R$577 84 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 89m² para alugar no Centro R$1.600 R$3.270 R$537 89 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 115m² para alugar no Centro R$2.000 R$3.646 R$808 115 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 129m² para alugar no Centro R$2.000 R$1.034 R$762 129 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 119m² para alugar no Centro R$2.200 R$4.371 R$774 119 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Sala-andar de 65m² para alugar no Centro R$1.900 R$13 R$396 65 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 100m² para alugar no Centro R$2.100 R$1.875 R$491 100 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 60m² para alugar no Centro R$1.800 R$891 R$263 60 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 65m² para alugar no Centro R$2.500 R$980 R$275 65 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 66m² para alugar no Centro R$2.500 R$791 R$299 66 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 55m² para alugar no Centro R$1.540 R$1.060 R$340 55 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 34m² para alugar no Centro R$1.900 R$344 R$1.049 34 m² 0 quartos 0 suítes 1 banheiro 1 vaga None
    Sala-andar de 59m² para alugar no Centro R$1.900 R$1.280 R$340 59 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 155m² para alugar no Centro R$2.800 R$2.657 R$729 155 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 60m² para alugar no Centro R$2.800 R$821 R$240 60 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 423m² para alugar no Centro R$3.000 R$8.683 R$2.704 423 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 124m² para alugar no Centro R$3.500 R$1.525 R$267 124 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 330m² para alugar no Centro R$4.000 R$8.760 R$1.770 330 m² 0 quartos 0 suítes 6 banheiros 1 vaga None
    Sala-andar de 74m² para alugar no Centro R$3.000 R$1.050 R$2.626 74 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 94m² para alugar no Centro R$3.000 R$1.006 R$491 94 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Sala-andar de 80m² para alugar no Centro R$3.500 R$3.443 R$459 80 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 105m² para alugar no Centro R$3.000 R$2.100 R$628 105 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    None None None None None None None None None None
    Sala-andar de 109m² para alugar no Centro R$3.000 R$700 R$281 109 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 13m² para alugar no Centro R$400 R$426 Não informado 13 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 115m² para alugar no Centro R$3.900 Não informado R$146 115 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 34m² para alugar no Centro R$450 R$403 R$194 34 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 33m² para alugar no Centro R$450 R$392 R$165 33 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 0 quartos, 25m² para alugar no Centro R$700 R$217 Não informado 25 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Vaga de Garagem de 16m² para alugar no Centro R$500 Não informado R$83 16 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 438m² para alugar no Centro R$7.500 R$5.213 R$2.127 438 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 21m² para alugar no Centro R$550 R$416 R$102 21 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 30m² para alugar no Centro R$550 R$350 R$220 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 28m² para alugar no Centro R$600 R$1.079 R$89 28 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 21m² para alugar no Centro R$700 R$558 R$91 21 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 34m² para alugar no Centro R$680 R$348 R$131 34 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 50m² para alugar no Centro R$750 R$1.370 R$223 50 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 42m² para alugar no Centro R$915 R$1.646 R$179 42 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 191m² para alugar no Centro R$3.000 R$3.727 R$646 191 m² 0 quartos 0 suítes 6 banheiros 0 vagas Tem elevador
    Sala-andar de 49m² para alugar no Centro R$1.051 R$1.888 R$86 49 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 22m² para alugar no Centro R$800 R$264 R$84 22 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 21m² para alugar no Centro R$800 R$425 R$110 21 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 33m² para alugar no Centro R$800 R$515 Não informado 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 33m² para alugar no Centro R$500 R$600 R$192 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 24m² para alugar no Centro R$500 R$700 R$94 24 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 66m² para alugar no Centro R$1.500 R$2.328 R$405 66 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 25m² para alugar no Centro R$350 R$346 R$1.250 25 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Apartamento de 1 quarto, 20m² para alugar no Centro R$1.300 R$400 Não informado 20 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 35m² para alugar no Centro R$500 R$625 R$177 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$500 R$750 R$125 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 24m² para alugar no Centro R$500 R$711 R$101 24 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 40m² para alugar no Centro R$594 R$550 R$100 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 90m² para alugar no Centro R$1.700 R$1.390 R$517 90 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 60m² para alugar no Centro R$1.400 R$1.275 R$175 60 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 40m² para alugar no Centro R$890 R$433 Não informado 40 m² 1 quarto 1 suíte 1 banheiro 0 vagas None
    Galpão de 3.000m² para alugar no Centro R$80.000 Não informado R$1.000 3000 m² 0 quartos 0 suítes 0 banheiros 5 vagas None
    Apartamento de 2 quartos, 100m² para alugar no Centro R$2.000 R$800 R$270 100 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 309m² para alugar no Centro R$6.000 Não informado R$2.400 309 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 208m² para alugar no Centro R$6.000 Não informado R$830 208 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 24m² para alugar no Centro R$514 R$925 R$89 24 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Casa de 0 quartos, 118m² para alugar no Centro R$4.000 Não informado R$394 118 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 156m² para alugar no Centro R$3.500 R$1.764 Não informado 156 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Apartamento de 0 quartos, 30m² para alugar no Centro R$1.000 R$320 R$25 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 27m² para alugar no Centro R$500 R$800 R$25 27 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 611m² para alugar no Centro R$8.000 Não informado R$1.710 611 m² 0 quartos 0 suítes 7 banheiros 0 vagas None
    Loja de 300m² para alugar no Centro R$27.000 R$4.452 R$1.034 300 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Loja de 140m² para alugar no Centro R$15.000 R$650 R$115 140 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$900 R$706 R$133 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 22m² para alugar no Centro R$400 R$400 Não informado 22 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 30m² para alugar no Centro R$500 R$550 R$50 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$500 R$650 R$130 30 m² 1 quarto 1 suíte 1 banheiro 1 vaga Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$500 R$589 R$75 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 34m² para alugar no Centro R$500 R$700 R$178 34 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$500 R$406 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 31m² para alugar no Centro R$560 R$450 Não informado 31 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 21m² para alugar no Centro R$500 R$360 R$76 21 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 32m² para alugar no Centro R$500 R$560 R$191 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 1.096m² para alugar no Centro R$75.000 R$18.632 R$2.192 1096 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 1.299m² para alugar no Centro R$90.000 R$19.485 R$5.196 1299 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 43m² para alugar no Centro R$570 R$704 R$222 43 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$580 R$486 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$500 R$780 R$73 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 250m² para alugar no Centro R$7.000 Não informado R$600 250 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Casa de 1 quarto, 40m² para alugar no Centro R$1.040 R$295 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 690m² para alugar no Centro R$10.000 R$17.042 R$2.576 690 m² 0 quartos 0 suítes 6 banheiros 0 vagas Tem elevador
    Loja de 105m² para alugar no Centro R$7.000 R$1.873 R$494 105 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 40m² para alugar no Centro R$1.180 R$379 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Casa de 1 quarto, 66m² para alugar no Centro R$610 R$858 R$122 66 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 28m² para alugar no Centro R$750 R$662 R$174 28 m² 0 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Casa de 1 quarto, 27m² para alugar no Centro R$630 R$430 Não informado 27 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 462m² para alugar no Centro R$21.000 R$5.311 R$1.951 462 m² 0 quartos 0 suítes 5 banheiros 0 vagas None
    Apartamento de 1 quarto, 80m² para alugar no Centro R$1.190 R$1.030 R$387 80 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$618 R$490 R$122 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 25m² para alugar no Centro R$600 R$442 R$17 25 m² 1 quarto 0 suítes 1 banheiro 1 vaga Tem elevador
    Casa de 1 quarto, 31m² para alugar no Centro R$600 R$900 Não informado 31 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 25m² para alugar no Centro R$610 R$442 Não informado 25 m² 1 quarto 0 suítes 1 banheiro 1 vaga Tem elevador
    Apartamento de 1 quarto, 33m² para alugar no Centro R$900 R$480 R$23 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 250m² para alugar no Centro R$5.000 Não informado R$1.100 250 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    None None None None None None None None None None
    Apartamento de 1 quarto, 90m² para alugar no Centro R$810 R$470 R$45 90 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 14 quartos, 710m² para alugar no Centro R$5.552 Não informado R$71 710 m² 14 quartos 1 suíte 5 banheiros 0 vagas None
    Sala-andar de 438m² para alugar no Centro R$4.500 R$5.213 R$2.304 438 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 33m² para alugar no Centro R$700 R$1.300 Não informado 33 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 31m² para alugar no Centro R$650 R$600 Não informado 31 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 32m² para alugar no Centro R$600 R$562 R$684 32 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 54m² para alugar no Centro R$2.000 R$781 Não informado 54 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 30m² para alugar no Centro R$700 R$594 Não informado 30 m² 0 quartos 0 suítes 1 banheiro 1 vaga None
    Sala-andar de 60m² para alugar no Centro R$1.150 R$692 R$296 60 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 38m² para alugar no Centro R$990 R$451 R$274 38 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 22m² para alugar no Centro R$800 R$538 R$150 22 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Cobertura de 2 quartos, 99m² para alugar no Centro R$1.990 R$150 Não informado 99 m² 2 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 296m² para alugar no Centro R$5.000 R$6.574 R$2.247 296 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Apartamento de 1 quarto, 43m² para alugar no Centro R$870 R$433 Não informado 43 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 33m² para alugar no Centro R$700 R$521 R$103 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 33m² para alugar no Centro R$680 R$850 Não informado 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 26m² para alugar no Centro R$680 R$486 Não informado 26 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Galpão de 2.650m² para alugar no Centro R$159.000 Não informado R$800 2650 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 93m² para alugar no Centro R$1.300 R$1.080 R$445 93 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 310m² para alugar no Centro R$4.000 R$5.960 R$2.354 310 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 290m² para alugar no Centro R$6.500 R$6.350 R$1.200 290 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 190m² para alugar no Centro R$4.500 R$2.447 R$860 190 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Apartamento de 2 quartos, 90m² para alugar no Centro R$2.200 R$550 Não informado 90 m² 2 quartos 1 suíte 1 banheiro 0 vagas None
    Sala-andar de 423m² para alugar no Centro R$4.500 R$8.683 R$2.704 423 m² 0 quartos 0 suítes 10 banheiros 0 vagas None
    Sala-andar de 260m² para alugar no Centro R$4.500 R$3.900 R$720 260 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Loja de 860m² para alugar no Centro R$7.500 Não informado R$89 860 m² 0 quartos 0 suítes 3 banheiros 10 vagas None
    Sala-andar de 50m² para alugar no Centro R$500 R$1.400 Não informado 50 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 2.157m² para alugar no Centro R$118.670 R$58.472 Não informado 2157 m² 0 quartos 0 suítes 14 banheiros 0 vagas None
    Prédio de 300m² para alugar no Centro R$5.000 R$2.919 Não informado 300 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 179m² para alugar no Centro R$5.500 R$2.960 R$560 179 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Casa de 1 quarto, 20m² para alugar no Centro R$720 R$390 Não informado 20 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$740 R$300 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 364m² para alugar no Centro R$5.824 R$5.467 R$2.464 364 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 254m² para alugar no Centro R$5.800 R$6.300 R$2.074 254 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 320m² para alugar no Centro R$6.000 R$8.800 R$2.100 320 m² 0 quartos 0 suítes 4 banheiros 4 vagas None
    Sala-andar de 400m² para alugar no Centro R$6.000 R$6.080 R$1.286 400 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 156m² para alugar no Centro R$6.000 R$2.450 R$670 156 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 240m² para alugar no Centro R$5.000 R$7.000 R$1.221 240 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 185m² para alugar no Centro R$6.000 R$5.200 R$1.490 185 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 259m² para alugar no Centro R$5.900 R$2.940 R$1.194 259 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 360m² para alugar no Centro R$5.000 R$4.233 R$1.232 360 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 145m² para alugar no Centro R$5.500 R$3.914 R$1.075 145 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 40m² para alugar no Centro R$772 R$431 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 32m² para alugar no Centro R$782 R$390 R$100 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Casa de 1 quarto, 25m² para alugar no Centro R$800 R$398 Não informado 25 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 50m² para alugar no Centro R$1.072 R$1.927 R$89 50 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 54m² para alugar no Centro R$1.158 R$2.081 R$89 54 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 200m² para alugar no Centro R$5.800 R$4.274 R$920 200 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 254m² para alugar no Centro R$6.000 R$7.118 R$1.989 254 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 200m² para alugar no Centro R$5.000 R$7.826 R$1.035 200 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 33m² para alugar no Centro R$500 R$830 R$190 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 59m² para alugar no Centro R$1.265 R$2.274 R$89 59 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 100m² para alugar no Centro R$6.000 R$2.000 Não informado 100 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 130m² para alugar no Centro R$6.000 R$2.000 Não informado 130 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 29m² para alugar no Centro R$770 R$380 R$24 29 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 403m² para alugar no Centro R$7.000 R$6.313 R$3.102 403 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$728 R$500 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 100m² para alugar no Centro R$1.500 R$1.091 R$553 100 m² 0 quartos 0 suítes 2 banheiros 1 vaga None
    Apartamento de 1 quarto, 50m² para alugar no Centro R$748 R$1.140 R$59 50 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 30m² para alugar no Centro R$2.757 R$848 R$112 30 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 690m² para alugar no Centro R$15.000 Não informado R$2.700 690 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Casa de 1 quarto, 27m² para alugar no Centro R$800 R$390 R$26 27 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$800 R$380 R$132 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 431m² para alugar no Centro R$18.000 R$4.698 R$4.881 431 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 200m² para alugar no Centro R$2.200 R$2.607 R$781 200 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 140m² para alugar no Centro R$2.600 R$2.600 R$1.045 140 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 88m² para alugar no Centro R$1.889 R$3.396 R$179 88 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 25m² para alugar no Centro R$820 R$350 R$23 25 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$810 R$456 R$94 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 28m² para alugar no Centro R$820 R$400 R$21 28 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 32m² para alugar no Centro R$810 R$545 R$99 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 32m² para alugar no Centro R$815 R$456 R$92 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 32m² para alugar no Centro R$900 R$453 R$100 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 31m² para alugar no Centro R$850 R$300 Não informado 31 m² 1 quarto 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 197m² para alugar no Centro R$4.000 R$2.226 Não informado 197 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Loja de 643m² para alugar no Centro R$50.000 R$8.359 R$7.908 643 m² 0 quartos 0 suítes 4 banheiros 4 vagas Tem elevador
    Casa de 1 quarto, 17m² para alugar no Centro R$932 R$300 R$21 17 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 197m² para alugar no Centro R$12.500 R$4.900 R$1.700 197 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Loja de 600m² para alugar no Centro R$20.000 Não informado R$3.200 600 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Loja de 525m² para alugar no Centro R$12.000 Não informado R$4.045 525 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Loja de 372m² para alugar no Centro R$26.077 Não informado Não informado 372 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 379m² para alugar no Centro R$26.565 Não informado Não informado 379 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 494m² para alugar no Centro R$34.615 Não informado Não informado 494 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 702m² para alugar no Centro R$49.179 Não informado Não informado 702 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    None None None None None None None None None None
    Sala-andar de 49m² para alugar no Centro R$500 R$500 R$190 49 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 26m² para alugar no Centro R$850 R$506 Não informado 26 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 72m² para alugar no Centro R$2.500 R$511 R$393 72 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 276m² para alugar no Centro R$2.500 R$5.550 R$1.678 276 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 40m² para alugar no Centro R$880 R$350 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$880 R$620 R$144 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 47m² para alugar no Centro R$1.500 R$952 R$353 47 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$825 R$453 R$100 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$820 R$453 R$100 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 28m² para alugar no Centro R$810 R$456 R$79 28 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 60m² para alugar no Centro R$1.400 R$3.300 Não informado 60 m² 0 quartos 0 suítes 0 banheiros 2 vagas None
    Casa de 1 quarto, 39m² para alugar no Centro R$997 R$450 Não informado 39 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 28m² para alugar no Centro R$980 R$362 Não informado 28 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 135m² para alugar no Centro R$3.400 R$1.500 R$863 135 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 160m² para alugar no Centro R$3.000 R$1.450 R$741 160 m² 0 quartos 0 suítes 2 banheiros 1 vaga Tem elevador
    Sala-andar de 58m² para alugar no Centro R$2.000 R$880 R$343 58 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Apartamento de 1 quarto, 33m² para alugar no Centro R$890 R$538 Não informado 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 56m² para alugar no Centro R$1.500 R$734 R$293 56 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 350m² para alugar no Centro R$7.900 Não informado Não informado 350 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    None None None None None None None None None None
    Sala-andar de 135m² para alugar no Centro R$3.600 R$1.500 R$863 135 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 135m² para alugar no Centro R$3.500 R$1.350 R$683 135 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 140m² para alugar no Centro R$3.500 R$1.300 R$992 140 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 148m² para alugar no Centro R$3.000 R$1.450 R$741 148 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 22m² para alugar no Centro R$1.060 R$500 Não informado 22 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 40m² para alugar no Centro R$982 R$300 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 38m² para alugar no Centro R$1.000 R$431 R$172 38 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 25m² para alugar no Centro R$999 R$430 R$21 25 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$990 R$204 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 60m² para alugar no Centro R$1.200 R$900 R$81 60 m² 1 quarto 0 suítes 2 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 35m² para alugar no Centro R$1.020 R$498 R$80 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 23m² para alugar no Centro R$1.015 R$300 Não informado 23 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$900 R$340 R$20 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 33m² para alugar no Centro R$1.300 R$350 Não informado 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$1.250 R$350 Não informado 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Casa de 1 quarto, 31m² para alugar no Centro R$1.100 R$689 Não informado 31 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$1.190 R$400 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 33m² para alugar no Centro R$1.400 R$350 Não informado 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$1.500 R$350 Não informado 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 37m² para alugar no Centro R$1.500 R$350 Não informado 37 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 35m² para alugar no Centro R$900 R$470 R$126 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 34m² para alugar no Centro R$1.500 R$350 Não informado 34 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 25m² para alugar no Centro R$1.200 R$400 R$22 25 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$1.000 R$500 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 45m² para alugar no Centro R$1.300 R$400 Não informado 45 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 28m² para alugar no Centro R$1.230 R$300 R$156 28 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 20m² para alugar no Centro R$1.370 R$332 R$21 20 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$1.190 R$377 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 22m² para alugar no Centro R$1.340 R$270 R$20 22 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Sala-andar de 37m² para alugar no Centro R$600 R$930 Não informado 37 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 60m² para alugar no Centro R$950 R$850 R$76 60 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 65m² para alugar no Centro R$1.000 R$770 R$71 65 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 75m² para alugar no Centro R$1.000 R$769 R$71 75 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$926 R$627 Não informado 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 3 quartos, 130m² para alugar no Centro R$2.600 R$800 R$292 130 m² 3 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 42m² para alugar no Centro R$1.120 R$650 Não informado 42 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 21m² para alugar no Centro R$1.108 R$365 Não informado 21 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 60m² para alugar no Centro R$970 R$547 R$156 60 m² 2 quartos 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 35m² para alugar no Centro R$1.470 R$528 Não informado 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 35m² para alugar no Centro R$1.615 R$530 R$16 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$1.420 R$510 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 13m² para alugar no Centro R$1.100 R$350 Não informado 13 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 28m² para alugar no Centro R$1.200 R$480 Não informado 28 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 27m² para alugar no Centro R$1.190 R$30 R$32 27 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 42m² para alugar no Centro R$1.300 R$861 R$56 42 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$1.275 R$486 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 48m² para alugar no Centro R$960 R$438 Não informado 48 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 34m² para alugar no Centro R$1.490 R$680 R$70 34 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$1.400 R$628 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 56m² para alugar no Centro R$1.365 R$556 R$54 56 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 191m² para alugar no Centro R$7.000 R$5.741 R$1.445 191 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 321m² para alugar no Centro R$7.500 R$5.960 R$2.432 321 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 231m² para alugar no Centro R$7.000 R$3.300 R$1.577 231 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Apartamento de 1 quarto, 32m² para alugar no Centro R$980 R$320 Não informado 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 32m² para alugar no Centro R$1.700 R$500 Não informado 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 50m² para alugar no Centro R$1.315 R$470 R$56 50 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 38m² para alugar no Centro R$3.400 R$650 R$250 38 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 35m² para alugar no Centro R$1.350 R$725 R$67 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 41m² para alugar no Centro R$1.050 R$505 R$21 41 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.279 R$300 R$25 40 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.550 R$430 R$45 40 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$1.300 R$330 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.420 R$480 R$50 40 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Sala-andar de 32m² para alugar no Centro R$350 R$1.124 R$218 32 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 200m² para alugar no Centro R$7.000 R$7.832 R$996 200 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 185m² para alugar no Centro R$7.000 R$1.483 R$1.014 185 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 60m² para alugar no Centro R$1.130 R$600 R$75 60 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 70m² para alugar no Centro R$1.420 R$500 Não informado 70 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 45m² para alugar no Centro R$1.084 R$450 R$20 45 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 34m² para alugar no Centro R$1.050 R$610 Não informado 34 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 48m² para alugar no Centro R$1.020 R$600 R$50 48 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 45m² para alugar no Centro R$1.100 R$526 Não informado 45 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 60m² para alugar no Centro R$1.360 R$610 R$51 60 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 3 quartos, 90m² para alugar no Centro R$1.870 R$500 R$42 90 m² 3 quartos 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.810 R$480 Não informado 40 m² 1 quarto 1 suíte 1 banheiro 0 vagas None
    Sala-andar de 28m² para alugar no Centro R$300 R$412 R$408 28 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 32m² para alugar no Centro R$480 R$462 Não informado 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Loja de 2.031m² para alugar no Centro R$80.000 Não informado Não informado 2031 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Apartamento de 2 quartos, 70m² para alugar no Centro R$1.768 R$700 R$50 70 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    None R$1.105 R$450 R$17 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 45m² para alugar no Centro R$1.290 R$350 R$55 45 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$1.200 R$400 R$17 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 57m² para alugar no Centro R$1.156 R$430 R$150 57 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 23m² para alugar no Centro R$1.150 R$10 Não informado 23 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 50m² para alugar no Centro R$1.100 R$705 R$59 50 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 55m² para alugar no Centro R$1.120 R$700 R$53 55 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 39m² para alugar no Centro R$1.199 R$435 R$52 39 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 46m² para alugar no Centro R$1.150 R$620 R$87 46 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 52m² para alugar no Centro R$1.280 R$845 Não informado 52 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.250 R$400 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 45m² para alugar no Centro R$1.500 R$500 R$50 45 m² 2 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Apartamento de 1 quarto, 48m² para alugar no Centro R$1.250 R$480 Não informado 48 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 50m² para alugar no Centro R$1.232 R$400 Não informado 50 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 42m² para alugar no Centro R$1.530 R$724 R$92 42 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 42m² para alugar no Centro R$1.500 R$714 R$92 42 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$1.250 R$340 Não informado 32 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.450 R$500 Não informado 40 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 38m² para alugar no Centro R$1.650 R$430 R$20 38 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 42m² para alugar no Centro R$1.410 R$712 R$90 42 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 3 quartos, 94m² para alugar no Centro R$2.300 R$800 R$127 94 m² 3 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Apartamento de 2 quartos, 47m² para alugar no Centro R$1.785 R$360 R$52 47 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 54m² para alugar no Centro R$1.700 R$585 R$75 54 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 34m² para alugar no Centro R$1.800 R$610 R$74 34 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.860 R$552 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 1 vaga Tem elevador
    Loja de 494m² para alugar no Centro R$35.000 R$13.709 R$1.809 494 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    None None None None None None None None None None
    Apartamento de 3 quartos, 100m² para alugar no Centro R$2.200 R$850 R$150 100 m² 3 quartos 0 suítes 2 banheiros 1 vaga Tem elevador
    Apartamento de 3 quartos, 99m² para alugar no Centro R$2.500 R$780 R$138 99 m² 3 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 42m² para alugar no Centro R$1.940 R$293 Não informado 42 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 45m² para alugar no Centro R$2.500 Não informado R$92 45 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 43m² para alugar no Centro R$2.000 R$300 Não informado 43 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 40m² para alugar no Centro R$2.300 R$680 R$50 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 32m² para alugar no Centro R$2.180 R$700 R$155 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 45m² para alugar no Centro R$2.100 R$600 R$85 45 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 40m² para alugar no Centro R$2.288 R$575 R$21 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 75m² para alugar no Centro R$2.430 R$750 Não informado 75 m² 2 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Apartamento de 3 quartos, 120m² para alugar no Centro R$2.800 R$700 R$125 120 m² 3 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 110m² para alugar no Centro R$2.400 R$2.310 Não informado 110 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 66m² para alugar no Centro R$1.590 R$2.360 R$421 66 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Apartamento de 2 quartos, 63m² para alugar no Centro R$1.500 R$483 R$72 63 m² 2 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 2 quartos, 67m² para alugar no Centro R$1.400 R$465 R$105 67 m² 2 quartos 0 suítes 1 banheiro 1 vaga None
    Apartamento de 3 quartos, 60m² para alugar no Centro R$2.600 R$350 R$204 60 m² 3 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 85m² para alugar no Centro R$1.600 R$979 R$247 85 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Apartamento de 1 quarto, 42m² para alugar no Centro R$1.800 R$500 Não informado 42 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 45m² para alugar no Centro R$1.900 R$714 R$85 45 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 156m² para alugar no Centro R$6.240 R$1.077 R$749 156 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 47m² para alugar no Centro R$900 R$563 Não informado 47 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 19m² para alugar no Centro R$800 R$490 Não informado 19 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 20m² para alugar no Centro R$500 R$370 Não informado 20 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 30m² para alugar no Centro R$800 R$320 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$3.000 R$450 R$59 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 3 quartos, 70m² para alugar no Centro R$3.000 R$549 R$84 70 m² 3 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 589m² para alugar no Centro R$25.000 R$13.000 R$4.124 589 m² 0 quartos 0 suítes 7 banheiros 0 vagas Tem elevador
    Sala-andar de 671m² para alugar no Centro R$30.195 R$18.068 R$2.325 671 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 562m² para alugar no Centro R$35.000 R$11.066 R$3.589 562 m² 0 quartos 0 suítes 7 banheiros 0 vagas Tem elevador
    Sala-andar de 594m² para alugar no Centro R$50.000 R$16.000 R$3.199 594 m² 0 quartos 0 suítes 6 banheiros 0 vagas Tem elevador
    Sala-andar de 650m² para alugar no Centro R$55.000 R$4.800 R$1.500 650 m² 0 quartos 0 suítes 9 banheiros 0 vagas Tem elevador
    Sala-andar de 440m² para alugar no Centro R$16.000 R$4.857 R$2.448 440 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 37m² para alugar no Centro R$850 R$478 Não informado 37 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 46m² para alugar no Centro R$900 R$695 R$62 46 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 505m² para alugar no Centro R$17.000 R$6.349 R$15.318 505 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$13.000 R$7.693 R$1.827 270 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 300m² para alugar no Centro R$12.000 R$8.945 R$2.111 300 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 41m² para alugar no Centro R$1.000 R$425 Não informado 41 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 4 quartos, 105m² para alugar no Centro R$3.000 R$200 R$125 105 m² 4 quartos 3 suítes 3 banheiros 0 vagas None
    Casa de 1 quarto, 45m² para alugar no Centro R$4.000 Não informado Não informado 45 m² 1 quarto 1 suíte 1 banheiro 0 vagas None
    Sala-andar de 150m² para alugar no Centro R$3.400 R$3.150 Não informado 150 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    None None None None None None None None None None
    Prédio de 675m² para alugar no Centro R$20.250 Não informado R$5.900 675 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 600m² para alugar no Centro R$5.000 R$12.649 R$2.902 600 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 100m² para alugar no Centro R$3.300 R$1.350 R$480 100 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 22m² para alugar no Centro R$1.800 R$178 R$493 22 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 385m² para alugar no Centro R$8.000 R$5.120 R$2.542 385 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Prédio de 1.042m² para alugar no Centro R$28.000 Não informado R$7.033 1042 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 1.140m² para alugar no Centro R$51.335 R$19.317 R$4.015 1140 m² 0 quartos 0 suítes 2 banheiros 18 vagas Tem elevador
    Sala-andar de 187m² para alugar no Centro R$1.500 R$2.082 Não informado 187 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 1.007m² para alugar no Centro R$45.339 R$26.568 Não informado 1007 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 48m² para alugar no Centro R$600 R$800 Não informado 48 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 969m² para alugar no Centro R$87.255 R$26.893 R$2.666 969 m² 0 quartos 0 suítes 6 banheiros 18 vagas None
    Sala-andar de 928m² para alugar no Centro R$83.534 R$25.747 R$2.552 928 m² 0 quartos 0 suítes 6 banheiros 18 vagas None
    Sala-andar de 940m² para alugar no Centro R$84.643 R$26.089 R$2.586 940 m² 0 quartos 0 suítes 6 banheiros 18 vagas None
    Sala-andar de 1.236m² para alugar no Centro R$129.780 R$24.658 R$9.270 1236 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 1.306m² para alugar no Centro R$78.362 R$22.203 R$6.100 1306 m² 0 quartos 0 suítes 6 banheiros 5 vagas Tem elevador
    Sala-andar de 1.107m² para alugar no Centro R$66.456 R$18.164 R$6.080 1107 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 956m² para alugar no Centro R$86.089 R$26.534 R$2.630 956 m² 0 quartos 0 suítes 6 banheiros 18 vagas None
    Sala-andar de 1.195m² para alugar no Centro R$119.500 R$23.840 R$8.962 1195 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 1.110m² para alugar no Centro R$83.293 R$18.880 R$5.187 1110 m² 0 quartos 0 suítes 6 banheiros 4 vagas Tem elevador
    Sala-andar de 1.266m² para alugar no Centro R$139.260 R$25.256 R$9.495 1266 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 547m² para alugar no Centro R$25.000 R$13.600 R$2.846 547 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 511m² para alugar no Centro R$23.035 R$13.498 Não informado 511 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 350m² para alugar no Centro R$8.500 R$5.800 R$1.400 350 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 1.299m² para alugar no Centro R$103.929 R$19.486 R$3.897 1299 m² 0 quartos 0 suítes 8 banheiros 6 vagas Tem elevador
    Sala-andar de 920m² para alugar no Centro R$30.000 R$14.200 R$5.102 920 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Sala-andar de 39m² para alugar no Centro R$400 R$1.124 R$260 39 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    None None None None None None None None None None
    Sala-andar de 575m² para alugar no Centro R$24.000 R$16.000 R$3.425 575 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 253m² para alugar no Centro R$25.000 R$8.830 R$1.844 253 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 225m² para alugar no Centro R$16.000 R$4.300 R$820 225 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 581m² para alugar no Centro R$29.050 R$12.822 R$3.015 581 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 414m² para alugar no Centro R$16.000 R$8.971 R$1.086 414 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 698m² para alugar no Centro R$45.395 R$14.743 R$4.609 698 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 191m² para alugar no Centro R$8.500 R$4.649 R$1.322 191 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 375m² para alugar no Centro R$8.800 R$5.960 R$2.822 375 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 354m² para alugar no Centro R$20.000 R$8.500 R$3.000 354 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 155m² para alugar no Centro R$10.000 R$7.989 R$795 155 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 289m² para alugar no Centro R$10.000 R$5.955 R$1.266 289 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 539m² para alugar no Centro R$18.000 R$9.041 R$1.654 539 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 381m² para alugar no Centro R$11.000 R$11.497 R$1.489 381 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 553m² para alugar no Centro R$15.000 R$11.615 R$1.489 553 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 554m² para alugar no Centro R$35.000 R$9.589 R$3.024 554 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 243m² para alugar no Centro R$11.000 R$3.175 R$1.053 243 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 160m² para alugar no Centro R$9.000 R$4.300 R$820 160 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 326m² para alugar no Centro R$14.000 R$5.300 R$1.602 326 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 355m² para alugar no Centro R$15.000 R$3.000 R$1.200 355 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 321m² para alugar no Centro R$11.500 R$6.340 R$2.059 321 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 420m² para alugar no Centro R$13.000 R$7.795 R$1.722 420 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 190m² para alugar no Centro R$12.000 R$4.711 R$1.253 190 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Sala-andar de 677m² para alugar no Centro R$44.010 R$14.293 R$4.468 677 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 575m² para alugar no Centro R$24.000 R$16.000 R$3.425 575 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 292m² para alugar no Centro R$8.000 R$7.200 R$1.700 292 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 394m² para alugar no Centro R$17.800 R$7.070 R$1.874 394 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 553m² para alugar no Centro R$12.000 R$11.608 R$1.547 553 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 381m² para alugar no Centro R$9.000 R$11.489 R$1.547 381 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 196m² para alugar no Centro R$10.000 R$1.330 R$855 196 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 320m² para alugar no Centro R$12.000 R$3.905 R$1.912 320 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 222m² para alugar no Centro R$17.000 R$2.524 R$1.412 222 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 750m² para alugar no Centro R$28.500 R$13.220 R$5.432 750 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 354m² para alugar no Centro R$12.000 R$6.340 R$2.256 354 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 32m² para alugar no Centro R$500 R$370 R$150 32 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 30m² para alugar no Centro R$500 R$424 R$148 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 25m² para alugar no Centro R$500 R$500 R$458 25 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 391m² para alugar no Centro R$25.468 R$12.147 R$1.324 391 m² 0 quartos 0 suítes 4 banheiros 1 vaga None
    None None None None None None None None None None
    Sala-andar de 579m² para alugar no Centro R$46.335 R$8.687 R$1.737 579 m² 0 quartos 0 suítes 6 banheiros 3 vagas Tem elevador
    Sala-andar de 545m² para alugar no Centro R$17.000 R$7.860 R$1.521 545 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 593m² para alugar no Centro R$29.678 R$3.150 R$2.892 593 m² 0 quartos 0 suítes 9 banheiros 0 vagas Tem elevador
    Sala-andar de 780m² para alugar no Centro R$39.000 R$9.215 R$2.164 780 m² 0 quartos 0 suítes 11 banheiros 0 vagas None
    Sala-andar de 273m² para alugar no Centro R$8.000 R$1.600 R$1.443 273 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    None None None None None None None None None None
    Sala-andar de 210m² para alugar no Centro R$12.500 R$4.700 R$1.104 210 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 225m² para alugar no Centro R$9.200 R$5.988 R$949 225 m² 0 quartos 0 suítes 5 banheiros 0 vagas None
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.439 R$2.146 340 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 150m² para alugar no Centro R$9.000 R$5.452 R$1.215 150 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 300m² para alugar no Centro R$13.000 R$7.397 R$2.101 300 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 450m² para alugar no Centro R$28.000 R$4.788 R$1.770 450 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 160m² para alugar no Centro R$11.000 R$5.887 R$699 160 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 245m² para alugar no Centro R$17.000 R$8.570 R$2.042 245 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 264m² para alugar no Centro R$8.500 R$6.707 R$1.851 264 m² 0 quartos 0 suítes 3 banheiros 1 vaga None
    None None None None None None None None None None
    Sala-andar de 360m² para alugar no Centro R$16.000 R$9.496 R$2.069 360 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 219m² para alugar no Centro R$8.760 R$4.312 R$1.434 219 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 282m² para alugar no Centro R$10.000 R$5.200 R$1.800 282 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 394m² para alugar no Centro R$9.000 R$5.164 R$2.492 394 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 219m² para alugar no Centro R$23.000 R$5.938 R$1.303 219 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 194m² para alugar no Centro R$8.500 R$4.274 R$920 194 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 478m² para alugar no Centro R$18.000 R$3.199 R$1.520 478 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 373m² para alugar no Centro R$11.300 R$7.200 R$2.275 373 m² 0 quartos 0 suítes 5 banheiros 1 vaga Tem elevador
    Sala-andar de 270m² para alugar no Centro R$10.000 R$4.600 R$1.800 270 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 350m² para alugar no Centro R$18.000 R$5.100 R$2.000 350 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 425m² para alugar no Centro R$9.000 R$9.178 R$2.104 425 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 286m² para alugar no Centro R$13.200 R$1.820 R$13.161 286 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 33m² para alugar no Centro R$500 R$580 R$173 33 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 68m² para alugar no Centro R$1.000 R$899 R$305 68 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 390m² para alugar no Centro R$23.442 R$13.284 R$1.628 390 m² 0 quartos 0 suítes 2 banheiros 1 vaga None
    Sala-andar de 367m² para alugar no Centro R$23.871 R$9.251 R$1.492 367 m² 0 quartos 0 suítes 4 banheiros 1 vaga None
    Sala-andar de 326m² para alugar no Centro R$19.561 R$11.085 R$1.337 326 m² 0 quartos 0 suítes 2 banheiros 1 vaga None
    Sala-andar de 773m² para alugar no Centro R$54.177 R$26.314 R$3.618 773 m² 0 quartos 0 suítes 4 banheiros 2 vagas None
    Sala-andar de 750m² para alugar no Centro R$40.000 R$7.200 R$2.018 750 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 44m² para alugar no Centro R$750 R$318 R$141 44 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 55m² para alugar no Centro R$700 R$637 R$261 55 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 29m² para alugar no Centro R$300 R$555 R$131 29 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Loja de 133m² para alugar no Centro R$1.000 R$1.568 R$1.186 133 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 196m² para alugar no Centro R$7.840 R$1.359 R$855 196 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 57m² para alugar no Centro R$5.187 R$1.596 R$210 57 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Loja de 100m² para alugar no Centro R$2.000 R$451 R$514 100 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Apartamento de 2 quartos, 45m² para alugar no Centro R$700 R$800 R$40 45 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 22m² para alugar no Centro R$660 Não informado Não informado 22 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Prédio de 480m² para alugar no Centro R$10.000 Não informado R$12.066 480 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 588m² para alugar no Centro R$52.979 R$16.308 R$2.152 588 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 562m² para alugar no Centro R$50.641 R$15.589 R$2.057 562 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 403m² para alugar no Centro R$36.303 R$11.175 R$1.475 403 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 560m² para alugar no Centro R$50.405 R$15.516 R$2.048 560 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 403m² para alugar no Centro R$36.272 R$11.166 R$1.474 403 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 563m² para alugar no Centro R$50.675 R$15.599 R$2.058 563 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 786m² para alugar no Centro R$55.087 R$15.739 R$4.721 786 m² 0 quartos 0 suítes 3 banheiros 9 vagas Tem elevador
    Sala-andar de 552m² para alugar no Centro R$38.000 R$11.046 R$3.313 552 m² 0 quartos 0 suítes 3 banheiros 3 vagas Tem elevador
    Sala-andar de 294m² para alugar no Centro R$14.000 R$4.704 R$73 294 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 373m² para alugar no Centro R$25.374 R$9.328 R$1.492 373 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 482m² para alugar no Centro R$28.920 R$8.194 R$1.446 482 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 32m² para alugar no Centro R$500 R$416 R$126 32 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 25m² para alugar no Centro R$500 R$500 R$168 25 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 403m² para alugar no Centro R$36.356 R$1.191 R$1.476 403 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 25m² para alugar no Centro R$790 R$479 Não informado 25 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 31m² para alugar no Centro R$550 R$490 R$116 31 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 28m² para alugar no Centro R$765 R$370 Não informado 28 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 296m² para alugar no Centro R$8.000 R$6.805 R$2.156 296 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 733m² para alugar no Centro R$36.650 R$3.382 R$3.520 733 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 254m² para alugar no Centro R$9.000 R$3.373 R$1.434 254 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 677m² para alugar no Centro R$44.000 R$13.113 R$4.468 677 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Casa de 1 quarto, 35m² para alugar no Centro R$608 R$840 R$80 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Sala-andar de 293m² para alugar no Centro R$11.720 R$2.032 R$1.428 293 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 231m² para alugar no Centro R$9.240 R$1.596 R$1.144 231 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 120m² para alugar no Centro R$4.000 R$2.526 R$334 120 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 200m² para alugar no Centro R$4.000 R$2.600 R$622 200 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$4.500 R$2.434 R$793 270 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 32m² para alugar no Centro R$600 R$490 R$116 32 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 50m² para alugar no Centro R$600 R$1.050 R$212 50 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 233m² para alugar no Centro R$5.008 R$9.001 R$358 233 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$5.000 R$3.000 R$1.726 270 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 162m² para alugar no Centro R$5.000 R$1.748 R$418 162 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    None None None None None None None None None None
    Sala-andar de 40m² para alugar no Centro R$680 R$740 Não informado 40 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 65m² para alugar no Centro R$900 R$1.560 R$472 65 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 300m² para alugar no Centro R$6.000 R$3.200 R$1.247 300 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 270m² para alugar no Centro R$5.000 Não informado R$1.250 270 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 240m² para alugar no Centro R$5.148 R$9.252 R$268 240 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 104m² para alugar no Centro R$6.760 R$2.461 R$904 104 m² 0 quartos 0 suítes 2 banheiros 2 vagas Tem elevador
    Sala-andar de 70m² para alugar no Centro R$1.200 R$1.250 R$449 70 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 22m² para alugar no Centro R$710 Não informado Não informado 22 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Apartamento de 4 quartos, 116m² para alugar no Centro R$1.800 R$1.300 R$294 116 m² 4 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 75m² para alugar no Centro R$5.281 Não informado Não informado 75 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 82m² para alugar no Centro R$5.751 Não informado Não informado 82 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 35m² para alugar no Centro R$770 R$450 R$21 35 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 70m² para alugar no Centro R$1.300 R$1.250 R$450 70 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 50m² para alugar no Centro R$1.000 R$600 R$170 50 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 46m² para alugar no Centro R$9.000 R$150 R$598 46 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 70m² para alugar no Centro R$1.200 R$1.200 R$449 70 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 74m² para alugar no Centro R$1.200 R$1.200 R$458 74 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 360m² para alugar no Centro R$7.500 Não informado Não informado 360 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 35m² para alugar no Centro R$950 R$657 Não informado 35 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 47m² para alugar no Centro R$1.000 R$657 Não informado 47 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 249m² para alugar no Centro R$4.000 R$2.986 Não informado 249 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 273m² para alugar no Centro R$4.000 R$2.900 Não informado 273 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 100m² para alugar no Centro R$2.000 R$451 R$514 100 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 80m² para alugar no Centro R$1.500 R$636 R$283 80 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 40m² para alugar no Centro R$790 R$430 R$23 40 m² 1 quarto 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 245m² para alugar no Centro R$5.500 R$5.145 Não informado 245 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 225m² para alugar no Centro R$5.000 R$4.500 R$1.300 225 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 225m² para alugar no Centro R$6.000 R$4.500 R$1.300 225 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 225m² para alugar no Centro R$4.900 R$4.500 R$1.300 225 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 245m² para alugar no Centro R$5.000 R$5.145 Não informado 245 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 219m² para alugar no Centro R$5.000 R$5.300 R$1.400 219 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 369m² para alugar no Centro R$7.000 R$3.500 R$1.204 369 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 100m² para alugar no Centro R$2.500 R$1.625 R$479 100 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 350m² para alugar no Centro R$8.000 R$1.400 R$3.100 350 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 37m² para alugar no Centro R$700 R$511 R$221 37 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 37m² para alugar no Centro R$400 R$935 R$252 37 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 38m² para alugar no Centro R$1.500 R$643 R$275 38 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Casa de 1 quarto, 39m² para alugar no Centro R$690 R$670 Não informado 39 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 544m² para alugar no Centro R$48.999 R$15.083 R$1.990 544 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 393m² para alugar no Centro R$35.411 R$10.900 R$1.438 393 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 393m² para alugar no Centro R$35.385 R$10.892 R$1.437 393 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 447m² para alugar no Centro R$40.291 R$12.402 R$1.636 447 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 540m² para alugar no Centro R$48.645 R$14.974 R$1.976 540 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 536m² para alugar no Centro R$48.296 R$14.867 R$1.961 536 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 393m² para alugar no Centro R$35.438 R$10.909 R$1.439 393 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 457m² para alugar no Centro R$49.299 R$15.175 R$2.002 457 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 459m² para alugar no Centro R$41.362 R$12.732 R$1.680 459 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 384m² para alugar no Centro R$34.636 R$10.662 R$1.406 384 m² 0 quartos 0 suítes 0 banheiros 1 vaga Tem elevador
    Sala-andar de 458m² para alugar no Centro R$41.264 R$12.703 R$1.676 458 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 45m² para alugar no Centro R$940 R$750 R$34 45 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 136m² para alugar no Centro R$2.500 R$1.799 R$614 136 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 270m² para alugar no Centro R$7.000 R$2.700 R$1.410 270 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 192m² para alugar no Centro R$7.000 R$3.691 R$1.503 192 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 300m² para alugar no Centro R$7.500 R$2.958 R$1.044 300 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 99m² para alugar no Centro R$6.971 Não informado Não informado 99 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 102m² para alugar no Centro R$7.170 Não informado Não informado 102 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 220m² para alugar no Centro R$7.000 R$3.500 R$300 220 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 130m² para alugar no Centro R$100 R$1.829 R$483 130 m² 0 quartos 0 suítes 2 banheiros 1 vaga Tem elevador
    Sala-andar de 270m² para alugar no Centro R$100 R$3.658 R$966 270 m² 0 quartos 0 suítes 2 banheiros 1 vaga Tem elevador
    None None None None None None None None None None
    Sala-andar de 50m² para alugar no Centro R$450 R$927 R$320 50 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 180m² para alugar no Centro R$9.000 Não informado R$970 180 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 40m² para alugar no Centro R$1.000 R$490 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Casa de 5 quartos, 550m² para alugar no Centro R$5.000 R$100 R$690 550 m² 5 quartos 0 suítes 3 banheiros 1 vaga None
    Apartamento de 2 quartos, 60m² para alugar no Centro R$1.292 R$900 R$92 60 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 201m² para alugar no Centro R$4.000 R$1.780 Não informado 201 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 423m² para alugar no Centro R$18.000 Não informado R$90 423 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Apartamento de 1 quarto, 45m² para alugar no Centro R$1.150 R$480 R$23 45 m² 1 quarto 1 suíte 1 banheiro 1 vaga Tem elevador
    Sala-andar de 50m² para alugar no Centro R$1.000 R$646 R$290 50 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 49m² para alugar no Centro R$1.190 R$600 R$58 49 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 34m² para alugar no Centro R$200 R$545 R$164 34 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 28m² para alugar no Centro R$150 R$636 R$25 28 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 40m² para alugar no Centro R$900 R$931 R$252 40 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 27m² para alugar no Centro R$100 R$1.126 R$154 27 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Loja de 860m² para alugar no Centro R$14.000 Não informado Não informado 860 m² 0 quartos 0 suítes 1 banheiro 10 vagas None
    Casa de 1 quarto, 38m² para alugar no Centro R$1.070 R$301 Não informado 38 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    None None None None None None None None None None
    Casa de 4 quartos, 127m² para alugar no Centro R$2.400 Não informado R$100 127 m² 4 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 603m² para alugar no Centro R$60.300 R$12.189 R$3.636 603 m² 0 quartos 0 suítes 5 banheiros 11 vagas Tem elevador
    Sala-andar de 600m² para alugar no Centro R$16.000 R$7.450 R$2.800 600 m² 0 quartos 0 suítes 10 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 27m² para alugar no Centro R$1.147 R$530 R$21 27 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 33m² para alugar no Centro R$1.350 R$420 Não informado 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 38m² para alugar no Centro R$640 R$700 R$185 38 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 50m² para alugar no Centro R$1.000 R$516 Não informado 50 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 208m² para alugar no Centro R$6.000 R$2.740 R$830 208 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 80m² para alugar no Centro R$1.800 R$1.800 R$661 80 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 85m² para alugar no Centro R$2.200 R$1.220 R$344 85 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 1.037m² para alugar no Centro R$35.000 R$10.400 R$6.013 1037 m² 0 quartos 0 suítes 8 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 32m² para alugar no Centro R$1.070 R$477 Não informado 32 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 41m² para alugar no Centro R$1.100 R$450 Não informado 41 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 800m² para alugar no Centro R$30.000 R$12.582 R$4.043 800 m² 0 quartos 0 suítes 6 banheiros 10 vagas None
    Sala-andar de 800m² para alugar no Centro R$25.000 R$12.413 R$4.043 800 m² 0 quartos 0 suítes 6 banheiros 10 vagas None
    Sala-andar de 320m² para alugar no Centro R$8.000 R$3.462 R$917 320 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 301m² para alugar no Centro R$10.000 R$3.442 R$928 301 m² 0 quartos 0 suítes 7 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.750 R$450 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Prédio de 765m² para alugar no Centro R$23.000 Não informado R$38.000 765 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 1.040m² para alugar no Centro R$40.000 R$10.400 R$5.787 1040 m² 0 quartos 0 suítes 8 banheiros 0 vagas None
    Sala-andar de 1.251m² para alugar no Centro R$137.610 R$31.275 R$3.753 1251 m² 0 quartos 0 suítes 4 banheiros 5 vagas Tem elevador
    Prédio de 572m² para alugar no Centro R$10.000 Não informado R$5.526 572 m² 0 quartos 0 suítes 8 banheiros 0 vagas None
    Sala-andar de 1.040m² para alugar no Centro R$60.000 R$8.725 R$5.787 1040 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    None None None None None None None None None None
    Sala-andar de 369m² para alugar no Centro R$9.900 R$6.000 R$3.337 369 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 293m² para alugar no Centro R$11.720 R$5.200 R$2.286 293 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 140m² para alugar no Centro R$8.500 R$2.400 R$745 140 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 800m² para alugar no Centro R$32.000 R$8.318 R$3.760 800 m² 0 quartos 0 suítes 6 banheiros 11 vagas Tem elevador
    Sala-andar de 597m² para alugar no Centro R$23.880 R$5.900 R$3.065 597 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 705m² para alugar no Centro R$77.550 R$17.625 R$2.115 705 m² 0 quartos 0 suítes 4 banheiros 3 vagas Tem elevador
    Sala-andar de 638m² para alugar no Centro R$38.289 R$17.230 R$4.658 638 m² 0 quartos 0 suítes 6 banheiros 4 vagas Tem elevador
    Sala-andar de 360m² para alugar no Centro R$9.000 R$2.968 R$1.208 360 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 361m² para alugar no Centro R$17.000 R$8.200 R$1.581 361 m² 0 quartos 0 suítes 4 banheiros 1 vaga None
    Sala-andar de 330m² para alugar no Centro R$21.450 R$8.118 R$2.475 330 m² 0 quartos 0 suítes 3 banheiros 2 vagas Tem elevador
    Sala-andar de 283m² para alugar no Centro R$14.188 R$3.836 R$1.318 283 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 293m² para alugar no Centro R$14.656 R$3.963 R$1.371 293 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 228m² para alugar no Centro R$20.081 R$3.648 R$1.004 228 m² 0 quartos 0 suítes 4 banheiros 2 vagas None
    None None None None None None None None None None
    None None None None None None None None None None
    Sala-andar de 361m² para alugar no Centro R$16.000 R$6.950 R$2.537 361 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 576m² para alugar no Centro R$28.845 R$7.684 R$2.699 576 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 294m² para alugar no Centro R$14.715 R$5.297 R$294 294 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 438m² para alugar no Centro R$48.264 R$6.638 R$1.659 438 m² 0 quartos 0 suítes 2 banheiros 2 vagas None
    Sala-andar de 771m² para alugar no Centro R$65.538 R$14.927 R$2.852 771 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 459m² para alugar no Centro R$40.450 R$7.350 R$2.022 459 m² 0 quartos 0 suítes 4 banheiros 2 vagas None
    Sala-andar de 210m² para alugar no Centro R$18.530 R$3.367 R$927 210 m² 0 quartos 0 suítes 4 banheiros 2 vagas None
    Sala-andar de 667m² para alugar no Centro R$17.000 R$17.272 R$2.662 667 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 638m² para alugar no Centro R$47.861 R$15.162 R$2.700 638 m² 0 quartos 0 suítes 6 banheiros 4 vagas Tem elevador
    Sala-andar de 698m² para alugar no Centro R$38.390 R$12.564 R$4.397 698 m² 0 quartos 0 suítes 6 banheiros 4 vagas Tem elevador
    Sala-andar de 362m² para alugar no Centro R$19.910 R$6.516 R$2.280 362 m² 0 quartos 0 suítes 3 banheiros 2 vagas Tem elevador
    Sala-andar de 371m² para alugar no Centro R$16.000 R$3.604 R$1.357 371 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 24m² para alugar no Centro R$450 R$440 R$10 24 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$24.300 R$6.210 R$193 270 m² 0 quartos 0 suítes 0 banheiros 5 vagas None
    Sala-andar de 370m² para alugar no Centro R$10.000 R$6.000 R$2.071 370 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 171m² para alugar no Centro R$12.017 Não informado Não informado 171 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 484m² para alugar no Centro R$10.000 R$7.282 R$1.884 484 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 484m² para alugar no Centro R$13.000 R$7.282 R$1.745 484 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 600m² para alugar no Centro R$23.880 R$5.900 R$3.065 600 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 300m² para alugar no Centro R$11.000 R$4.000 R$1.178 300 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 379m² para alugar no Centro R$8.500 R$5.613 R$2.056 379 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 678m² para alugar no Centro R$18.000 R$9.994 R$3.030 678 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 540m² para alugar no Centro R$15.000 R$5.785 R$6.107 540 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 168m² para alugar no Centro R$8.400 R$3.360 R$840 168 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 350m² para alugar no Centro R$20.000 R$3.000 R$1.102 350 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 791m² para alugar no Centro R$51.436 R$11.910 R$3.403 791 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 300m² para alugar no Centro R$8.000 R$2.958 R$1.044 300 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 760m² para alugar no Centro R$17.000 R$8.419 R$4.124 760 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 470m² para alugar no Centro R$21.150 R$14.085 R$2.394 470 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 300m² para alugar no Centro R$8.000 R$4.000 R$1.839 300 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 148m² para alugar no Centro R$9.620 R$3.351 R$1.249 148 m² 0 quartos 0 suítes 2 banheiros 3 vagas Tem elevador
    Sala-andar de 760m² para alugar no Centro R$91.236 R$16.726 R$3.974 760 m² 0 quartos 0 suítes 6 banheiros 0 vagas Tem elevador
    Sala-andar de 160m² para alugar no Centro R$10.400 R$3.811 R$1.343 160 m² 0 quartos 0 suítes 3 banheiros 3 vagas Tem elevador
    Sala-andar de 520m² para alugar no Centro R$18.000 R$6.400 R$1.130 520 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 258m² para alugar no Centro R$10.000 R$5.300 R$1.250 258 m² 0 quartos 0 suítes 4 banheiros 3 vagas Tem elevador
    Sala-andar de 400m² para alugar no Centro R$32.000 R$6.000 R$1.200 400 m² 0 quartos 0 suítes 3 banheiros 3 vagas Tem elevador
    Sala-andar de 460m² para alugar no Centro R$15.000 R$7.130 R$2.884 460 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 450m² para alugar no Centro R$10.000 R$8.327 R$1.673 450 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 640m² para alugar no Centro R$13.728 R$12.336 R$89 640 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 320m² para alugar no Centro R$15.000 R$2.400 R$7.015 320 m² 0 quartos 0 suítes 6 banheiros 0 vagas Tem elevador
    Sala-andar de 579m² para alugar no Centro R$23.880 R$5.900 R$3.065 579 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 433m² para alugar no Centro R$32.475 R$9.526 R$2.234 433 m² 0 quartos 0 suítes 2 banheiros 6 vagas Tem elevador
    Sala-andar de 156m² para alugar no Centro R$11.700 R$3.430 R$1.363 156 m² 0 quartos 0 suítes 2 banheiros 3 vagas Tem elevador
    Sala-andar de 641m² para alugar no Centro R$10.000 R$7.680 R$3.846 641 m² 0 quartos 0 suítes 9 banheiros 0 vagas Tem elevador
    Sala-andar de 597m² para alugar no Centro R$23.880 R$5.900 R$3.065 597 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 200m² para alugar no Centro R$10.000 R$2.500 R$900 200 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 380m² para alugar no Centro R$9.000 R$4.000 R$1.682 380 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 260m² para alugar no Centro R$18.000 R$3.052 R$5.000 260 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 25m² para alugar no Centro R$600 R$346 R$1.250 25 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 34m² para alugar no Centro R$400 R$530 R$160 34 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 130m² para alugar no Centro R$1.100 R$1.829 R$483 130 m² 0 quartos 0 suítes 2 banheiros 1 vaga Tem elevador
    Loja de 94m² para alugar no Centro R$3.419 Não informado R$419 94 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    None None None None None None None None None None
    None None None None None None None None None None
    Sala-andar de 85m² para alugar no Centro R$1.100 R$1.464 R$181 85 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Casa de 2 quartos, 80m² para alugar no Centro R$1.880 Não informado Não informado 80 m² 2 quartos 0 suítes 1 banheiro 0 vagas None
    Casa de 0 quartos, 450m² para alugar no Centro R$15.000 Não informado Não informado 450 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 128m² para alugar no Centro R$1.000 R$3.194 R$768 128 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 60m² para alugar no Centro R$1.200 R$840 R$294 60 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 29m² para alugar no Centro R$550 R$381 R$169 29 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Vaga de Garagem de 10m² para alugar no Centro R$450 Não informado R$816 10 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 2.315m² para alugar no Centro R$115.000 R$33.854 R$4.262 2315 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 2.188m² para alugar no Centro R$110.000 R$31.999 R$4.028 2188 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 2.397m² para alugar no Centro R$120.000 Não informado R$4.413 2397 m² 0 quartos 0 suítes 0 banheiros 89 vagas Tem elevador
    Sala-andar de 75m² para alugar no Centro R$900 R$719 R$300 75 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 27m² para alugar no Centro R$700 R$1.247 R$157 27 m² 0 quartos 0 suítes 1 banheiro 1 vaga None
    Sala-andar de 35m² para alugar no Centro R$1.000 R$307 R$220 35 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 30m² para alugar no Centro R$1.000 R$307 R$220 30 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 58m² para alugar no Centro R$800 R$1.294 R$335 58 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 34m² para alugar no Centro R$800 R$298 R$160 34 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 40m² para alugar no Centro R$1.200 R$640 Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 39m² para alugar no Centro R$1.420 R$500 R$75 39 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 34m² para alugar no Centro R$850 R$450 R$125 34 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 2.260m² para alugar no Centro R$135.600 R$42.940 Não informado 2260 m² 0 quartos 0 suítes 8 banheiros 10 vagas None
    Sala-andar de 47m² para alugar no Centro R$1.400 R$950 R$80 47 m² 0 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Apartamento de 1 quarto, 46m² para alugar no Centro R$1.000 R$430 R$211 46 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 36m² para alugar no Centro R$1.000 R$403 Não informado 36 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 670m² para alugar no Centro R$27.000 R$6.908 R$2.190 670 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 296m² para alugar no Centro R$10.000 R$253 R$1.329 296 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 703m² para alugar no Centro R$38.665 R$17.012 R$2.959 703 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 203m² para alugar no Centro R$14.254 Não informado Não informado 203 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 134m² para alugar no Centro R$9.438 Não informado Não informado 134 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 440m² para alugar no Centro R$28.000 R$8.200 R$16.364 440 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 141m² para alugar no Centro R$12.690 R$3.243 R$99 141 m² 0 quartos 0 suítes 2 banheiros 3 vagas None
    None None None None None None None None None None
    Sala-andar de 25m² para alugar no Centro R$300 R$429 R$109 25 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Apartamento de 1 quarto, 40m² para alugar no Centro R$1.040 Não informado Não informado 40 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$1.040 R$400 Não informado 30 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Prédio de 2.400m² para alugar no Centro R$168.000 Não informado Não informado 2400 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Prédio de 647m² para alugar no Centro R$6.000 Não informado R$2.013 647 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Apartamento de 1 quarto, 60m² para alugar no Centro R$1.615 R$600 R$67 60 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 137m² para alugar no Centro R$4.500 R$3.700 R$899 137 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 150m² para alugar no Centro R$2.300 R$1.920 R$708 150 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 350m² para alugar no Centro R$15.000 R$6.436 R$2.238 350 m² 0 quartos 0 suítes 4 banheiros 2 vagas Tem elevador
    Sala-andar de 58m² para alugar no Centro R$800 R$816 R$238 58 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 333m² para alugar no Centro R$5.000 R$8.636 R$1.383 333 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 27m² para alugar no Centro R$200 R$443 R$115 27 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 86m² para alugar no Centro R$3.500 R$1.469 R$542 86 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 56m² para alugar no Centro R$2.000 R$941 R$394 56 m² 0 quartos 0 suítes 1 banheiro 1 vaga None
    Sala-andar de 170m² para alugar no Centro R$7.900 Não informado R$867 170 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 286m² para alugar no Centro R$7.000 R$3.787 R$1.617 286 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 44m² para alugar no Centro R$900 R$369 R$199 44 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 42m² para alugar no Centro R$900 R$349 R$199 42 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 300m² para alugar no Centro R$8.000 R$5.000 Não informado 300 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 860m² para alugar no Centro R$14.000 Não informado Não informado 860 m² 0 quartos 0 suítes 0 banheiros 1 vaga None
    Sala-andar de 39m² para alugar no Centro R$600 R$652 R$184 39 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 55m² para alugar no Centro R$1.200 R$1.200 R$462 55 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 85m² para alugar no Centro R$1.500 R$1.100 R$350 85 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 106m² para alugar no Centro R$2.500 R$1.541 R$624 106 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 164m² para alugar no Centro R$2.000 R$1.058 R$1.339 164 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 59m² para alugar no Centro R$1.500 R$897 R$317 59 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 300m² para alugar no Centro R$15.000 Não informado Não informado 300 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 52m² para alugar no Centro R$1.800 R$452 R$90 52 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 99m² para alugar no Centro R$3.000 R$800 R$295 99 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 26m² para alugar no Centro R$400 R$226 R$160 26 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 32m² para alugar no Centro R$500 R$590 R$161 32 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 70m² para alugar no Centro R$700 R$1.100 R$236 70 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 782m² para alugar no Centro R$9.800 R$6.022 Não informado 782 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 75m² para alugar no Centro R$1.000 R$1.367 R$138 75 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 135m² para alugar no Centro R$9.500 R$2.755 R$291 135 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 50m² para alugar no Centro R$600 R$833 R$312 50 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 64m² para alugar no Centro R$1.200 R$1.027 R$350 64 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 156m² para alugar no Centro R$10.500 R$1.100 R$1 156 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 35m² para alugar no Centro R$400 R$537 R$102 35 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 32m² para alugar no Centro R$500 R$416 R$126 32 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Loja de 1.120m² para alugar no Centro R$170.000 R$17.000 R$10.500 1120 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 667m² para alugar no Centro R$9.000 R$17.272 R$2.767 667 m² 0 quartos 0 suítes 5 banheiros 0 vagas None
    Sala-andar de 667m² para alugar no Centro R$8.000 R$17.272 R$2.767 667 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 503m² para alugar no Centro R$8.000 R$5.368 R$2.191 503 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 63m² para alugar no Centro R$2.500 R$1.330 R$3.622 63 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 149m² para alugar no Centro R$2.500 R$2.400 R$528 149 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 225m² para alugar no Centro R$5.000 R$2.485 R$1.246 225 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 256m² para alugar no Centro R$2.500 R$207 R$216 256 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 217m² para alugar no Centro R$5.500 R$1.576 R$627 217 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 291m² para alugar no Centro R$6.400 R$4.232 R$1.698 291 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 288m² para alugar no Centro R$6.000 R$2.001 R$887 288 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 391m² para alugar no Centro R$15.000 R$5.604 Não informado 391 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 135m² para alugar no Centro R$9.500 R$2.755 R$291 135 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Loja de 230m² para alugar no Centro R$10.000 Não informado R$1.446 230 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 70m² para alugar no Centro R$2.000 R$855 Não informado 70 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 135m² para alugar no Centro R$3.600 R$1.500 R$86.336 135 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 310m² para alugar no Centro R$4.000 R$5.960 R$23.544 310 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Prédio de 680m² para alugar no Centro R$20.000 Não informado R$50.063 680 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 321m² para alugar no Centro R$7.500 R$5.960 R$24.321 321 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Sala-andar de 700m² para alugar no Centro R$10.000 R$6.914 R$3.472 700 m² 0 quartos 0 suítes 8 banheiros 0 vagas Tem elevador
    Sala-andar de 300m² para alugar no Centro R$10.000 R$1.545 R$685 300 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 562m² para alugar no Centro R$70.000 R$10.800 Não informado 562 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 360m² para alugar no Centro R$8.000 R$4.204 R$1.580 360 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 135m² para alugar no Centro R$3.400 R$1.500 R$8.633 135 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 175m² para alugar no Centro R$3.000 R$3.750 Não informado 175 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 1.300m² para alugar no Centro R$25.000 Não informado Não informado 1300 m² 0 quartos 0 suítes 0 banheiros 4 vagas None
    Sala-andar de 337m² para alugar no Centro R$10.000 R$2.584 R$1.760 337 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$5.000 R$3.000 R$17.267 270 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$7.000 R$3.000 R$17.267 270 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 38m² para alugar no Centro R$722 R$557 R$40 38 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 28m² para alugar no Centro R$630 R$400 Não informado 28 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 90m² para alugar no Centro R$13.000 Não informado Não informado 90 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 30m² para alugar no Centro R$250 R$250 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 40m² para alugar no Centro R$790 R$640 R$62 40 m² 1 quarto 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 292m² para alugar no Centro R$3.900 R$4.225 R$1.334 292 m² 0 quartos 0 suítes 5 banheiros 0 vagas None
    Sala-andar de 1.330m² para alugar no Centro R$79.500 R$32.000 R$7.552 1330 m² 0 quartos 0 suítes 8 banheiros 0 vagas None
    Casa de 0 quartos, 410m² para alugar no Centro R$9.900 R$6.619 R$1.876 410 m² 0 quartos 0 suítes 9 banheiros 0 vagas None
    Sala-andar de 1.330m² para alugar no Centro R$69.500 R$32.000 R$6.706 1330 m² 0 quartos 0 suítes 8 banheiros 0 vagas None
    Loja de 483m² para alugar no Centro R$19.356 R$4.200 R$2.886 483 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Loja de 7m² para alugar no Centro R$2.500 R$275 Não informado 7 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 7m² para alugar no Centro R$2.000 R$275 Não informado 7 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Loja de 11m² para alugar no Centro R$4.500 Não informado R$191 11 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 95m² para alugar no Centro R$1.100 Não informado R$220 95 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 38m² para alugar no Centro R$700 R$1.615 R$244 38 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 0 quartos, 406m² para alugar no Centro R$8.900 R$8.526 Não informado 406 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 29m² para alugar no Centro R$500 R$557 R$103 29 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 28m² para alugar no Centro R$500 R$574 R$101 28 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Loja de 38m² para alugar no Centro R$8.500 R$1.755 R$463 38 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 21m² para alugar no Centro R$800 R$425 R$110 21 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 2 quartos, 48m² para alugar no Centro R$1.200 R$579 R$62 48 m² 2 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 28m² para alugar no Centro R$750 R$650 R$174 28 m² 0 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 200m² para alugar no Centro R$5.800 R$4.274 R$920 200 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 50m² para alugar no Centro R$1.072 R$1.927 R$89 50 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 100m² para alugar no Centro R$6.000 R$2.000 Não informado 100 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 100m² para alugar no Centro R$6.000 R$2.000 Não informado 100 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 100m² para alugar no Centro R$6.000 Não informado Não informado 100 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 100m² para alugar no Centro R$6.000 R$2.000 Não informado 100 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$800 R$460 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$810 R$456 R$94 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$900 R$453 R$100 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Apartamento de 1 quarto, 33m² para alugar no Centro R$1.400 R$350 Não informado 33 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 231m² para alugar no Centro R$7.000 R$3.300 R$1.577 231 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Apartamento de 1 quarto, 45m² para alugar no Centro R$1.400 R$535 R$52 45 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 156m² para alugar no Centro R$6.240 R$1.077 R$663 156 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 196m² para alugar no Centro R$7.840 R$1.359 R$941 196 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 600m² para alugar no Centro R$5.000 R$12.649 R$2.902 600 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 100m² para alugar no Centro R$3.300 R$1.350 R$480 100 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.439 R$1.820 340 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.397 R$2.450 340 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 30m² para alugar no Centro R$250 R$250 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 30m² para alugar no Centro R$250 R$250 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    None None None None None None None None None None
    Sala-andar de 30m² para alugar no Centro R$250 R$250 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 671m² para alugar no Centro R$30.195 R$18.068 R$2.325 671 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 671m² para alugar no Centro R$30.195 R$18.068 R$2.325 671 m² 0 quartos 0 suítes 6 banheiros 0 vagas None
    Sala-andar de 394m² para alugar no Centro R$17.800 R$7.070 R$1.874 394 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 394m² para alugar no Centro R$17.800 R$7.070 R$1.874 394 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 394m² para alugar no Centro R$17.800 R$7.070 R$1.874 394 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 219m² para alugar no Centro R$17.000 R$5.938 R$1.529 219 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.439 R$2.013 340 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 210m² para alugar no Centro R$12.500 R$6.445 R$1.062 210 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 220m² para alugar no Centro R$13.900 R$2.515 R$1.544 220 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 225m² para alugar no Centro R$16.000 R$4.300 R$820 225 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 414m² para alugar no Centro R$16.000 R$8.971 R$1.086 414 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 581m² para alugar no Centro R$29.050 R$13.595 R$3.015 581 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 414m² para alugar no Centro R$16.000 R$8.971 R$1.086 414 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.439 R$2.013 340 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 225m² para alugar no Centro R$16.000 R$4.300 R$820 225 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 593m² para alugar no Centro R$29.678 R$3.150 R$2.892 593 m² 0 quartos 0 suítes 9 banheiros 0 vagas Tem elevador
    Sala-andar de 593m² para alugar no Centro R$29.678 R$3.150 R$2.892 593 m² 0 quartos 0 suítes 9 banheiros 0 vagas Tem elevador
    Sala-andar de 593m² para alugar no Centro R$29.678 R$3.150 R$2.892 593 m² 0 quartos 0 suítes 9 banheiros 0 vagas Tem elevador
    Sala-andar de 593m² para alugar no Centro R$29.678 R$3.150 R$2.892 593 m² 0 quartos 0 suítes 9 banheiros 0 vagas Tem elevador
    Sala-andar de 354m² para alugar no Centro R$20.000 R$8.500 R$3.117 354 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 354m² para alugar no Centro R$20.000 R$8.500 R$3.117 354 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 354m² para alugar no Centro R$20.000 R$8.500 R$3.117 354 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.439 R$2.146 340 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.439 R$2.013 340 m² 0 quartos 0 suítes 5 banheiros 0 vagas Tem elevador
    Sala-andar de 340m² para alugar no Centro R$13.000 R$7.397 R$2.450 340 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 375m² para alugar no Centro R$8.800 R$5.960 R$2.774 375 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 68m² para alugar no Centro R$1.300 R$899 R$305 68 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 74m² para alugar no Centro R$1.200 R$1.200 R$458 74 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 25m² para alugar no Centro R$500 R$500 R$168 25 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Casa de 1 quarto, 22m² para alugar no Centro R$660 Não informado Não informado 22 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 25m² para alugar no Centro R$500 R$500 R$168 25 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Sala-andar de 231m² para alugar no Centro R$9.240 R$1.596 R$1.057 231 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 293m² para alugar no Centro R$11.720 R$2.032 R$1.341 293 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 208m² para alugar no Centro R$6.000 R$2.740 R$830 208 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 208m² para alugar no Centro R$6.000 R$2.740 R$830 208 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 208m² para alugar no Centro R$6.000 R$2.740 R$830 208 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 70m² para alugar no Centro R$1.300 R$1.250 R$45 70 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 225m² para alugar no Centro R$6.000 R$4.500 R$1.300 225 m² 0 quartos 0 suítes 5 banheiros 0 vagas None
    Sala-andar de 225m² para alugar no Centro R$6.000 R$4.500 R$1.300 225 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 225m² para alugar no Centro R$6.000 R$4.500 R$1.300 225 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 270m² para alugar no Centro R$1 R$3.934 R$966 270 m² 0 quartos 0 suítes 4 banheiros 1 vaga Tem elevador
    Sala-andar de 270m² para alugar no Centro R$7.000 R$3.000 R$1.726 270 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 192m² para alugar no Centro R$7.000 R$3.691 R$1.503 192 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$1 R$3.738 R$966 270 m² 0 quartos 0 suítes 2 banheiros 1 vaga Tem elevador
    Sala-andar de 270m² para alugar no Centro R$100 R$3.658 R$966 270 m² 0 quartos 0 suítes 4 banheiros 1 vaga Tem elevador
    Sala-andar de 270m² para alugar no Centro R$100 R$3.658 R$966 270 m² 0 quartos 0 suítes 4 banheiros 1 vaga Tem elevador
    Sala-andar de 130m² para alugar no Centro R$10 R$1.829 R$490 130 m² 0 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 130m² para alugar no Centro R$100 R$1.859 R$490 130 m² 0 quartos 0 suítes 1 banheiro 1 vaga Tem elevador
    Sala-andar de 201m² para alugar no Centro R$1 R$1.740 R$670 201 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 379m² para alugar no Centro R$8.500 R$5.613 R$2.056 379 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 208m² para alugar no Centro R$6.000 R$2.740 R$830 208 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 208m² para alugar no Centro R$6.000 R$2.740 R$830 208 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 597m² para alugar no Centro R$23.880 R$5.400 R$3.065 597 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 350m² para alugar no Centro R$20.000 R$3.000 R$1.102 350 m² 0 quartos 0 suítes 4 banheiros 0 vagas None
    Sala-andar de 379m² para alugar no Centro R$8.500 R$5.613 R$2.056 379 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 703m² para alugar no Centro R$38.688 R$17.022 R$2.963 703 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 361m² para alugar no Centro R$17.000 R$8.200 R$1.581 361 m² 0 quartos 0 suítes 4 banheiros 1 vaga None
    Sala-andar de 379m² para alugar no Centro R$8.500 R$5.613 R$2.302 379 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 379m² para alugar no Centro R$8.500 R$5.613 R$2.302 379 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    None None None None None None None None None None
    Sala-andar de 350m² para alugar no Centro R$20.000 R$3.000 R$1.102 350 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 379m² para alugar no Centro R$8.500 R$5.613 R$2.138 379 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 379m² para alugar no Centro R$8.500 R$5.613 R$2.472 379 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 200m² para alugar no Centro R$10.000 R$2.500 R$900 200 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 29m² para alugar no Centro R$400 R$341 R$144 29 m² 0 quartos 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 29m² para alugar no Centro R$400 R$391 R$138 29 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 85m² para alugar no Centro R$1.100 R$1.464 R$181 85 m² 0 quartos 0 suítes 2 banheiros 0 vagas None
    Sala-andar de 130m² para alugar no Centro R$1.100 R$1.820 R$483 130 m² 0 quartos 0 suítes 1 banheiro 0 vagas Tem elevador
    Vaga de Garagem de 10m² para alugar no Centro R$450 Não informado Não informado 10 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Vaga de Garagem de 10m² para alugar no Centro R$450 Não informado Não informado 10 m² 0 quartos 0 suítes 0 banheiros 0 vagas None
    Sala-andar de 2.188m² para alugar no Centro R$110.000 Não informado R$4.029 2188 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 162m² para alugar no Centro R$10 R$1.748 R$418 162 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Sala-andar de 670m² para alugar no Centro R$27.000 R$6.908 R$2.190 670 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 670m² para alugar no Centro R$27.000 R$6.908 R$1.983 670 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Sala-andar de 670m² para alugar no Centro R$27.000 R$6.908 R$1.983 670 m² 0 quartos 0 suítes 0 banheiros 0 vagas Tem elevador
    Apartamento de 1 quarto, 30m² para alugar no Centro R$1.040 R$400 Não informado 30 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Sala-andar de 175m² para alugar no Centro R$3.000 R$3.750 Não informado 175 m² 0 quartos 0 suítes 2 banheiros 0 vagas Tem elevador
    Sala-andar de 375m² para alugar no Centro R$8.800 R$5.960 R$8.633 375 m² 0 quartos 0 suítes 4 banheiros 0 vagas Tem elevador
    Sala-andar de 270m² para alugar no Centro R$7.000 R$3.000 R$17.268 270 m² 0 quartos 0 suítes 3 banheiros 0 vagas Tem elevador
    Casa de 1 quarto, 30m² para alugar no Centro R$700 R$350 R$113 30 m² 1 quarto 1 suíte 1 banheiro 0 vagas Tem elevador
    Sala-andar de 30m² para alugar no Centro R$250 R$250 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas None
    Sala-andar de 150m² para alugar no Centro R$3.000 R$500 R$150 150 m² 0 quartos 0 suítes 3 banheiros 0 vagas None
    None None None None None None None None None None
    Casa de 1 quarto, 30m² para alugar no Centro R$750 R$460 Não informado 30 m² 1 quarto 0 suítes 1 banheiro 0 vagas Tem elevador



```python
csv_file.close()
```


```python
print(len(todos_links))
```

    1049



```python

```
