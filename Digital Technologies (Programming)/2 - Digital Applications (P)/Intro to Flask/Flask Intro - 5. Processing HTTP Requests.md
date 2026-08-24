# Flask Intro - 5. Processing HTTP Requests
HTTP methods are a set of request types that a client (like a web browser) can make to a server when interacting with a web application.

In the context of Flask, these methods play a crucial role in handling different types of requests.

We USUALLY only will be using GET and POST requests.

|**Request**|**Purpose**|
|---|---|
|GET|The most common method. A GET message is send, and the server returns data|
|POST|Used to send HTML form data to the server. The data received by the POST method is not cached by the server.|
|HEAD|Same as GET method, but no response body.|
|PUT|Replace all current representations of the target resource with uploaded content.|
|DELETE|Deletes all current representations of the target resource given by the URL.|

So far we have only used the GET request, and that happens every time we **get** the HTML displayed on our browser.

The **POST** request is made when you use a **form** in a HTML page (although there are many other ways to make a POST request, this is most common for us)

We are going to build a form into our Pokedex website to be able to search for a Pokemon.

For simplicity, we’ll just be searching by ID, but if you’d like to search by name you can do that too (though it will be much more complicated)

## Deciding how to do this within our website

There are a lot of different ways we could implement a search function within our website

1. A search bar in a navigation bar
2. A dedicated search page that returns the result on the same page
3. A dedicated search page that returns the result on a different page

For simplicity, right now we’re going to go with option 3, because we already have a page where we can display Pokemon based on their ID, so all we need to do is build in the actual search page.

## Adding a Form to the HTML

Creating a form isn’t too tricky, but there are a couple of things to note about this one:

- For them to work as intended here, you **must set the method to be “post”**
- Here, we're going to give the form the `action` tag, with the argument of `/search`. This is going to tell the form that it is going to send us to the `/search` route when we click the submit button.
- Using the **label** tags is the best practice
- The button giving the “submit” type is also required.

```html
<form action="/search" method="post">
   <label for="pokemon-id">Select a pokemon by ID:</label>
   <input id="pokemon-id" name="id" />
   <button type="submit">Submit</button>
</form>
```

I’m going to let you do the rest of the webpage for this one, it’s pretty easy! You can actually just go and add to the top of any of our existing webpages!

To access the contents of a form, you need to use the **request** object. From it, you can check:
- the request method, to see if it was a GET or POST request
- the data from the form

You need to make sure you have added the viable request methods to the decorator above the function as well.

```python
@app.route("/search", methods=["POST"])
def search():
   i = int( request.form["id"])
   if i > len(pokedex) or i <= 0:
       i = 0
   return redirect(url_for("by_id", id = i))

```

You need to ensure that you have imported the following objects from flask:

```python
from flask import Flask, render_template, request, redirect, url_for
```

- request is for handling POST requests (usually through forms)
- redirect is used for pushing the logic path to another function in the flask app
- url_for is for handling URLs, since we don’t want to be making specific URLs, when we can make them relative like this