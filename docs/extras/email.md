# Email Functionality in Django-Allauth

Django-Allauth is a robust library that provides authentication, registration, and account management for Django projects. One of the essential features of this library is its support for sending transactional emails, such as verification emails, password reset emails, and more. Here’s a brief overview of how email functionality works in a Django-Allauth project and how you can customize email templates.

### Default Email Templates

By default, Django-Allauth includes plain text (.txt) message templates for various email types. These templates are used to send transactional emails without requiring any additional setup. The templates are originally found in the Django-Allauth library but are moved into the project folder to be customized.  They can be found in the following directory:

```bash
project/templates/account/email
```

### Customizing Email Templates  

If you wish to customize the email templates to better fit your project's needs, you can move the default templates from the Django-Allauth package into your project's templates directory and modify them as necessary.

### HTML Email Templates

Django-Allauth only comes out-of-the-box with text (.txt) message templates. If you want to send emails using HTML, you need to create the HTML templates yourself. For each email type, you should have two versions of the template:

A plain text version (e.g., email_confirmation.txt)
An HTML version (e.g., email_confirmation.html)
When both plain text and HTML templates are provided, Django-Allauth will send multipart emails containing both text and HTML versions. This ensures that recipients who prefer plain text emails or whose email clients do not support HTML will still receive the content of the email.

### Base Templates and Extending

Django-Allauth supports the use of base templates to streamline the process of creating consistent email designs. You can define a base message template for both text and HTML formats:

base_message.txt
base_message.html

Other email templates can then extend these base templates, allowing you to maintain a consistent look and feel across all your emails while only needing to update the base templates when making global changes.

### Example Directory Structure

Here’s an example directory structure for your email templates:

```markdown
project/
└── templates/
    └── account/
        └── email/
            ├── base_message.txt
            ├── base_message.html
            ├── email_confirmation_message.txt
            ├── email_confirmation_message.html
            ├── password_reset_key_message.txt
            ├── password_reset_key_message.html
            └── ...
```

### Sending Test Emails

You can use a custom management commands to send test emails for each type to verify that your templates are working correctly. Here is an example of how to use the provided Makefile commands to send test emails:

```sh
make test_email type=email_confirmation
make test_email type=password_reset
```

By setting up your templates in this manner, you can ensure that all your transactional emails have a professional and consistent appearance, improving the overall user experience.
