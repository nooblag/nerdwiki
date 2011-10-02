## Start a new development environment

`virtualenv --no-site-packages django-blog`

`. django-blog/bin/activate`

## Install Django in new environment

`pip install -E django-blog django`

## Start a new project

`django-admin.py startproject blog`

## Start local server. This starts with a default port of 8000

`python manage.py runserver`

## Start with different port

`python manage.py runserver 0.0.0.0:8081`

## Edit settings.py and uncomment lines to enable admin mode, and edit sql settings

`nano settings.py`

## Setup database

`python manage.py syncdb`

## Edit urls.py and uncomment lines to enable admin mode

`nano urls.py`
