# Create Django App in Subdirectory

### Step 1: Create the App
Use the startapp command without the project directory prefix:
```bash
poetry run python manage.py startapp newapp
```
This command creates a new Django app in your project root directory.

### Step 2: Move the App
Move the newly created app into your desired subdirectory (project/apps/).
```bash
mv showcase project/apps/
```

### Step 3: Update INSTALLED_APPS
In common.py of the settings module, you'll need to add the app using its new path. Since Python uses dots to navigate through modules, you should use the full Python path to your app:
```py title="common.py"
INSTALLED_APPS = [
    ...
    "project.apps.showcase",
    ...
]
```
### Step 4: Verify the App Structure
Ensure that your app directory structure looks like this:
```
project/
    apps/
        newapp/
            migrations/
            __init__.py
            admin.py
            apps.py
            models.py
            views.py
```
### Step 5: Adjust the App's Apps.py
In project/apps/newapp/apps.py, make sure the name attribute of the app's configuration class reflects the new path:
```py title="apps.py"
from django.apps import AppConfig

class NewappConfig(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "project.apps.newapp"
```
### Step 6: Add URLs to project if necessary
Add include to root url.py file at project.core.urls
```py title="urls.py"
path("", include("project.apps.newapp.urls")),
```
Create new urls.py in the new app.  Create urls.py in project.apps.newapp
```py title="urls.py"
from django.urls import path
from .views import ViewName

app_name = "appname"

urlpatterns = [
    path("path/", ViewName.as_view(), name="pathname"),
]
```

By following these steps, you create a Django app in a nested directory structure, which can help organize larger projects with multiple apps. Remember to use the new path (project.apps.showcase) when referring to the app in your Django project, such as in INSTALLED_APPS and when using management commands like makemigrations and migrate.