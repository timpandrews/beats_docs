# Project Dependencies

## Listing from pyproject.toml

```yaml title="pyproject.toml (partial, 2/2/2024)"
[tool.poetry.dependencies]
python = "^3.12"
django = "^5.0"
django-admin-env-notice = "^1.0"
django-allauth = "^0.59.0"
django-bootstrap-datepicker-plus = "^5.0.5"
django-bootstrap-input-group = "^1.0.1"
django-bootstrap5 = "^23.3"
django-environ = "^0.11.2"
django-htmx = "^1.17.2"
django-import-export = "^3.3.6"
django-split-settings = "^1.2.0"
django-timezone-field = "^6.1.0" # TODO: not using timezone field anymore. Remove?
django-waffle = "^4.1.0"
fitdecode = "^0.10.0"
pendulum = "^3.0.0"
pillow = "^10.1.0"
psycopg2-binary = "^2.9.9"
pytz = "^2023.3.post1"
pyyaml = "^6.0.1"


[tool.poetry.group.dev.dependencies]
black = "^23.12.0"
colorlog = "^6.8.0"
coverage = "^7.3.3"
flake8 = "^6.1.0"
isort = "^5.13.1"
pre-commit = "^3.6.0"
ruff = "^0.1.7"  
```

## Dependencies
- python
- django

- **django-admin-env-notice**  
<small>Used to display environment-specific notices in the Django admin interface. It's useful for distinguishing between different deployments of your Django application, such as development, staging, and production.</small>  
<a href="https://pypi.org/project/django-admin-env-notice/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/dizballanze/django-admin-env-notice" target="_blank">:fontawesome-brands-github: GitHub</a> 

- **django-allauth**   
<small>a Django package for comprehensive authentication, supporting social and local login with advanced features like signup, email verification, and password management.</small>  
<a href="https://allauth.org/" target="_blank">allauth.org</a> | 
<a href="https://docs.allauth.org/en/latest/" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
<a href="https://pypi.org/project/django-environ/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/pennersr/django-allauth" target="_blank">:fontawesome-brands-github: GitHub</a>

- **django-bootstrap-datepicker-plus**  
<small>This django widget contains Date-Picker, Time-Picker, DateTime-Picker, Month-Picker and Year-Picker input with date-range-picker functionality.</small>  
<a href="https://django-bootstrap-datepicker-plus.readthedocs.io/en/latest/" target="_blank">:octicons-book-24: ReadTheDocs</a> |
<a href="https://pypi.org/project/django-bootstrap-datepicker-plus/" target="_blank">:fontawesome-brands-python: PyPi</a>

- **django-bootstrap-input-group**  
<small>This is an add-on for django-bootstrap5 for rendering multiple django form fields as a Bootstrap input group.</small>  
<a href="https://pypi.org/project/django-bootstrap-input-group/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/Actionb/django-bootstrap-input-group" target="_blank">:fontawesome-brands-github: GitHub</a> | 
[:mag:  Internal Docs](extras/forms-w-django-bootstrap-input-group.md)   

- **django-bootstrap5** <small>\*</small>  
<small>The django-bootstrap5 library seamlessly integrates Bootstrap 5 into Django, offering template tags and widgets for quick, responsive UI design without extensive CSS, enhancing web development efficiency. </small>  
<a href="https://github.com/zostera/django-bootstrap5" target="_blank">:fontawesome-brands-github: GitHub</a> | 
<a href="https://django-bootstrap5.readthedocs.io/en/stable/" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
[:mag:  Internal Docs](extras/forms-w-django-bootstrap5.md)   
<small>\* *There are two similar libraries available: django-bootstrap5 and django-bootstrap-v5.  The two are almost identical and perform the same function, but the django-bootstrap5 project is preferred because it is the one that is currently being maintained.*</small>

- **django-environ**  
<small>a Django utility that simplifies the process of handling environment variables in Django projects.</small>  
<a href="https://django-environ.readthedocs.io/en/latest/" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
<a href="https://pypi.org/project/django-environ/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/joke2k/django-environ" target="_blank">:fontawesome-brands-github: GitHub</a> | 
<a href="extras/django-environ.md" style="color: lightgray; pointer-events: none; text-decoration: none;">:mag: TODO: Internal Docs</a>

- **django-htmx**  
<small>HTMX is a JavaScript library that enhances web applications by enabling dynamic, real-time interactions using HTML attributes. It allows you to update parts of a web page without a full page reload. "django-htmx" is a Django library that simplifies using HTMX with Django projects, streamlining the integration of real-time features by leveraging HTML attributes and Django views, reducing the need for extensive JavaScript development.</small>  
<a href="https://django-htmx.readthedocs.io/en/latest/index.html" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
<a href="https://pypi.org/project/django-htmx/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/adamchainz/django-htmx" target="_blank">:fontawesome-brands-github: GitHub</a> |
<a href="https://htmx.org/" target="_blank">![htmx](assets/icons/htmx_icon.png){: width="2%"} htmx.org
</a>

