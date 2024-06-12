# Django Error Logs - In Production Settings

Logging django error messages is configured in environment specific settings file.

```py title="env_production.py"
# UPDATE THE LOGGING CONFIGURATION FOR PRODUCTION
# Extend the existing LOGGING configuration
LOGGING["handlers"]["file"] = {
    "level": "WARNING",
    "class": "logging.FileHandler",
    "filename": os.path.join(BASE_DIR, "logs", "django_errors.log"),
    "formatter": "standard",
}
```

Logs can be found at */home/rocket/beats/project/logs/django_errors.log*
```bash
sudo tail -f /home/rocket/beats/project/logs/django_errors.log
```