Getting Started with Python on Heroku
=====================================
(Adapted from [https://github.com/jamesward/hello-python-flask](https://github.com/jamesward/hello-python-flask))

Some of the libraries involved here are only for Python 2.7, so you must first [install that version of Python](https://www.python.org/downloads/).

Now, make sure you have the latest version of **pip**:

    python -m pip install -U pip

Next, make sure you have virtualenv installed:

    virtualenv --version

If this gives you an error message, run:

    pip install virtualenv
-----------------
# Quick Start on Windows #

To experiment locally on Windows (before deploying on Heroku) I've gone through the various thrashings-around and tried to capture and simplify things.

**Flask-SocketIO** relies on **gevent** which in turn relies on **greenlet**, both of which are binaries. You can figure out how to install the right [Microsoft Visual C++ Compiler](http://www.microsoft.com/en-us/download/confirmation.aspx?id=44266 "Microsoft Visual C++ Compiler") and configure it so that you don't get the message about not finding **vcvarsall.bat** file, but I couldn't figure that out and I eventually discovered that I could install directly from the *wheel* files. I've included the wheel files in this distribution, and you'll see that in **setup2.bat** the **pip** commands to directly install the wheel files precede the **pip** install using **requirements.txt**. This seems to work (but note that my particular wheel files might be out of date when you read this).

Now, for your local Windows testing you should be able to run:

		setup1.bat
		setup2.bat
 
And then be ready to start the app:

		python main.py

If that succeeds, you should be able to [open a local page](http://localhost:5000) and see the results.

The **go.bat** and **bye.bat** allow you to quickly enter and leave the **virtualenv**.

-----------
**Note**: this initial version is taken directly from [Miguel Grinberg's example](https://github.com/miguelgrinberg/Flask-SocketIO). The goal was to get it going, and then see if it could be launched on Heroku.

-----------
# Run Locally #

1. Setup virtualenv

        virtualenv venv --distribute

2. Activate virtualenv:

    Mac/Linux:

    source venv/bin/activate

  Windows (you can also just type "go"):

        venv\Scripts\activate.bat

3. Get the deps:

        pip install -r requirements.txt

4. Start Flask Server

        python main.py

5. Test out the app

    [http://localhost:5000](http://localhost:5000)


Run on Heroku
-------------

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
* When you change **main.py**, Flask's automatic refresh doesn't work. You have to kill it and restart it to see the results. The refresh only seems to work on templates.
* Here's information from Heroku on [using websockets with python](https://devcenter.heroku.com/articles/python-websockets).
