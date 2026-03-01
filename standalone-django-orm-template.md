# Standalone Django ORM(Object-Relational Mapper)

This document provides a guide to setting up a standalone Django ORM environment, allowing you to use Django's powerful database management features without the need for a full Django project.

Recomended project structure:
```
myproject/
|-- orm_setup/
|-- models.py
|-- main.py
|-- mydatabase.sqlite3
```

# step 1: Installation
To get started, you need to install Django. You can do this using pip:

```bash
pip install Django
```
# step 2: Create a Django Project
Next, you need to create a Django project. This will serve as the foundation for your standalone ORM setup. 
Run the following command:

```bash
django-admin startproject myproject
```
# step 3: Configure the Database

```python
import os
import django
from django.conf import settings
from pathlib import Path

# Build paths relative to this file
BASE_DIR = Path(__file__).resolve().parent

def setup():
    if not settings.configured:
        settings.configure(
            DEBUG=True,
            # Use an in-memory DB for speed, or a local file for persistence
            DATABASES={
                "default": {
                    "ENGINE": "django.db.backends.sqlite3",
                    "NAME": BASE_DIR / "db.sqlite3",
                }
            },
            INSTALLED_APPS=[
                "django.contrib.contenttypes", # Often required by other apps
                "django.contrib.auth",
                "models_app",
            ],
            # Essential for modern Django versions
            DEFAULT_AUTO_FIELD="django.db.models.BigAutoField",
        )
        django.setup()

if __name__ == "__main__":
    setup()
    # Your logic here...
```
# step 4: Define Your Models
Create a file named `models.py` and define your Django models as you would in a regular Django application. For example:

```python
import os
import django
from django.conf import settings
from pathlib import Path

# Build paths relative to this file
BASE_DIR = Path(__file__).resolve().parent

def setup():
    if not settings.configured:
        settings.configure(
            DEBUG=True,
            # Use an in-memory DB for speed, or a local file for persistence
            DATABASES={
                "default": {
                    "ENGINE": "django.db.backends.sqlite3",
                    "NAME": BASE_DIR / "db.sqlite3",
                }
            },
            INSTALLED_APPS=[
                "django.contrib.contenttypes", # Often required by other apps
                "django.contrib.auth",
                "models_app",
            ],
            # Essential for modern Django versions
            DEFAULT_AUTO_FIELD="django.db.models.BigAutoField",
        )
        django.setup()

if __name__ == "__main__":
    setup()
    # Your logic here...
```
# step 5: Run Migrations
After defining your models, you need to run migrations to create the corresponding database tables. You can do this by running the following commands in your terminal:

```bash
python manage.py makemigrations
python manage.py migrate
```
# step 6: Use the ORM
Now you can use the Django ORM to interact with your database. You can create, read, update, and delete records using the models you defined. For example:

```python
from orm_setup import setup
from django.core.management import call_command

# 1. Initialize Django
setup()

# 2. Sync the Database 
# 'migrate' automatically creates tables for all models in INSTALLED_APPS
# It's much safer than manual schema_editor calls.
call_command("migrate", verbosity=0, interactive=False)

from models_app.models import Student

# 3. Insert data (using get_or_create to prevent duplicates on re-runs)
student, created = Student.objects.get_or_create(
    name="Vedant", 
    defaults={"age": 20}
)

if created:
    print(f"Created new student: {student.name}")
else:
    print(f"Student {student.name} already exists.")

# 4. Query data efficiently
# .values_list or .values is faster if you only need specific fields
for s in Student.objects.all():
    print(f"Name: {s.name} | Age: {s.age}")
```
# final step: Run Your Script
You can run your script using the following command:

```bash
python main.py
```
**Now you have a standalone Django ORM setup that allows you to manage your database using Django's powerful features without the overhead of a full Django project!, and are good to go!**
