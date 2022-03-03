# Web scraping

We'll start by installing our dependency.
To that end, type in the terminal
```
pip install beautifulsoup4
pip install requests
```

In the project, we are going to import them accordingly:
```
from bs4 import BeautifulSoup
import requests
```

We will fetch the data from the website using requests:
```
wanted_game_name = 'name of the game'.lower()
steam = 'https://store.steampowered.com/search/?term='+wanted_game_name
```

lower() will let us use any letter capitalized as we want without error.
Next, we will get all articles inside the page as follows:

```
game_found = soup.find_all("a", class_="search_result_row")
```

This leaves us with a table of x articles (in this case, each article is a game page).
For each of those, we will get the information about the searched game.  
```
for game in game_found:
                name = str(game.find(class_="title").contents[0]).lower()

                if name == wanted_game_name:
                        price = game.find('div', class_="search_price").contents
                        found = True
```
Don't forget to add this at the beginning of the file:  
```
found = False
```

We just need to think about the appropriate exceptions and print the right information:
```
if found != True:
                print(f'{wanted_game_name} not found, please verify the orthograph')
        else:
                if len(price) == 4:
                        price = price[3].strip()
                        print(f'{wanted_game_name} is {float(price.replace(",", ".")[:-1])} €')
                else:   
                        price = price[0].strip()
                        print(f'{wanted_game_name} is {float(price.replace(",", ".")[:-1])} €')
```

                        
At this point, you should have this:
```py
from bs4 import BeautifulSoup
import requests

wanted_game_name = wanted_game_name.lower()
found = False
steam = 'https://store.steampowered.com/search/?term='+(wanted_game_name)

#       ┌────────────────┐
#       │  page request  │
#       └────────────────┘
response = requests.get(steam)
soup = BeautifulSoup(response.text, features='html.parser')

#       ┌────────────┐
#       │  get data  │
#       └────────────┘
game_found = soup.find_all("a", class_="search_result_row")

for game in game_found:
        name = str(game.find(class_="title").contents[0]).lower()

        if name == wanted_game_name:
            price = game.find('div', class_="search_price").contents
            found = True

if found != True:
        print(f'{wanted_game_name} not found, please verify the orthograph')
else:
        if len(price) == 4:
            price = price[3].strip()
            print(f'{wanted_game_name} is {float(price.replace(",", ".")[:-1])} €')
        else:   
            price = price[0].strip()
            print(f'{wanted_game_name} is {float(price.replace(",", ".")[:-1])} €')
```

We will now make this a function to loop in a list of wanted game.
This is the final code:  

```py
from bs4 import BeautifulSoup
import requests

def get_game_price(wanted_game_name):
        wanted_game_name = wanted_game_name.lower()
        found = False
        steam = 'https://store.steampowered.com/search/?term='+(wanted_game_name)

        #       ┌────────────────┐
        #       │  page request  │
        #       └────────────────┘
        response = requests.get(steam)
        soup = BeautifulSoup(response.text, features='html.parser')

        #       ┌────────────┐
        #       │  get data  │
        #       └────────────┘
        game_found = soup.find_all("a", class_="search_result_row")

        for game in game_found:
                name = str(game.find(class_="title").contents[0]).lower()

                if name == wanted_game_name:
                        price = game.find('div', class_="search_price").contents
                        found = True

        if found != True:
                print(f'{wanted_game_name} not found, please verify the orthograph')
        else:
                if len(price) == 4:
                        price = price[3].strip()
                        print(f'{wanted_game_name} is {float(price.replace(",", ".")[:-1])} €')
                else:   
                        price = price[0].strip()
                        print(f'{wanted_game_name} is {float(price.replace(",", ".")[:-1])} €')
                        

my_game_list = ['test nul', 'Iceberg Lovecraft Tribute', 'the evil within', 'elden ring']
for game in my_game_list:
        get_game_price(game)
```  
  
<div align="center"><a href="../4. Flask app/flask-app.md">⏩ FLASK APP ⏩</a></div>   
