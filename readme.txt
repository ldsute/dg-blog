Using pyenv to manage Python/Virtualenv
$ pyenv virtualenv 3.4.3 dg-blog
$ pyenv shell dg-blog

Installing libraries
$ pip install --upgrade pip setuptools
$ pip install -r requirements.txt

Getting started with Django
# Create the project
$ django-admin startproject mysite .

# Edit mysite/settings.py
# Set local time zone as needed
#   TIME_ZONE = 'US/Mountain' # From https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
# Add base directory for static files (bottom of settings)
#   STATIC_ROOT = os.path.join(BASE_DIR, 'static')

# Create the database
$ python manage.py migrate

# Test execution
$ python manage.py runserver

# Create admin superuser
$ python manage.py createsuperuser

# Create app
$ python manage.py startapp blog

# Add new app to settings.INSTALLED_APPS
#INSTALLED_APPS = (
#    'django.contrib.admin',
#    'django.contrib.auth',
#    'django.contrib.contenttypes',
#    'django.contrib.sessions',
#    'django.contrib.messages',
#    'django.contrib.staticfiles',
#    'blog'
#)

# Repeat: Create/update model in app
# 1. Add model to <app>/models.py
# 2. Create migration file:
    $ python manage.py makemigrations blog
# 3. Apply migration file:
    $ python manage.py migrate blog
# 4. If model to be managed by django-admin, update registered models
#   from .models import Post
#   admin.site.register(Post)

# Create git repository
$ git init
$ git config --global user.name "Justin Stewart"
$ git config --global user.email ldsute@gmail.com
$ echo "*.pyc
__pycache__
myvenv
db.sqlite3
.DS_Store" > .gitignore
$ git status
$ git add -A .
$ git commit -m "My blog, first commit"
# To commit regularly ...
$ git commit -a

# Sync with GitHub
# Create GitHub repository
$ git remote add origin
$ git push -u origin master
# To push regularly ...
$ git push

# Loading to PythonAnywhere
# Login and start Bash shell
$ git clone https://github.com/ldsute/dg-blog.git
$ cd dg-blog
$ virtualenv --python=python3.4 myvenv
$ source myvenv/bin/activate
$ pip install -r requirements.txt
$ python manage.py collectstatic
$ python manage.py migrate
$ python manage.py createsuperuser
# Back at the PythonAnywhere web admin site:
#   Create Webapp
#   Enter virtualenv path (/home/ldsute/dg-blog/myvenv)
#   Edit wsgi file (use contents of /var/www/ldsute_pythonanywhere_com_wsgi.py)
#   Click "Reload ldsute.pythonanywhere.com" button
# Browse to http://ldsute.pythonanywhere.com/
# Browse to http://ldsute.pythonanywhere.com/admin