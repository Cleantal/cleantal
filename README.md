# CLEANTAL README

Welcome to Cleantal repository, please follow this steps for running locally the project.

If you have issues with this please send an email to: 
 - font3face@gmail.com
 - bryanandreslopezarango@gmail.com

# Cleantal Backend
Cleantal backend is a project developed using Ruby on Rails and contains the code for Cleantal.
## Getting Started
To run this porject on your local machine you have two options:
1. [Install ruby, postgres and redis on your machine](#1-install-ruby-postgres-and-redis-on-your-machine).
2. [Install docker and run all services as containers](#2-install-docker-and-run-all-services-as-containers).

### 1. Install ruby, postgres and redis on your machine.
Some of the following steps will include instructions for Mac and Linux machines:

- #### Install system dependencies
    The following dependencies are need to build the project:

    * ##### Linux:
    ```
    sudo apt-get update
    sudo apt-get install cmake
    sudo apt-get install pkg-config
    ```
    Installing node js can be done in several ways, for example the most common is using apt-get:
    ```
    sudo apt-get install nodejs
    ```

    However using this command you wont be able to select a specific version for project, we encourage the use of a node version manager, for instance, volta:
    ```
    curl https://get.volta.sh | bash
    ```

    * ##### MAC:
    ```
    brew install cmake
    ```
    Installing node js can be done in several ways, we encourage the use of a node version manager, for instance, volta:
    ```
    curl https://get.volta.sh | bash
    ```

- #### Install ruby dependencies:
    Clone the rbenv repository (another good option is rvm) from GitHub into the directory ~/.rbenv
    ```
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    ```

    Next, add ~/.rbenv/bin to your $PATH so that you can use the rbenv command line utility. Do this by altering your ~/.bashrc file so that it affects future login sessions:
    ```
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    source ~/.bashrc
    ```

    Verify that rbenv is set up properly by using the type command, which will display more information about the rbenv command:
    ```
    type rbenv
    ```
    Next, install the ruby-build, plugin. This plugin adds therbenv install command, which simplifies the installation process for new versions of Ruby:
    ```
    git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
    ```
    With the ruby-build plugin now installed, you can install versions of Ruby y may need through a simple command. First, let's list all the available versions of Ruby:
    ```
    rbenv install 2.7.2
    ```
    Turn off gem documentation
    ```
    echo "gem: --no-document" > ~/.gemrc
    ```

- #### Install app dependencies:
    Make sure you have the correct version of ruby installed before running bundle install or it will generate errors.

    ```
    bundle install
    ```

- #### Install assets dependencies:
    ```
    npm i -g yarn
    yarn install
    ```
- #### Setup pre-commit gem
    ```
    pre-commit install
    ```

- #### Install Database
    Before continue creating the data base, you might get an error creating it due to postgres, to avoid that we are going to install the postgreSQL database and configure a user to manage it.

    * ##### Linux:
    The first thing you must do is configure the repositories lists

    ```
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list -
    sudo apt update -
    ```

    Once the list of postgreSQL packages is updated we will use the following command to install it

    ```
    sudo apt -y install postgresql-12 postgresql-client-12
    ```

    Once postgreSQL is installed, we will enter the session and create from there a new user with the ability to create databases

    ```
    sudo -i -u postgres
    createuser --pwprompt --interactive (enter here the user name with out  () )
    Enter password for new role: ****** (your password)
    Enter it again: ******
    Shall the new role be a superuser? (y/n) y
    ```

    To exit the postgreSQl session we must use the exit command

    After get installed postgres, you got to open Cleantal's repository, go to config/database.yml and set the username & password that you created before for postgres. In the test line too.

    * ##### MAC:
    Install postgres:
    ```
    brew install postgresql
    ```

    Start the Postgres service:
    ```
    brew services start postgresql
    ```

    Run `initdb /usr/local/var/postgres` to check the username, and update `config/database.yml` with the new username in `default`.
