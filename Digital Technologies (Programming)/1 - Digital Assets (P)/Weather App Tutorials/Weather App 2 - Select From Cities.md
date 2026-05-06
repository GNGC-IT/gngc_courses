# Weather App Part 2 - Selecting from Cities
Now we have some basics working, let's allow the users to choose from a few options for where they want to check the weather.


## Location Data
The way that I would like to tackle this, is by creating a dictionary object that will store the Lat and Lon for a small set of cities. Here's mine, feel free to use it!

```python
cities = {
    "Canberra": {
        "Lat": -35.282001,
        "Lon": 149.128998
    },
    "Sydney": {
        "Lat": -33.868820,
        "Lon": 151.209290
    },
    "Melbourne": {
        "Lat": -37.813629,
        "Lon": 144.963058
    },
    "Brisbane": {
        "Lat": -27.469771,
        "Lon": 153.025124
    }
}
```
Pop that at the top of your code to live in your "global variables and constants" section.

## Let the User choose
Next, we need to add the options to the UI. I've decided to go with a drop-down box, and I'm going to structure it so that my City drop-down will go right next to the "Check Weather" button.

Here's my little GUI code that I've added to my window:
```python
    with dpg.group(horizontal=True):

        dpg.add_combo(items=list(cities.keys()), default_value="Canberra", tag="city", width=200)

        dpg.add_button(label="Check Weather", callback=check_weather)
```
And here's how it looks:
![[Pasted image 20260506124111.png]]

## Show the weather for the set city
Next, we just need to make sure that our `check_weather` function will use the selected city!

We just need to tweak the first few lines of that function, like so:
```python
def check_weather():
    city = dpg.get_value("city")
    lat = cities[city]["Lat"]
    lon = cities[city]["Lon"]
    ...
```

## Check if it works!
With those little changes, we should have that little feature working!
Run it, and see if it works:
![[Weather Part 2.gif]]


## Extension ideas
Of course, this is fairly limited! Two ways to make it more interesting:
- Add more cities to the dictionary
	- Fairly easy to do, just a bit of googling!
- Implementing a search function
	- It's absolutely possible to connect this with OpenWeather's Geolocation API, where you can basically send a city name string to the API, and it will send you back the Lat and Lon for the city, so you can then get the weather for it.
	- Watch out though! There are some cities that share a name with other cities; how are you going to make sure that you're giving the user the information for the correct Newcastle or Perth?