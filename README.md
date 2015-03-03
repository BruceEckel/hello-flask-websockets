Getting Started with Python on Heroku
=====================================

Run Locally
-----------

1. Setup virtualenv

        virtualenv venv --distribute

2. Activate virtualenv:

        source venv/bin/activate

3. Get the deps:

        pip install -r requirements.txt

4. Start Flask Server
    
        python web.py

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

