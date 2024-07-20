# SMTP Info

### SMTP2Go

Using SMTP2GO (www.smtp2go.com) as an email delivery service. Use for SMTP Relay 
Service & Email Tracking.

```py title='.env'
# Email Configuration
EMAIL_HOST=mail.smtp2go.com
EMAIL_PORT=2525
EMAIL_HOST_USER=cyclingbeats.com
EMAIL_HOST_PASSWORD=*****************
EMAIL_USE_TLS=True
```

### Testing from python shell  
- Open python shell within django environment
```bash
cd /home/rocket/beats
source _env/bin/activate
python manage.py shell
```
- execute commands from shell
```shell
# import send_mail
from django.core.mail import send_mail

# import settings
from django.conf import settings

# send test email
send_mail("test_email", "This is a test email", "admin@cyclingbeats.com", ["timpandrews@yahoo.com"], fail_silently=False,)

# review settings
print("EMAIL_BACKEND:", settings.EMAIL_BACKEND)
print("EMAIL_HOST:", settings.EMAIL_HOST)
print("EMAIL_PORT:", settings.EMAIL_PORT)
print("EMAIL_USE_TLS:", settings.EMAIL_USE_TLS)
print("EMAIL_HOST_USER:", settings.EMAIL_HOST_USER)
print("EMAIL_HOST_PASSWORD:", settings.EMAIL_HOST_PASSWORD)
print("DEFAULT_FROM_EMAIL:", settings.DEFAULT_FROM_EMAIL)

# update settings
settings.EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
settings.EMAIL_HOST = 'smtp.example.com'  # Replace with your SMTP host
settings.EMAIL_PORT = 587
settings.EMAIL_USE_TLS = True
settings.EMAIL_HOST_USER = 'your_email@example.com'
settings.EMAIL_HOST_PASSWORD = 'your_password'
settings.DEFAULT_FROM_EMAIL = 'your_email@example.com'
```
