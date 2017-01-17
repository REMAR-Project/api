REMAR/Crabbler-Web
==================

This is the server side web component for the REMAR citizen science Mangrove crab study.

Running REMAR/Crabbler-web
==========================

Crabbler-web should be deployed using uWSGI as the app server but it should run perfectly happyily using the Flask development server. Assuming that you have Pip, VirtualEnv and CouchDB installed, cd into the case.study/daybook/ directory then create a new virtualenv:
    $ cd case.study/daybook/
    $ virtualenv env

Start your virtualenv then install the external libraries using the supplied requirements.txt
    $ source env/bin/activate
    $ pip install -r requirements.txt

Now create a var/ directory to store log files from the running app and create an empty log file ready for data:
    $ mdkir var
    $ touch var/daybook.log

Now create a data/ directory where uploaded json files can be stored:
    $ mkdir data


Finally, we want Crabbler-web to run with the src directory as a sub-directory of our application root (mainly so that the etc/ and var/ directories are located correctly relative to the running app) so cd to the crabbler-web folder then start the app as follows:
    $ python src/crabbler_web.py

Now open a browser and navigate to http://localhost:5000/

There isn't much to see as this server app is, for the moment, mostly aimed at consuming data from the crabbler Android app. However, you can test the routes using the JSON API and the cURL command line tool as describer in the section "Using the API".

Run the tests
=============

Add application src to the PYTHONPATH:
    $ PYTHONPATH=`pwd`/src/crabbler-web

Run the tests:
    $ python test/crabbler-web/crabbler-web_test.py

Using the API
=============

You can call the upload route, using a suitable JSON document as a payload as follows:

    $ curl -H "Content-type: application/json" http://localhost:5000/up -X POST  -d @test.json 

Which should get you a response similar to the following:
    {
      "message": "File Uploaded to data/2017-01-17T18:54:33.683936_e44aeafe-64bc-4099-a38d-124ba1147287.json", 
      "status": "ko", 
      "statuscode": 200
    }

