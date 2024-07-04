# Functions for collecting product information

#Product name
def get_name(soup):
  content = soup.find('div', id = 'mainContent')
  product_name = content.find('span', class_ = 'ux-textspans ux-textspans--BOLD').text
  return product_name

#Product price
def get_price(soup):
  product_price = soup.find('div', class_ = 'x-price-primary').text
  return product_price

#Product condition
def get_condition(soup):
  product_condition = soup.find('span', class_ = 'ux-icon-text__text').text
  return product_condition

#Function for scraping the whole page
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

#Finds all products with selected key word

def scrape_search_page(url,num_pages):
  items_array = []
  for k in range(1, num_pages + 1):

    paged_url = url2 + "&_pgn=" + str(k)
    response2 = requests.get(paged_url)
    soup2 = BeautifulSoup(response2.content, 'html.parser')
    all_items = soup2.find('div', class_ = 'srp-river-results clearfix')
    items = all_items.find_all('li', class_ = 's-item s-item__pl-on-bottom')

  #Displays information

    for item in items:
      try:
        #finds element that contains link to product page
        link_element = item.find('a', href = True)
        
        #finds link to product page
        href = link_element.get('href')
        array_data = scrape_product_page(href)
        items_array.append(array_data)
      except AttributeError:
        pass
      else:
        pass
      finally:
        pass
    return items_array


def export_to_excel(items_array, sheet_number, file_name):
  # Create a DataFrame from the scraped data
  df = pd.DataFrame(items_array, columns=['Name', 'Price', 'Condition'])
  name_of_sheet = 'sheet' + str(sheet_number)
  # Write the DataFrame to an Excel file using xlsxwriter
  with pd.ExcelWriter(file_name, engine='xlsxwriter') as writer:
      df.to_excel(writer, index=False, sheet_name= name_of_sheet)

test_urls_arr = []
filename = input('Enter file name: ')
for i in range(0, len(test_urls_arr)):
  items_array = scrape_search_page(test_urls_arr[i],1)
  export_to_excel(items_array, i, filename)
