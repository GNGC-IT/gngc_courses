# Flask Intro - 2. Working with Templates
Templates are used to create dynamic HTML content that can be rendered and displayed in response to user requests.
Templates help separate the logic of your Python code from the presentation of your web pages, which follows the basic principles of web development (keeping this separate, HTML, CSS, JS, etc)
The templating engine used is **Jinja2**

### Jinja Syntax
`{{....}}` are expressions used to print to template output
`{%....%}` are for statements
`{#....#}` are for comments which are not included in the template output

## Flask Project Structure
```
my-flask-app/
   ├── static/
   │   └── css/
   │       └── styles.css
   ├── templates/
   │   └── index.html
   └── app.py
```

First, we need to look at our folder structure again.
All templates need to be in our project folder, inside a folder called “**templates**”. You can name the actual file anything you like, but they must be in that folder.
Inside the `templates` folder, create a file inside it called **index.html**. We'll add the code to it soon.

While we're looking at this, make a folder called **"static"** as well. This is going to hold any files that we're going to load on our front-end (CSS Stylesheets, Javascript files, images, etc.)


## app.py - Python Code
```python
from flask import Flask, render_template
import os

app = Flask(__name__)
 
menu = ["Burgers", "Chips", "Drink"]

@app.route('/')
def test():
    return render_template("index.html", user = os.getlogin(), array = menu)

if __name__ == '__main__':
    app.run(debug = True)

```
This is the Flask code that we're going to use for this little test.
- We've created a list called "menu" containing three strings.
- When the user goes to the root directory of the web application, Flask is going to **render a template**, and send it two variables
	- A variable called `user` that will take the name of the currently logged in user on the computer that you're running the code on
	- A variable called `array`, which will be our `menu` we created earlier.

So how do we use our variables that we've passed to the HTML?
## index.html - HTML code with Jinja Templating
```jinja2
<!DOCTYPE html>
<html>

<head>
    <title>My Hello World Site</title>
</head>

<body style="font-family: Arial, Helvetica, sans-serif;">

    <p>{{user}}</p>
    <ol>
        {% for item in array %}
            <li>{{item}}</li>
        {% endfor %}
    </ol>
</body>

</html>
```

You can see two key demonstrations here:
- When we want to display variables directly, we can use `{{variable_name}}` to display it
- We can loop through lists (or any type of collection technically) using: 
	- `{% for new_variable in list_variable %}`
	- It works just like it would in Python, but since we're dealing in a HTML landscape, we need an opening and a closing statement, so we need to be careful to remember the `{% endfor% }`as well
	- What we can specifically expect, is that our webpage is going to display an ordered list, with each element of our list being rendered as a list item

## IF Statements
Here's a quick little demo of how to use IF statements!
It's a mild simplification, but I'm sure you recognise that this is a pretty common use case!
```python
@app.route('/login')
def loginTest():
    return render_template('dashboard.html', user="Alex")
```

```jinja2
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Dashboard</title>
</head>
<body>
    {% if user is defined %}
        <h1>{{ user }}'s Dashboard</h1>
        <p>Welcome back!</p>
    {% else %}
        <h1>Guest Dashboard</h1>
        <p>Please log in to continue.</p>
    {% endif %}
</body>
</html>
```

`% if user is defined %}` checks to see if the variable `user` is sent to the frontend, or if it equals `null`. If it's a defined variable with a value, then we're going to show the details for the user. If it wasn't sent at all, or if it was sent but equals `null`, then we'll do the "Guest Dashboard".

