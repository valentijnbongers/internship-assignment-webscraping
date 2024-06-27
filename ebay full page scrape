from typing import Text
import requests
from bs4 import BeautifulSoup

# Product page
url = "https://www.ebay.com.my/itm/142825385094?hash=item21410e6c86%3Ag%3ANIsAAOSwZB9aGiJK&itmprp=enc%3AAQAJAAAA8O%2BilpF42fR2wJd7JXVFL1XE8kAHWAufEcYBbPzp8SC%2BzCuQB%2BPSrGmMaY11jxWTCPsU9ojnFFVNjwoGeZKFwu8TOYlkuBBs%2FtpjnM1BSF3nnsjC8pXsg7kYcbbZPUb2zaRan2vG4ez6X%2BG8qkJD9QRXIe5g%2FkEqrT6LoRfhiIMB64mQjNkKnBmTRHpkhw4CftlrPJ4%2BEZDGsTEbaJpcy4ffic46oDpib6dQryIhilKJTY31Ejw2Ob9NLbPyLcxwgClDpHOh56Myn%2BEEDyBgdeOznmlxajakTSBRsM38VpNqvUmuBb8%2Fk5DXCGRM1KKeSA%3D%3D%7Ctkp%3ABk9SR5K6jOWJZA&LH_BIN=1"

# Use requests to retrieve data from a given URL
response = requests.get(url)

# Parse the whole HTML page using BeautifulSoup
soup = BeautifulSoup(response.content,'html.parser')


# functions for collecting product information
def get_name(soup):
  content = soup.find('div', id = 'mainContent')
  product_name = content.find('span', class_ = 'ux-textspans ux-textspans--BOLD').text
  return product_name

def get_price(soup):
  product_price = soup.find('div', class_ = 'x-price-primary').text
  return product_price

def get_condition(soup):
  product_condition = soup.find('span', class_ = 'ux-icon-text__text').text
  return product_condition


#function for getting all info from 1 page
def scrape_product_page(page_url):
  response = requests.get(page_url)
  soup = BeautifulSoup(response.content,'html.parser')
  name = get_name(soup)
  price = get_price(soup)
  condition = get_condition(soup)
  if condition != '--not specified':
    condition = condition[:int((len(condition)/2))]
  arr = [name, price, condition]
  return arr

  
num_of_pages = 2
items_array = []
url2 = "https://www.ebay.com.my/sch/i.html?_from=R40&_trksid=m570.l1313&_nkw=pants&_sacat=0"
for k in range(1, num_of_pages + 1):

  paged_url = url2 + "&_pgn=" + str(k)
  response2 = requests.get(paged_url)
  soup2 = BeautifulSoup(response2.content, 'html.parser')
  all_items = soup2.find('div', class_ = 'srp-river-results clearfix')
  print(all_items)
  items = all_items.find_all('li', class_ = 's-item s-item__pl-on-bottom')

  for item in items:
    try:
      #finds element that contains link to product page
      link_element = item.find('a', href = True)
      #finds link to product page
      href = link_element.get('href')
      array_data = scrape_product_page(href)
      print(href)
      print(f'Name: {array_data[0]}')
      print(f'Price: {array_data[1]}')
      print(f'condition: {array_data[2]}')
      items_array.append(array_data)
    except AttributeError:
      pass
    else:
      pass
    finally:
      pass
