import requests
from bs4 import BeautifulSoup
import pandas as pd

df = pd.read_excel("Colleges.xlsx")
df['Address'] = ""
df['Principal'] = ""
for index, row in df.iterrows():
    url = row['Website']
    try:
        page = requests.get(url)
        soup = BeautifulSoup(page.content, 'html.parser')
        address = soup.find('div', class_='address')
        if address:
            nb
            df.at[index, 'Address'] = address.get_text().strip()
        principal = soup.find('div', class_='principal')
        if principal:
            df.at[index, 'Principal'] = principal.get_text().strip()
             except:
        print(f"Error accessing website for {row['College Name']}")

# write the updated dataframe to the excel file
df.to_excel("Colleges_updated.xlsx", index=False)

