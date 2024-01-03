- 👋import requests

def phone_number_info(phone_number):
   response = requests.get(f'https://www.truecaller.com/search/{phone_number}')

   if response.status_code == 200:
       soup = BeautifulSoup(response.text, 'html.parser')
       info = {}
       info['name'] = soup.find('h1', {'class': 'user-info__name'}).text
       info['city'] = soup.find('div', {'class': 'user-info__city'}).text
       info['province'] = soup.find('div', {'class': 'user-info__province'}).text
       info['country'] = soup.find('div', {'class': 'user-info__country'}).text

       return info
   else:
       return None

if __name__ == "__main__":
   phone_number = input("Enter a phone number: ")
   info = phone_number_info(phone_number)

   if info:
       print("Information Found:")
       print(f"Name: {info['name']}")
       print(f"City: {info['city']}")
       print(f"Province: {info['province']}")
       print(f"Country: {info['country']}")
   else:
       print("No information found for the provided phone number.") 
