
## Create a new folder and run the next lines:

```
pip install "pyramid==1.10.5"
pip install ruamel.yaml
pip install Jinja2
pip install pyramid-jinja2-webpack
pip install pyramid-debugtoolbar
```  

## Inside the folder, open a python file and insert the next piece of code:

```
from wsgiref.simple_server import make_server
from pyramid.config import Configurator
from pyramid.response import Response

def hello_world(request):
    return Response('Hello World!')

if __name__ == '__main__':
    with Configurator() as config:
        config.add_route('hello', '/')
        config.add_view(hello_world, route_name='hello')
        app = config.make_wsgi_app()
    server = make_server('0.0.0.0', 6543, app)
    server.serve_forever()
```  
  
<div align="center"><a href="./django & flask.md">⏩ DJANGO & FLASK ⏩</a></div>  
