# Weather App Part 1 - Getting Started
Let's get started on making our Weather App!
First, let's recap the requirements:


>Your weather app should be able to display the following information:
>- The user should be able to select from at least three different locations
>- The current weather for a location
>	- This can be just the current specifics (temperature, with current weather), or you might like to include the upcoming hourly forecast
>- The predicted weather for the next week
>	- This must include at least the high and low temperatures, along with the general weather prediction (rainy, sunny, etc.)

So let's get a bit of a plan going for how we're going to tackle this. There's a few ways we can order it, but because I want to go in order of difficulty, let's go in this order:
1. Get the current weather for a set location
2. Allow the user to choose between a few different locations
3. Show the user the week's forecast for the chosen location

## Showing the Current Weather
I'm going to assume that you've worked through the content on Google Classroom for making the Weather API work in the console, and now we're going to start implementing it into the GUI

### GUI Structure
First, before we implement any functionality, let's give ourselves a bit of a template for the DearPyGUI package for us to build from, and I'm also setting up the starter window for us to build from.

```python
import requests, json, os
from datetime import datetime
import dearpygui.dearpygui as dpg

folder_path = os.path.dirname(os.path.abspath(__file__))

#Helper Functions
def check_weather():
    pass

dpg.create_context()

with dpg.window(label="Weather App", width=600, height=600):
    dpg.add_button(label="Check Weather", callback=check_weather)
    dpg.add_spacer(height=10)
    dpg.add_separator()
    dpg.add_spacer(height=10)

    dpg.add_text("", tag="time")

    dpg.add_spacer(height=10)
    dpg.add_separator()
    dpg.add_spacer(height=10)

    dpg.add_text("Current Weather")
    dpg.add_text("", tag="temp")
    dpg.add_text("", tag="weather")

dpg.create_viewport(title="Weather App", width=600, height=600)
dpg.setup_dearpygui()
dpg.show_viewport()
dpg.start_dearpygui()

dpg.destroy_context()
```

Let's break down the current content:
1. A "Check Weather" button. This currently has a callback function that is empty, we're going to write that function next!
2. A few text fields that don't have any text at the moment; we are going to fill them with data in our `check_weather` function. These are `time`, `temp` and `weather`
3. Some separators and spacers to try to keep things neat and tidy!

Result:
![[Pasted image 20260505102736.png]]

### The `check_weather` function
Ok, let's replace the current version of the `check_weather` function with this new version. It's very similar to the work we've already completed, and the code provided over on Google Classroom. I've just adapted it so that it's going to print to the GUI rather than the console!

```python
def check_weather():
    lat = -35.282001 #Lat and Lon for Canberra
    lon = 149.128998
    exclude = "hourly,minutely,alerts"
    appid = "db5620faef0a378e1f0a1ac502088363"
    units = "metric"

    apiCall = f"https://api.openweathermap.org/data/3.0/onecall?lat={lat}&lon={lon}&exclude={exclude}&appid={appid}&units={units}"

    r = requests.get(url=apiCall)
    print(r.status_code)
    data = r.json()

    dpg.set_value("temp", "Current Temp: " + str(data["current"]["temp"]) + "°c")
    dpg.set_value("weather", "Weather: " + str(data["current"]["weather"][0]["description"]).capitalize() )

    time = data["current"]["dt"]
    time = datetime.fromtimestamp(time)
    dpg.set_value("time", time.strftime("%A, %d/%m/%Y, %H:%M%p"))
```

Let's take a closer look!
- First section is setting up the variables to use in our API Call
- We then build the API call string with those variables
- Make the API call with requests, check the Status Code, and then pull the data out of it to it's own variable for easy use
- Set the `temp` and `weather` text labels on the GUI directly, since they're pretty easy to handle
- Convert the datetime epoch returned to us to the current date and time, and set the `time` text label to the output with our "string from time" formatted string.

### Current Version 
There's the basics! Next we'll get the user to be able to select between a few different cities!
![[Weather Part 1.gif]]