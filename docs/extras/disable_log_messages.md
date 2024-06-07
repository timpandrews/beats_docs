#Disable Logging Temporarily

If you want to disable logging temporarily within a specific test to prevent a warning from being printed to the console, you can use the logging.disable function within a context manager. This will only suppress logging for the duration of the test, allowing you to isolate the effect to the specific test case.

```py
# This test will generate an expected warning:
# "WARNING django.request Not Found: /nonexistent-page/"
# Disable logging to prevent warning from being printed to console
logging.disable(logging.WARNING)
```