# Cron Starter Kit

## About this template

This is a simple starter kit for deploying and maintaining cron jobs on EC2 servers.

The kit gives you:

- Simple deployment commands for getting the project on a server and installing the crontab to `etc/cron.d`.
- A default logging setup -- logging is good!
- A workflow for isolating project secrets from the repository both locally and on the server through environment variables (see `app_config.py` and `run_on_server.sh`).
- A way to keep cron job projects in version control!
- Convenience variables for deployment to Amazon S3, something we do often from a cron job.

This codebase is licensed under the MIT open source license. See the LICENSE file for the complete license.

## Assumptions

The following things are assumed to be true in this documentation.

* You are running OSX.
* You are using Python 2.7. (Probably the version that came with OSX.)
* You have [virtualenv](https://pypi.python.org/pypi/virtualenv) and [virtualenvwrapper](https://pypi.python.org/pypi/virtualenvwrapper) installed and working.

For more details on our stack, see our [development environment blog post](http://blog.apps.npr.org/2013/06/06/how-to-setup-a-developers-environment.html).

## Copy the template

Create a new repository on Github. Everywhere you see ``$NEW_PROJECT_NAME`` in the following script, replace it with the name of the repository you just created.

```
git clone git@github.com:nprapps/cron-starter-kit.git $NEW_PROJECT_NAME
cd $NEW_PROJECT_NAME

mkvirtualenv $NEW_PROJECT_NAME
pip install -r requirements.txt

fab bootstrap
```

This will setup the new repo and will replace `README.md` (this file) with `PROJECT_README.md`. See that file for usage documentation.

By default `bootstrap` will use `nprapps` as the Github username, and the current directory name as the repository name. **This is a best practice**, but you can override these defaults if you need to:

```
fab bootstrap:$GITHUB_USERNAME,$REPOSITORY_NAME
```

## Configuring for yourself

This project contains a number of default variables for NPR's setup. These all live in `app_config.py`. To adapt this for your organization, change the following variables to the appropriate values:

* `GITHUB_USERNAME` -- Github username so that this project pushes and pulls from the correct repo
* `PRODUCTION_S3_BUCKET` -- From production, the S3 bucket the cron job would deploy to
* `STAGING_S3_BUCKET` -- From staging, the S3 bucket the cron job would deploy to
* `PRODUCTION_SERVERS` -- A list of servers to deploy to when deploying to production
* `STAGING_SERVERS` -- A list of servers to deploy to when deploying to staging
* `SERVER_USER` -- The user that the project should use as the SSH user
* `SERVER_PYTHON` -- The version of Python on the server
* `SERVER_PROJECT_PATH` -- Where the setup script should install the project
* `SERVER_REPOSITORY_PATH` -- Where the setup script should install the repository on the server
* `SERVER_VIRTUALENV_PATH` -- Where the setup script should install the virtualenv on the server
