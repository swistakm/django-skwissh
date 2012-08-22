.. image:: http://github.com/rsaikali/django-skwissh/raw/master/doc/images/skwissh-logo.png

Introduction
============

A Django application for remotely monitoring servers using SSH.

In background (crontabed jobs) Skwissh uses Python Fabric (http://fabfile.org/) to execute SSH commands, aka. "sensors", get the output and store timestamped values.
Measures are taken every minute.

On the other side, Skwissh is able to display nice charts (linechart, piechart or simple text) with aggregated measures. 

Default sensors available (tested on Ubuntu 12.04) :

* Memory
* CPU
* WaitIO
* Load Averages
* Disk usage
* Top

But you can easily add your own ones !!

Visit the Skwissh demo at http://skwissh.com/ (username ``test`` / password ``test``).

Follow @skwissh on Twitter.

Installation
============

Configure your Django project in a normal way (database, etc...).

Add ``skwissh`` and ``kronos`` to your Django ``INSTALLED_APPS``:

::

    INSTALLED_APPS = (
        ...
        'kronos',
        'skwissh',
    )

Add Skwissh to your ``urls.py``:

::

    # Skwissh
    url(r'^skwissh/', include('skwissh.urls')),

Synchronize your database (this command will load defaut sensors through fixtures):

::

    ./manage.py syncdb
    
Install Skwissh tasks (will write to your user crontab, thanks to 'django-kronos'):

::

    ./manage.py installtasks
    
You can check that 4 crontab job have been configured:

::

    crontab -l

If you want to activate i18n (French & English currently supported), follow the next steps:

In your project ``settings.py``, add the Django ``LocaleMiddleware`` and set the ``LANGUAGES`` variable:

::

	MIDDLEWARE_CLASSES = (
		...
        'django.middleware.locale.LocaleMiddleware',
        ...
    )

    LANGUAGES = (
        ('fr', 'Français'),
        ('en', 'English'),
    )

You're ready to go ! 
Connect to the application and start configure your servers and sensors !

Screenshots
===========

Load averages
~~~~~~~~~~~~~
.. image:: http://github.com/rsaikali/django-skwissh/raw/master/doc/images/loads-screenshot.png

Disk usage
~~~~~~~~~~
.. image:: http://github.com/rsaikali/django-skwissh/raw/master/doc/images/diskusage-screenshot.png

Top output
~~~~~~~~~~
.. image:: http://github.com/rsaikali/django-skwissh/raw/master/doc/images/top-screenshot.png

Server edition
~~~~~~~~~~~~~~
.. image:: http://github.com/rsaikali/django-skwissh/raw/master/doc/images/editserver-screenshot.png

Sensor edition
~~~~~~~~~~~~~~
.. image:: http://github.com/rsaikali/django-skwissh/raw/master/doc/images/editsensor-screenshot.png

Credits
=======

* Uses Django 1.4.1 (https://www.djangoproject.com).
* Uses Django applications and addons :

  - django-kronos (https://github.com/jgorset/django-kronos) from Johannes Gorset (https://github.com/jgorset).
  - django-extra-views (https://github.com/AndrewIngram/django-extra-views) from Andrew Ingram (https://github.com/AndrewIngram). 

* Uses Fabric (http://fabfile.org) SSH Python library.
* Uses jqPlot (http://www.jqplot.com) jQuery plotting and charting library.
* Uses Zurb Foundation (http://foundation.zurb.com) responsive CSS/JS/HTML bootstrap.
* Includes icons from TheNounProject (http://thenounproject.com).