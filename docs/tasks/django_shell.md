# Using Django Shell to Build DB Queries
Steps for working with the Django Shell, a command-line interface provided by Django to interact with your Django project.  This can be useful for interactively testing and exploring your Django models and queries within the Django Shell. 

- Open Django Shell
```bash
poetry run python manage.py shell
```
- import your model
```dj
from project.apps.activity.models import Modelname
```
- make and instance of the model that you want to test
```dj
instance = Activity.objects.get(id=222)
```
- view items in that instance 
```dj
for field, value in instance.__dict__.items():
    print(f"{field}: {value}")
```
<small>\* be sure to indent lines 2+ and double return to execute loop</small>

- build & test your query for inclusion in kudos.yaml config
```dj
if instance.core_data["distance"] >= 100:
    achieved = True
else:
    achieved = False
print(achieved)
```
<small>
\* indent as you normaly would.  
\* One return to execute one line command or next line of multi-line command  
\* Two returns to execute multi-line command
</small>