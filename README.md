Websockets in Flask on Heroku
=====================================
<a href="http://flask.pocoo.org/"><img
   src="http://flask.pocoo.org/static/badges/flask-powered.png"
   border="0"
   alt="Flask powered"
   title="Flask powered"></a><br/>
(With inspiration from [https://github.com/jamesward/hello-python-flask](https://github.com/jamesward/hello-python-flask))

**Note**: this example is taken directly from [Miguel Grinberg's example](https://github.com/miguelgrinberg/Flask-SocketIO). The goal was just to get it going, and then see if it could be launched on Heroku.

-----------
Some of the libraries involved here are only for Python 2.7, so you must first [install that version of Python](https://www.python.org/downloads/).

Although the most recent versions of Python do install **pip**, for some reason it's an old version. To get the latest version of [pip](https://pip.pypa.io/en/latest/user_guide.html):

    python -m pip install -U pip

Next, make sure you have virtualenv installed:

    virtualenv --version

If this gives you an error message, run:

    pip install virtualenv

-----------------
# Quick Start on Windows #

(Tested on Windows 7 and Windows 8).

To experiment locally on Windows (before deploying on Heroku) I've gone through the various thrashings-around and tried to capture and simplify things.

**Flask-SocketIO** relies on **gevent** which in turn relies on **greenlet**, both of which are binaries. You can figure out how to install the right [Microsoft Visual C++ Compiler](http://www.microsoft.com/en-us/download/confirmation.aspx?id=44266 "Microsoft Visual C++ Compiler") and configure it so that you don't get the message about not finding **vcvarsall.bat** file, but I couldn't figure that out and I eventually discovered that I could install directly from the [wheel files](http://wheel.readthedocs.org/en/latest/). I've included the necessary wheel files in this distribution, and you'll see that in **setup2.bat** the **pip** commands to directly install the wheel files precede the **pip** install using **requirements.txt**. This seems to work (but note that my particular wheel files might be out of date when you read this).

Now, for your local Windows testing you should be able to run:

	setup1.bat
	setup2.bat
 
And then be ready to start the app:

	python main.py

If that succeeds, you should be able to <a href="http://localhost:5000" target="_blank">open a local page</a> and see the results.

The **go.bat** and **bye.bat** allow you to quickly enter and leave the **virtualenv**.

The Heroku deploy ignores the **.bat** files and just uses the **requirements.txt** which does the normal builds (using Heroku's C++ compiler).

-----------
# Run Locally on Mac/Linux #

1. Setup virtualenv

        virtualenv venv --distribute

2. Activate virtualenv:

		source venv/bin/activate

3. Get the dependencies:

        pip install -r requirements.txt

4. Start Flask Server

        python main.py

5. Test out the app by <a href="http://localhost:5000" target="_blank">opening a local page</a> to see the results.


------------------
# Run on Heroku #

1. Create the app

        heroku create -s cedar

2. Deploy the app

        git push heroku master

3. Open the app in your browser

        heroku open

### Nicer alternative: ###
Log onto Heroku.com, then follow the instructions to connect to your github repository and launch your app. This can include auto-deployment every time you update your Github repository!

Notes
-------------
* [Flask main site](http://flask.pocoo.org/).
* [Flask documentation](http://flask.pocoo.org/docs/0.10/).
* When you change **main.py**, Flask's automatic refresh doesn't work. You have to kill it and restart it to see the results. The refresh only seems to work on templates.
* Here's information from Heroku on [using websockets with python](https://devcenter.heroku.com/articles/python-websockets).
* Here are lots of [prebuilt wheel binaries](http://www.lfd.uci.edu/~gohlke/pythonlibs/).
* Here is a [special version of Microsoft Visual C++ for Python 2.7](http://www.microsoft.com/en-us/download/details.aspx?id=44266). After installing it I still got the ["cannot find vcvarsall.bat" error](http://stackoverflow.com/questions/2817869/error-unable-to-find-vcvarsall-bat) so I gave up and went with wheels instead.
* The [Flask-SocketIO Github page](https://github.com/miguelgrinberg/Flask-SocketIO).
* The [Flask-SocketIO Docs](http://flask-socketio.readthedocs.org/en/latest/).
* An alternative [Flask websocket library](https://github.com/kennethreitz/flask-sockets).
* [Miguel Grinberg's tutorial](http://blog.miguelgrinberg.com/post/easy-websockets-with-flask-and-gevent).
* If you run [**pip freeze**](https://pip.pypa.io/en/latest/reference/pip_freeze.html) once everything is running (inside a virtualenv so you don't get anything that isn't necessary for your project), you can redirect the results right into your **requirements.txt**. However note that in this project most of those lines are redundant.
* If you deploy to Heroku and it doesn't work you should [view the logs](https://devcenter.heroku.com/articles/getting-started-with-python#view-logs).
* [Virtualenvwrapper](http://docs.python-guide.org/en/latest/dev/virtualenvs/#virtualenvwrapper) is designed to make virtualenv easier to use. However, it's designed for *nix-based systems.

