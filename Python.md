## Setup dev environment

`easy_install virtualenv`

Navigate to project directory and run -

`virtualenv env`

Activate new environment - 

`. env/bin/activate`

Then use `pip install django` or whatever you want to install to that environment only.

## Install Cheetah

Application framework, used by SABnzbd and SickBeard.

Assumes `easy_install virtualenv` has been run.

`pip install cheetah`

Run in a virtualenv or system wide, which may be best for multiple projects on the same system.

## Simple HTTP server from any directory

`python -m SimpleHTTPServer [port]`
