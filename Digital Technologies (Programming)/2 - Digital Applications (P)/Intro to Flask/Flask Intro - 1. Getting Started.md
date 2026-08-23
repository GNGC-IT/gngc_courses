# Flask Intro - 1. Getting Started
## Creating a new project

Whenever we work in Flask, we should work in a **virtual environment.**  
We should also use “Open Folder” on Visual Studio Code to ensure we’re running everything in the environment

|       | Steps                                                                                                                             | Explanation                                                                                                           |
| ----- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **1** | Create a new folder for your project in your Programming folder                                                                   |                                                                                                                       |
| **2** | In Visual Studio Code, **File > Open Folder**, and select the new folder                                                          |                                                                                                                       |
| **3** | Open the Command Palette with **Ctrl+Shift+P,**   <br>Then select **Python: Create Environment**. Select **venv**                 | This will create a virtual environment that will keep our project independent of the rest of our computer             |
| **4** | Open the Command Palette again (**Ctrl+Shift+P**),   <br>Go to **Terminal: Select Default Profile** and select **Command Prompt** | For the next command to work, we need to ensure that our Terminal is set to be Command Prompt rather than Powershell. |
| **5** | In the top menu, select **Terminal>New Terminal**<br>Ensure that the terminal starts with (venv)                                  | This is going to activate the new virtual environment that you created                                                |
| **6** | In the new terminal, type and run:   <br>**pip install flask**                                                                    | We have to install Flask inside the _venv_                                                                            |
## A Hello World Program
First, make a new python file called **app.py**
Add the code below, and hit run!
```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
@app.route("/home")
def home():
    return "Hello Flask!"

@app.route("/other")
def other():
    return "Welcome to a different page"  

if __name__ == '__main__':
    app.run(debug = True)
```

It will then come up with a run of information that looks like this
![[flask_run_terminal.png]]
- Type the IP Address and Port Number (127.0.0.1:5000) into your web browser, and it should show up with “Hello Flask!”
	- You can also just type in localhost:5000
- When you’re done, or want to change your code, head back to the terminal, and hit CTRL+C or the rubbish bin icon to stop the program.

## So what does it do?
If you add the "/other" to the URL, you’ll be redirected to a different page!
This is using **routes**. They control the URL of the website you’re accessing. 
You need to create functions for each different page you want it to route to, but you can have multiple routes go to one page.
The actual lines starting with the @ symbol are called **decorators**, and they modify the function that follows it (you’ll only find these in Python)

