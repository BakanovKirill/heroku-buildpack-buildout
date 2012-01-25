Heroku buildpack: Buildout
==========================

This is a completely unofficial [Heroku buildpack](http://devcenter.heroku.com/articles/buildpack) for Python apps that need Buildout, for some reason.
It uses [virtualenv](http://www.virtualenv.org/) and [pip](http://www.pip-installer.org/).

Usage
-----

Example usage:

    $ ls
    Procfile  bootstrap.py  buildout.cfg

    $ heroku create --stack cedar --buildpack git@github.com:kennethrietz/heroku-buildpack-buildout.git

    $ git push heroku master
    something.

The buildpack will detect your app as Buildout if it has the file `buildout.cfg` in the root. It will detect your app as Python/Django if there is an additional `settings.py` in a project subdirectory.

It will use virtualenv and pip to install your dependencies, vendoring a copy of the Python runtime into your slug.  The `bin/`, `include/` and `lib/` directories will be cached between builds to allow for faster pip install time.

Hacking
-------

To use this buildpack, fork it on Github.  Push up changes to your fork, then create a test app with `--buildpack <your-github-url>` and push to it.

To change the vendored virtualenv, unpack the desired version to the `src/` folder, and update the virtualenv() function in `bin/compile` to prepend the virtualenv module directory to the path. The virtualenv release vendors its own versions of pip and setuptools.
