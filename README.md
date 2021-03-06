# PyPI package cookiecutter template

Matt's personal [cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) template for creating new PyPI packages.

## Create the package

    $ pip install cookiecutter
    $ cookiecutter https://github.com/mmedal/cookiecutter-pypackage
    author [Matthew Medal]:
    email [matt.medal@gmail.com]:
    github_username [mmedal]:
    module_name [example_package]: my_example_project
    package_name [example-package]: my-example-project
    project_title [Example package]:
    project_description [An example package.]:
    version [0.0.1]:
    year [2016]:

## Change directory into the package

    cd {{package_name}}

## Create the GitHub repo

* Make sure it's under `{{github_username}}/{{package_name}}`

## Enable in Travis

* Navigate to `https://travis-ci.org/profile/{{github_username}}`
* "Sync account"
* Turn on

## Push the package to GitHub

    git init
    git add .
    git commit -m "Initial commit"
    git remote add origin git@github.com:{{ github_username }}/{{package_name}}.git
    git push -u origin master

## Install requirements

    pyvenv-3.5 env
    source env/bin/activate
    pip install --upgrade pip
    pip install -r requirements-unfrozen.txt

## Create an initial pull request

    git checkout -b freeze-requirements
    pip freeze > requirements.txt
    git add requirements.txt
    git commit -m "Freeze requirements"
    git push --set-upstream origin freeze-requirements

Ensure the travis tests run and merge the pull request on GitHub.

## Publish the package on PyPI

    git checkout master
    git pull
    ./setup.py register
    ./setup.py publish
    git tag -a 0.0.1 -m 'version 0.0.1'
    git push --tags
