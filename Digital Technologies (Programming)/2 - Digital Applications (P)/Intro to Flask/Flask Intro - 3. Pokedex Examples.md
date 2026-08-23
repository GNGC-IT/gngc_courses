# Flask Intro - 3. Pokedex Examples
Here, we’re going to make our first mini-project, taking data from a JSON file, and displlaying it using Flask and Jinja Templates.

Let’s take a look at the JSON file we’re going to be investigating first, and I’m going to highlight the elements that we’re going to focus on displaying:

[https://raw.githubusercontent.com/Purukitto/pokemon-data.json/master/pokedex.json](https://raw.githubusercontent.com/Purukitto/pokemon-data.json/master/pokedex.json)

```json
{
    "id": 1,
    "name": {
      "english": "Bulbasaur",
      "japanese": "フシギダネ",
      "chinese": "妙蛙种子",
      "french": "Bulbizarre"
    },
    "type": ["Grass", "Poison"],
    "base": {
      "HP": 45,
      "Attack": 49,
      "Defense": 49,
      "Sp. Attack": 65,
      "Sp. Defense": 65,
      "Speed": 45
    },
    "species": "Seed Pokémon",
    "description": "Bulbasaur can be seen napping in bright sunlight. There is a seed on its back. By soaking up the sun’s rays, the seed grows progressively larger.",
    "evolution": { "next": [["2", "Level 16"]] },
    "profile": {
      "height": "0.7 m",
      "weight": "6.9 kg",
      "egg": ["Monster", "Grass"],
      "ability": [
        ["Overgrow", "false"],
        ["Chlorophyll", "true"]
      ],
      "gender": "87.5:12.5"
    },
    "image": {
      "sprite": "<https://raw.githubusercontent.com/Purukitto/pokemon-data.json/master/images/pokedex/sprites/001.png>",
      "thumbnail": "<https://raw.githubusercontent.com/Purukitto/pokemon-data.json/master/images/pokedex/thumbnails/001.png>",
      "hires": "<https://raw.githubusercontent.com/Purukitto/pokemon-data.json/master/images/pokedex/hires/001.png>"
    }
  }
```

We’re going to focus on: **Name (english), ID, Type, Species, Description,** and **Image (hires)**

First, let’s sort out what we’ll do on the Flask end.

Let’s start off by just **displaying a random Pokemon each time the page loads**

Most of this code should look familiar to you, as we’re just opening the JSON file like we have in the past, and then selecting a random Pokemon, and sending it as the variable **pok**.

```python
from flask import Flask, render_template
import json, os, random

folderPath = os.path.dirname(os.path.abspath(__file__))

with open(folderPath + '/pokedex.json', 'r',  encoding="utf8") as f:
    pokedex = json.load(f)

app = Flask(__name__)
 
@app.route("/")
def index():
     i = random.randint(0, len(pokedex)-1)
     return render_template("pokDetails.html", pok = pokedex[i])
 
if __name__ == '__main__':
   app.run(debug = True)
```

Here in our Jinja Template, we’re going to display all the desired contents of the **pok** variable, which we can treat like a dictionary, as we usually do with JSON contents.

```jinja2
<!DOCTYPE html>
<html>

<head>
    <style>
        html {
            font-family: Verdana, Geneva, Tahoma, sans-serif;
            background-color: rgb(215, 250, 248);
        }
    </style>
    <title>{{pok["name"]["english"]}}</title>
</head>

<body>
    <h1>{{pok["name"]["english"]}}</h1>
    <p>ID: {{pok["id"]}}</p>
    <p>Type: {{pok["type"]}}</p>
    <p>Species: {{pok["species"]}}</p>
    <p>{{pok["description"]}}</p>
    <img src={{pok["image"]["hires"]}}>
   
</body>

</html>
```

We should end up with something like this:

![[Registeel.png]]

## Improvements

We can make a BUNCH of improvements to this, but we’re going to focus on a couple small ones for now

- Find a specific Pokemon by their ID Number
- List details about the evolutions

### Find by ID

We’re going to keep this VERY SIMPLE for the moment, and use the URL arguments to our advantage.

With the code below, you’ll be able to type in “/ID” into the URL at the end of the address, and it should display the Pokemon in question!

Try [http://localhost:5000/25](http://localhost:5000/25) and you should get Pikachu!

```python
@app.route("/<num>")
def find(num):
     i = int(num)-1
     return render_template("pokDetails.html", pok = pokedex[i])
```

### Evolution Information

Many Pokemon evolve, and many Pokemon evolve from others. We can display some basic information about Pokemon evolution in our web app.

Let’s take a look at how evolution information is stored in the JSON. This is extracted from the Ivysaur entry:

```json
"evolution": { "prev": ["1", "Level 16"], "next": [["3", "Level 32"]] },
```

So we can look at “prev” and “next” to look at evolution to see what Pokemon (ID) they evolve from and to, and how.

We can use IF Statements to show evolution information if it is relevant:

```jinja2
{% if pok["evolution"]["prev"] != null %}
    <p>Evolves from pokemon #{{pok["evolution"]["prev"][0]}} from {{pok["evolution"]["prev"][1]}}</p>
{% endif %}
{% if pok["evolution"]["next"] != null %}
    <p>Evolves into pokemon #{{pok["evolution"]["next"][0][0]}} from {{pok["evolution"]["next"][0][1]}}</p>
{% endif %}
```

NOTE! This doesn’t work for pokemon like Eevee that have multiple evolution paths!  
~~(I didn’t want to do it).~~ This is left as an exercise for the reader. 