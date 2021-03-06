Ushahidi online-offline Reporting Web Application
------------------------------------------------

    https://sites.google.com/site/onlineofflinewebapps/ushahidi-webapp

How to start
------------

  Build the project:

    $ cd /var/www/
    $ git clone git://github.com/axaroth/ushahidi-webapp.git oo-report
    $ cd ushahidi-dev
    $ python2.6 bootstrap.py
    $ ./bin/buildout

  Start the http server:

    $ ./bin/serve-static

  Rules for Apache:

    RewriteRule ^/oo-report/(.*) http://127.0.0.1:8005/$1 [P,L]
    <Directory /var/www>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>


What we used
------------

    Development http server

        zc.buildout, Paste and PasteScript (and other Python libraries)

    WebApp

        jQuery JavaScript Library v1.5
            http://jquery.com/

        jQuey Mobile 1.0a3
            http://jquerymobile.com/

        geo-location-javascript v0.4.3
            http://code.google.com/p/geo-location-javascript/

        persistence.js
            http://persistencejs.org/

How it works
------------

    default.ini

        Configuration for 'paste serve' script (simple http server)

    ushahidi.reporting.webapp

        Provides the html5 manifest generation and a fake Ushahidi API
        for testing purpose.

    index.html

        This page contains the html to render the interfaces and loads
        the application code and libraries.

    interview.db.js

        Setup the DB and provides the functions to manage the collected
        data.

    interview.mobile.js

        It contains the code that manages the user interfaces and the
        actions on the forms.


NOTE: How 'upload picture' works

    - data store
    1. get the file (fs path) from the form
    2. transform the file in base64 encoding

    - data send
    1. get the base64 encoding from DB
    2. create a blob from the enconding using blob builder: https://developer.mozilla.org/en/DOM/BlobBuilder
    3. create the FormData object and append the blobfile)

    options:
        4. send the FormData object using XMLHttpRequest: http://www.html5rocks.com/en/tutorials/forms/html5forms/#toc-form-data-object
        4. send the FormData object using $.ajax:http://stackoverflow.com/questions/5392344/sending-multipart-formdata-with-jquery-ajax
