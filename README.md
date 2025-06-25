import requests as rq
from bs4 import BeautifulSoup as bs
import pandas as pd
url='https://webscraper.io/test-sites/e-commerce/allinone/computers/laptops'
req=rq.get(url)
soup=bs(req.text,"html.parser")


Titles=[item.text.strip() for item in soup.find_all("a",class_="title")]
Prices=[item.text.strip() for item in soup.find_all("h4",class_="price float-end card-title pull-right")]
Description=[item.text.strip() for item in soup.find_all("p",class_="description card-text")]
NOofReviwes=[item.text.strip() for item in soup.find_all("p",class_="review-count float-end")]

Pd_df=pd.DataFrame({
    "Titles":Titles,
    "Description":Description,
    "Prices":Prices,
    "Reviwes":NOofReviwes
})



Pd_df.to_excel("LaptopData.xlsx",index=False)







