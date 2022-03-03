<h1 align="center">Python's big guns</h1>  
<div align="center"><img src="https://www.mattlayman.com/img/2021/django-flask.png" alt="DjangoFlask" width="350px"/></div>  

---  

## Hello world by Flask        
    
```  
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"

app.run(host='0.0.0.0', port=81)
```  
  
## Hello world by Dja... Oh, wait  

Any idea why it's not exactly the smartest plan?  
Here's a small hint:  

![Gordon's Knife](https://images-cdn.9gag.com/photo/apNxZjM_700b.jpg)  

<div align="center"><a href="../3. Web scraping/web-scraping.md">⏩ WEB SCRAPING ⏩</a></div>        