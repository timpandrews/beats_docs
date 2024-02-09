# ![Logging](../assets/icons/log_file.png){: width="10%"} Logging 

## Basic Setup
```py title="import & create logger object" hl_lines="1 9"
import logging

from django.contrib.auth.models import User
from django.db.models.signals import post_save, pre_delete
...
...
from .models import Activity

logger = logging.getLogger(__name__)
...
```
## Logger Levels & Messages
```py
logger.debug("Harmless debug Message")
logger.info("Just an information")
logger.warning("Its a Warning")
logger.error("Did you try to divide by zero")
logger.critical("Internet is down")
```

## Example
```py title="forms.py"
if user:  # if user is available
    # setup profile
    ...
else:
    # Set default values if user is not provided and log a warning
    ...
    logger.warning("User is not provided for RideForm. Default values are set.")
```