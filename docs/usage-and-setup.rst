Usage and Setup Instructions
============================

Usage
-----

**Running the development server**

After following the `Setup Instructions`_ you can work on your project again by doing the following. ::

$ workon example
$ ./manage.py runserver


**Editing the SCSS/CSS**

First from the root of the project install compass and bootstrap-sass. This requires that your first install `bundler <http://bundler.io/>`_. ::

$ bundler install

Then you can run ``compass watch`` which will watch for changes to your SCSS files (e.g. ``static/scss/base.scss``). ::

$ compass watch


Setup Instructions
------------------

.. note::

    If you want to use Vagrant then use the :ref:`Vagrant Instructions <using-vagrant>`. Otherwise, continue with these instructions.

Before you begin make sure you've setup and installed `Virtualenvwrapper <http://www.doughellmann.com/projects/virtualenvwrapper/>`_.

Create a directory for your new Django site. ::

$ cd ~/Sites

In the same directory run the following command to setup a virtualenv for your new site. ::

$ mkvirtualenv --no-site-packages --distribute example
$ pip install django

Create your Django Base Site. The following will create a new project called "example". ::

$ django-admin.py startproject example --template=https://github.com/epicserve/django-base-site/archive/master.zip

Install the base requirements and development requirements. ::

$ cd example
$ pip install -r config/requirements/dev.txt

Add the project root to your Python path. ::

$ add2virtualenv .

Set your ``DJANGO_SETTINGS_MODULE`` environment variable (You'll need to do this everytime you work on this project). ::

$ export DJANGO_SETTINGS_MODULE=config.settings.dev

Setup your python virtual environment to load environment variables and switch you to the project root. ::

$ echo `pwd` > $VIRTUAL_ENV/.project
$ echo 'export DJANGO_SETTINGS_MODULE=config.settings.dev' >> $VIRTUAL_ENV/bin/postactivate
$ echo 'cdproject' >> $VIRTUAL_ENV/bin/postactivate

Remove all unnecessary example config and template files and create a `config/settings/local.py` settings file::

$ python utils/create_local_settings_file.py
$ make clean

Setup your database::

$ django-admin.py migrate

At this point your base site should be setup and you can now run your dev server. ::

$ django-admin.py runserver
