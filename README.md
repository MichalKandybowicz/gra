# Game

Online RPG game

## Quick Start

Create a Database and Database User
By default, Postgres uses an authentication scheme called “peer authentication” for local connections. Basically, this means that if the user’s operating system username matches a valid Postgres username, that user can login with no further authentication.

During the Postgres installation, an operating system user named postgres was created to correspond to the postgres PostgreSQL administrative user. We need to change to this user to perform administrative tasks:
```
sudo su - postgres
```
You should now be in a shell session for the postgres user. Log into a Postgres session by typing:
```
psql
```
First, we will create a database for our Django project. Each project should have its own isolated database for security reasons. We will call our database myproject in this guide, but it’s always better to select something more descriptive:
```
CREATE DATABASE myproject;
```
Remember to end all commands at an SQL prompt with a semicolon.

Next, we will create a database user which we will use to connect to and interact with the database. Set the password to something strong and secure:
```
CREATE USER myprojectuser WITH PASSWORD 'password';
```
Afterwards, we’ll modify a few of the connection parameters for the user we just created. This will speed up database operations so that the correct values do not have to be queried and set each time a connection is established.

We are setting the default encoding to UTF-8, which Django expects. We are also setting the default transaction isolation scheme to “read committed”, which blocks reads from uncommitted transactions. Lastly, we are setting the timezone. By default, our Django projects will be set to use UTC:
```
ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE myprojectuser SET timezone TO 'UTC';
```
Now, all we need to do is give our database user access rights to the database we created:
```
GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;
```
Exit the SQL prompt to get back to the postgres user’s shell session:
```
\q
```
Exit out of the postgres user’s shell session to get back to your regular user’s shell session:


To get this project up and running locally on your computer:
1. Set up the [Python development environment](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/development_environment).
   We recommend using a Python virtual environment.
1. Assuming you have Python setup, run the following commands (if you're on Windows you may use `py` or `py -3` instead of `python` to start Python):
   ```
   pip3 install -r requirements.txt
   python3 manage.py makemigrations
   python3 manage.py migrate
   python3 manage.py collectstatic
   python3 manage.py test # Run the standard tests. These should all pass.
   python3 manage.py createsuperuser # Create a superuser
   python3 manage.py runserver
   ```
1. Open a browser to `http://127.0.0.1:8000/admin/` to open the admin site
1. Create a few test objects of each type.
1. Open tab to `http://127.0.0.1:8000` to see the main site, with your new objects.

```
Link with tutorial (google acc connect)
https://medium.com/trabe/oauth-authentication-in-django-with-social-auth-c67a002479c1
```