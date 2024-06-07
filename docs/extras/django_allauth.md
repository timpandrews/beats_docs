# Django-Allauth

## Template Info

*django-allauth* provides a range of templates used for handling account management and authentication tasks. Here’s a list of the primary templates that you might want to customize in your Django project:

### Account Management
- **login.html**: Used for the login page.
- **signup.html**: Used for user registration.
- **logout.html**: Displays a logout confirmation.
- **password_change.html**: For changing an existing password.
- **password_change_done.html**: Confirmation that the password has been changed.
- **password_reset.html**: For initiating a password reset.
- **password_reset_done.html**: Confirms that a password reset email has been sent.
- **password_reset_from_key.html**: Allows entering a new password using a reset key received by email.
- **password_reset_from_key_done.html**: Confirmation that the password has been reset successfully.

### Email Management
- **email.html**: Page to manage email addresses (add, remove, set primary).
- **email_confirm.html**: Confirmation page for when a user adds a new email address.
- **email_confirmation_done.html**: Page shown after a user has confirmed their email address.
- **email_confirmation_subject.txt**: Subject line template for the email confirmation email.
- **email_confirmation_message.txt**: Email body template for the email confirmation email.
- **email_confirmation_signup_subject.txt**: Subject template for the email confirmation on signup.
- **email_confirmation_signup_message.txt**: Email body template for the confirmation on signup.

### Social Account Management (If using allauth.socialaccount)
- **connections.html**: Manages connections to social accounts.
- **login_cancelled.html**: Shown if social login is cancelled.
- **login_error.html**: Displays errors during the social login process.
- **signup.html**: Additional signup form used when signing up via a social account, if additional information is required.

### Template Location
These templates are located inside the *djgano-allauth* package found at **.venv/lib/python3.12/site-packages/allauth**.  Templates are located within the **templates/account/** and **templates/socialaccount/** directories. To override these templates, you should replicate the same directory structure within your project's templates directory. For example, to override the signup template for account management, you would place your custom signup.html in **your_project/templates/account/signup.html**.

By customizing these templates, you can provide a user experience that fits seamlessly with the rest of your site’s design and meets your project's specific needs.
