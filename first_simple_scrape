from typing import Text
import requests
from bs4 import BeautifulSoup

url = 'https://quotes.toscrape.com/'

response = requests.get(url)

soup = BeautifulSoup(response.content,'html.parser')
quotes = soup.find('div', class_ = 'quote')
author = quotes.find('small', class_ = 'author').text
quote = quotes.find('span', 'text').text
print(quote, ' - ', author)
