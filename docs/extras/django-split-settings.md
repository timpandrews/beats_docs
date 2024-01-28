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
            dev_development.py
            local_settings.py
            logging.py
            smtp.py
```

``` py title="__init__.py (as of 1/25/2024)"
"""
Django Settings Configuration using django-split-settings.

For more information on django-split-settings, visit:
https://github.com/sobolevn/django-split-settings

This file serves as the main entry point for Django settings,
organizing configurations into modular files for better maintainability.

Default environment is set to 'development'.

Usage
-----
- Standard Django settings are configured in 'common.py'.
- PostgreSQL settings are configured in 'database.py'.
- SMTP settings are configured in 'smtp.py'.
- Logging settings are configured in 'logging.py'.
- Environment-specific settings can be defined in 'env_{DJANGO_ENV}.py'.
- Local overrides (not in version control) can be placed in 'local_settings.py'.

To customize settings for specific environments or scenarios, modify the
respective configuration files mentioned above.
"""

import os
from pathlib import Path

import environ
from split_settings.tools import include, optional

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent.parent

# Initialize environment variables
env = environ.Env()

# Read environment variables from the .env file in the 'core' directory
environ.Env.read_env(os.path.join(BASE_DIR, "core/.env"))

# Retrieve the current environment or default to 'development'
DJANGO_ENV = env("DJANGO_ENV") or "development"

# Define the list of base settings files to include
base_settings = [
    "common.py",  # standard django settings
    "database.py",  # postgres
    "smtp.py",  # smtp
    "logging.py",  # logging
    optional(f"env_{DJANGO_ENV}.py"),  # environment-specific settings
    optional("local_settings.py"),  # local overrides (not in version control)
]

# Include settings by passing the list of base settings files
include(*base_settings)

```


