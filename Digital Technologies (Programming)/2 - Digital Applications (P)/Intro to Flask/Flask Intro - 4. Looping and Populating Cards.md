# Flask Intro - 4. Looping and Populating Cards
Cards generally refer to a UI component used to present concise and visually appealing information.

We’re going to use a FOR Loop to create many cards for our web app.

Everything we do here you can use any time you’re trying to display arrays and dictionaries worth of data

We’re going to continue using the Pokedex JSON file for this.

### Card Design

First thing we need to do is design a little Card for ourselves to use. This is going to be mostly working in CSS.

At the moment for simplicity, I’ll continue working inside the Style section rather than a separate file.

Here’s the HTML and CSS for a single card:

```jinja2
<div class="card">
    <img src={{pok["image"]["hires"]}} width="200px" height="200px">
    <div style="float: right; width: 360px;">
        <h1>{{pok["name"]["english"]}}</h1>
        <p>ID: {{pok["id"]}}</p>
        <p>Type: {{pok["type"]}}</p>
        <p>Species: {{pok["species"]}}</p>
        <p>{{pok["description"]}}</p>
    </div>
</div>
```

```css
.card {
    width: 600px;
    border: 2px solid black;
    border-radius: 10px;
    padding: 10px;
    display: block;
    overflow: auto;
    margin-top: 20px;
}
```

![[bulba-card.png]]

## Displaying the original 151

```python
@app.route('/kanto/') 
def kanto(): 
    return render_template("index.html", pokemon = pokedex[0:151])
```

```jinja2
<!DOCTYPE html>
<html>

<head>
    <style>
        html {
            font-family: Verdana, Geneva, Tahoma, sans-serif;
            background-color: rgb(215, 250, 248);
        }

        .card {
            width: 600px;
            border: 2px solid black;
            border-radius: 10px;
            padding: 10px;
            display: block;
            overflow: auto;
            margin-top: 20px;
        }
    </style>
    <title>Pokedex</title>
</head>
<body>

    {% for pok in pokemon%}
    <div class="card">
        <img src={{pok["image"]["hires"]}} width="200px" height="200px">
        <div style="float: right; width: 360px;">
            <h1>{{pok["name"]["english"]}}</h1>
            <p>ID: {{pok["id"]}}</p>
            <p>Type: {{pok["type"]}}</p>
            <p>Species: {{pok["species"]}}</p>
            <p>{{pok["description"]}}</p>
        </div>
    </div>
    {% endfor %}

</body>
</html>
```

![[pokedexCards.gif]]