- **django-import-export** 
<small>Adds tools to the Django-Admin site that allows importing and exporting data between Django models and various formats such as Excel, CSV, JSON, and YAML. It simplifies the process of transferring data to and from Django applications.</small>  
<a href="https://django-import-export.readthedocs.io/en/stable/" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
<a href="https://github.com/django-import-export/django-import-export/" target="_blank">:fontawesome-brands-github: GitHub</a> 

- **django-split-settings** ![django-split-settings](assets/icons/django-split-settings-icon.png){: width="2%"}  
<small>Organize Django settings into multiple files and directories. Easily override and modify settings. Use wildcards in settings file paths and mark settings files as optional.</small>  
<a href="https://django-split-settings.readthedocs.io/en/latest/index.html" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
<a href="https://pypi.org/project/django-split-settings/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/wemake-services/django-split-settings" target="_blank">:fontawesome-brands-github: GitHub</a> | 
[:mag: Internal Docs](extras/django-split-settings.md)

- django-timezone-field <small>*not using timezone fields anymore. Remove?*</small>

- **django-waffle** 
<small>Django Waffle is feature flipper for Django. You can define the conditions for which a flag, switches, or sample should be active, and use them in a number of ways.</small>  
<a href="https://waffle.readthedocs.io/en/stable/" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
<a href="https://pypi.org/project/django-waffle/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/django-waffle/django-waffle" target="_blank">:fontawesome-brands-github: GitHub</a> |
<a href="extras/django_waffles.md" style="color: lightgray; pointer-events: none; text-decoration: none;">:mag: TODO: Internal Docs</a>

- **fitdecode**  
<small>A FIT file parsing and decoding library written in Python3</small>  
<a href="https://fitdecode.readthedocs.io/en/latest/" target="_blank">:octicons-book-24: ReadTheDocs</a> |
<a href="https://github.com/polyvertex/fitdecode" target="_blank">:fontawesome-brands-github: GitHub</a>

- **Pendulum**  
<small>Pendulum is a Python package for easier datetime manipulation, offering a more intuitive API, timezone handling, and improved formatting and parsing.</small>  
<a href="https://pendulum.eustace.io/" target="_blank">pendulum.eustace.io</a> | 
<a href="https://pypi.org/project/pendulum/" target="_blank">:fontawesome-brands-python: PyPi</a>

- **pillow**  
<small>The Python Imaging Library adds image processing capabilities to your Python interpreter.  This library provides extensive file format support, an efficient internal representation, and fairly powerful image processing capabilities.</small>  
<a href="https://python-pillow.org/" target="_blank">![Pillow](assets/icons/pillow.png){: width="2%"}python-pillow.org</a> | 
<a href="https://pillow.readthedocs.io/en/stable/" target="_blank">:octicons-book-24: ReadTheDocs</a> | 
<a href="https://pypi.org/project/pillow/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/python-pillow/Pillow" target="_blank">:fontawesome-brands-github: GitHub</a>

- **psycop2-binary**  
<small>Psycopg is a PostgreSQL adapter for the Python programming language. It is a wrapper for the libpq, the official PostgreSQL client library.</small>  
<a href="https://www.psycopg.org/docs/index.html" target="_blank">![Psycop](assets/icons/psycopg.png){: width="2%"} psycopg.org</a> | 
<a href="https://pypi.org/project/django-waffle/" target="_blank">:fontawesome-brands-python: PyPi</a> | [:mag: Internal Docs](extras/psycopg2-binary_vs_psycopg2.md)

- **pytz**  
<small>Pytz brings the Olson tz database into Python and thus supports almost all time zones. This module serves the date-time conversion functionalities and helps user serving international client’s base. It enables time-zone calculations in our Python applications and also allows us to create timezone aware datetime instances.</small>  
<a href="https://pypi.org/project/pytz/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/stub42/pytz" target="_blank">:fontawesome-brands-github: GitHub</a>

- **pyyaml**  
<small>PyYAML features a complete YAML 1.1 parser, Unicode support, pickle support, capable extension API, and sensible error messages. PyYAML supports standard YAML tags and provides Python-specific tags that allow to represent an arbitrary Python object.</small>  
<a href="https://pyyaml.org/" target="_blank">pyyaml.org</a> | 
<a href="https://pyyaml.org/wiki/PyYAML" target="_blank">:octicons-book-24: Wiki</a> | 
<a href="https://pypi.org/project/PyYAML/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/yaml/pyyaml" target="_blank">:fontawesome-brands-github: GitHub</a>









## Dev Dependencies
- flake8
- pre-commit
- black
- isort
- ruff
- coverage
- colorlog 

## Prod Dependencies
- **gunicorn**  
<small>Gunicorn is a WSGI server for deploying Django projects, acting as an interface between Django applications and Nginx, handling HTTP requests efficiently.</small>  
<a href="https://gunicorn.org/" target="_blank">![htmx](assets/icons/gunicorn.png){: width="2%"} gunicorn.org</a> |
<a href="https://pypi.org/project/gunicorn/" target="_blank">:fontawesome-brands-python: PyPi</a> | 
<a href="https://github.com/benoitc/gunicorn" target="_blank">:fontawesome-brands-github: GitHub</a>

