# Flask Intro - 6. Template Inheritance and a `base.html`

## The current problem
So right now when we create a new HTML page for our website, we need to recreate a bunch of existing code:
- CSS and JS file links 
- Navigation Bar
- General structure
- Footer (if you like)
There’s usually a lot of HTML code in common between pages, so we can use **inheritance** to create a base html page that we can expand on.

## Inheritance Recap
Inheritance is an OOP concept that refers to defining a **Parent** or **Base** object, so we can then expand on it in **children**.

In classes, you create a basic class, and then expand on it in the children. Any variables or functions created in the parent class become accessible to the children, and then allow for distinct functionality.

## What is repeatable?
```jinja2
<!DOCTYPE html>
<html>
   <head>
   <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
		<title>{{pok["name"]["english"]}}</title>
   </head>
   <body>
       <nav>
           <a href="/">Random Pokemon</a>
           <a href="/kanto">Gen 1</a>
       </nav>
       <form action="/search" method="post">
           <label for="pokemon-id">Search a pokemon by ID:</label>
           <input id="pokemon-id" name="id" />
           <button type="submit">Search</button>
       </form>

       <h1>{{pok["name"]["english"]}}</h1>
       <p>ID: {{pok["id"]}}</p>
       <p>Type: {{pok["type"]}}</p>
       <p>Species: {{pok["species"]}}</p>
       <p>{{pok["description"]}}</p>
       <br>
       <img src={{pok["image"]["hires"]}}>
   </body>
</html>
```

Looking at this code here, there are only two sections that need to be exclusive to this specific page
- The Title of the webpage 
	- In this case, we're displaying the rendered pokemon's name as the title
- The main content of the webpage 
	- Everything from the H1 with the pokemon's name, down to it's image

Everything else can be on every webpage in our website!
- The Styling settings
- Navigation bar
- Search function is great to have on every page!

## Implementation
So how do we implement it?
In our `base.html` file, we create **blocks**, and then in our templates that inherit from it, we just fill in those blocks.

You can see here, our `base.html` has all the essential code, and defines a **title** block and a **content** block (which is for the main content of the webpage)
### `base.html`
```jinja2
<!DOCTYPE html>
<html>

<head>
   <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
   <title>{% block title %}{%endblock%}</title>
</head>

<body>
   <nav>
       <a href="/">Random Pokemon</a>
       <a href="/kanto">Gen 1</a>
   </nav>
   <form action="/search" method="post">
       <label for="pokemon-id">Search a pokemon by ID:</label>
       <input id="pokemon-id" name="id" />
       <button type="submit">Search</button>
   </form>

   {% block content %}

   {% endblock %}
</body>

</html>


```

### pokemon.html
Our pokemon page (which renders the details of a single pokemon), has just three sections:
- References the `base.html` template, so Flask knows to inherit most of the details from there
- Then just fills in the contents of the Title and Content blocks.
```jinja2
{% extends "base.html" %}

{% block title %} {{pok["name"]["english"]}} {% endblock %}

{% block content %}
   <h1>{{pok["name"]["english"]}}</h1>
   <p>ID: {{pok["id"]}}</p>
   <p>Type: {{pok["type"]}}</p>
   <p>Species: {{pok["species"]}}</p>
   <p>{{pok["description"]}}</p>
   <br>
   <img src={{pok["image"]["hires"]}}>
{% endblock %}


```
