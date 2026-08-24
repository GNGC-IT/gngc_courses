## Displaying a list on a single line
```jinja2
        <div class="game-card">
            <h2>{{g["title"]}}</h2>
            <p>
                {%for gnr in g["genres"]%}
                {{gnr}},
                {%endfor%}
            </p>
        </div>
```

The key element here is the `{%for gnr in g["genres"]%}`, which loops through the contents of the `genres` key ( a list of the genres)
All inside of the one set of pragaraph tags, it loops through the items in the list, adding a comma after each item.
There is a way to make the ensure there isn't trailing comma after the last item, but that's for you to work out!

## Using URL Arguments
Being able to select the exact item you want to display from a data set is really useful!

This route below, takes the ID number that the user enters into the URL (or, is linked like below), and finds the details of the item in the data source. 

```python
@app.route("/g/<int:id>")
def by_id(id):
    return render_template("game.html", game = game_data[id])
```

- You can see that the route is `/g/<int:id>`
	- The g is there so we know we're looking under a specific path in the URL (in this case, g stands for game)
	- The URL then accepts an integer, and sends it to the function as the variable called `id`
- We then render a template based on the sent ID number

>[!NOTE]+ What if the ID Number doesn't start at zero?!
>Currently, this will only work if the dataset has an ID field, and the ID field starts at 0
>If your data set has an ID field that starts at 1, then you should look at the example below, from our Pokedex practice! We just need to be careful in places to take away 1 from the ID number.
```python
@app.route("/p/<int:id>")
def find(id):
     i = id-1
     return render_template("pokDetails.html", pok = pokedex[i])
```

## Placing DOM Objects next to each other
There are a LOT of ways to do this, but the easiest (and also most janky), is to just give them both the styling of `float:left`.
This is going to get them to float next to each other.
In order for them to look **actually nice**, you will need to also give one or both of them some margin.
Take a look at my example below!

```jinja2
<img src="{{game['poster']}}" width="200" height="300" style="float: left;">
<div style="float: left; margin-left: 30px;">
	<h1>{{game["title"]}}</h1>
	<h4 style="color:#666666">Released on {{game["release_date"]}}</h4>
</div>
```

You can see the image has the style `float: left` as the inline styling
The div has the style of `float: left; margin-left: 30px`
This will give the whole block the ability to go next to the image, and it will also make sure that it isn't directly next to it either.
Putting all the text content inside the div makes it nice and easy!

## Linking cards to a page
It's nice to be able to link whole cards to another page, so that if the user clicks anywhere on a card it will take them to a full page description of the card's summary.

```jinja2
<a href="/g/{{g['id']}}">
	<div class="game-card">
		<h2>{{g["title"]}}</h2>
		<p>
			{%for gnr in g["genres"]%}
			{{gnr}},
			{%endfor%}
		</p>
	</div>
</a>
```

Here, you can see that the opening and closing tags wrap around the div that defines the card.
This will make the whole div act as a link!
But take a look at it now:
![[unstyled-linked-card.png]]
YUCK! I still want it to look as it did before.
We can just set up some styling for the `<a>` tags in our CSS, so that our text colour and decoration is just "default"
```css
a {
    color: black;
    text-decoration: none;
}
```
Set the colour to whatever you want the text colour on your webpage to be, and `text-decoration: none` will turn off any underlining that is happening.

### The CSS for that card if you're interested
```css
.game-card {
    border: solid 1px black;
    width: 400px;
    height: 200px;
    margin-bottom: 20px;
    margin-right: 20px;
    padding-left: 20px;
    float: left;
}
```