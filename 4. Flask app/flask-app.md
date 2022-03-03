### Application Web avec Flask Python

## Installation

- Python.3.10
- pip install flask
- pip install flask_sqlalchemy
- pip install sqlite3

## Création d'une Task List

- création des différentes routes
- création des différentes opérations crud

## Lancement du projet

- py app.py 
## Démarche pour la création du projet dans le fichier App

# import de Flask et ses différents composants " 
- from flask import Flask, render_template, request, redirect, url_for

# import de flask_sqlalchemy 
- from flask_sqlalchemy import SQLAlchemy

# déclaration de la base de données uttilisée : 
- app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database/tasts.db'
- db = SQLAlchemy(app)

# déclaration de la classe utilisée :

- class Task(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    content = db.Column(db.String(200))
    done = db.Column(db.Boolean)

# Déclaration des différentes routes et commande pour lancer l'application

- @app.route('/')
- def home():
    tasks = Task.query.all()
    return render_template("index.html", tasks=tasks)


- @app.route('/create-task', methods=['POST'])
- def create():
    task = Task(content=request.form['content'], done=False)
    db.session.add(task)
    db.session.commit()
    return redirect(url_for('home'))


- @app.route('/done/<id>')
- def done(id):
    task = Task.query.filter_by(id=int(id)).first()
    task.done = not (task.done)
    db.session.commit()
    return redirect(url_for('home'))


- @app.route('/delete/<id>')
- def delete(id):
    Task.query.filter_by(id=int(id)).delete()
    db.session.commit()
    return redirect(url_for('home'))


- if __name__ == '__main__':
    app.run(debug=True)
  
  
## Utilisation d'un fichier css : main.css
  
## Dans le fichier index.html, utilisation de bootstrap ainsi que les différentes fonts et l'appel du fichier main.css
  
- <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootswatch@4.5.2/dist/lux/bootstrap.min.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Dosis:wght@600&family=Josefin+Sans:wght@100&family=Lobster&family=Nova+Round&family=Sriracha&display=swap"   rel="stylesheet">
  <link rel="stylesheet" href="{{ url_for('static', filename='main.css') }}">  
  
- création d'un formulaire dans une class "card" 
- création de 2 bouton pour "suppression" de la task et le "done"
  
## Utilisation de sqlite3, création de la base de données "tasts.db
  
- qui est par défaut avec "Pycharm" 
  
## Merci pour votre participation !  
  
<div align="center"><a href="../5. Useful links/useful-links.md">⏩ USEFUL LINKS ⏩</a></div>  