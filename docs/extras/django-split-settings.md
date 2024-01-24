# ![django-split-settings](../assets/icons/django-split-settings-icon.png){: width="4%"} django-split-settings

<a href="https://skillshats.com/blogs/efficient-django-project-settings-with-split-settings-library/" target="_blank">SkillsHats:
Efficient Django Project Settings with Split Settings Library</a>

- Settings becomes it's own module within the Core App
- Settings are configured in the \_\_init\_\_.py file of the Settings module
- Settings are broken into multiple setting_name.py files.
- Settings files can be created based on setting type (ie common, db, email, logging, etc) or environment (ie dev, staging, prod) or optional (ie local_settings)


``` title="Directory Structure (as of 1/25/2024)"
project  
    core  
        settings
            __init__.py
            common.py
            database.py
            local_settings.py
            logging.py
```

``` py title="__init__.py (as of 1/25/2024)"
"""
This is a django-split-settings main file.
For more information read this:
https://github.com/sobolevn/django-split-settings
Default environment is `developement`.
"""

import os
from pathlib import Path

import environ
from split_settings.tools import include, optional

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent.parent

env = environ.Env()
environ.Env.read_env(os.path.join(BASE_DIR, "core/.env"))

DJANGO_ENV = env("DJANGO_ENV") or "development"

base_settings = [
    "common.py",  # standard django settings
    "database.py",  # postgres
    "smtp.py",  # smtp
    "logging.py",  # logging
    # TODO: Setup settings files for Dev and Prod
    optional(f"env_{DJANGO_ENV}.py"),
    # Optionally override some settings:
    optional("local_settings.py"),
]

# Include settings:
include(*base_settings)
```


