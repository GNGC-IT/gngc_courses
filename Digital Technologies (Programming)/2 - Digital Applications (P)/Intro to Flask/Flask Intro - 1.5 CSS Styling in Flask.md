A quick note that I should probably place here!

It's usually best practice to keep all your CSS Styling in a css file, rather than including in on a page-by-page basis in the `<style>` tags in the head of the HTML file.

This gives us a bunch of advantages
- You only write it once, and any time you make a new page, you just link it to your existing CSS file
- Any changes you want to make to your website's style (from small changes, to large) you only have to change it **in one place**

## A basic CSS file
Here's the basis for the plainest (but essential CSS I usually use)
In a flask project, the file should be called `styles.css`, and it should be stored inside of a folder called `static`.
```css
html {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    background-color: rgb(215, 250, 248);
}

table,
th,
td {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 5px;
}

```

## Referencing it in the HTML
This is what your head should look like in your HTML:
```jinja2
<head>
   <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
   <title>Some Title</title>
</head>

```

You can see there, Flask uses Jinja's `url_for` function to lookup the CSS file inside the static folder.
We use the `url_for` any time we need to render a stored asset on the frontend (CSS files, JavaScript files, sometimes JSON files, and most importantly, images stored on the server)