# Robots.txt

## Overview

#### What is *robots.txt*?

*robots.txt* is a standard used by websites to communicate with web crawlers and other web robots. It specifies which parts of the website should not be accessed or scanned by these automated agents. This file is placed at the root of the website and is publicly accessible.  

#### Purpose of *robots.txt*

- Control Web Crawlers: Direct web crawlers on which pages they can or cannot access.
- Prevent Overloading: Prevent web crawlers from overloading the server by limiting their access.
- Protect Sensitive Information: Restrict access to parts of the website that contain sensitive information or are not meant for public viewing.

## Using django-robots in This Project

*django-robots* is a Django library that provides a simple way to manage your robots.txt file. It allows you to define rules and URLs directly from the Django admin interface, making it easy to update and maintain.

#### Creating Rules and URLs

1. Access the Django Admin:
    Navigate to the Django admin interface (e.g., http://127.0.0.1:8000/admin/).
2. Add a Rule:
    - Go to the Robots section.
    - Click on Add Rule.
    - Fill in the details:
        - User-agent: Specify the user-agent (e.g., Googlebot or * for all user agents).
        - Advanced options:
            - Crawl-delay: Optionally, specify a crawl delay.
3. Add URLs to the Rule:
    - After creating a rule, you can add URLs to it.
    - Click on Add URL under the rule.
    - Specify the URL pattern (e.g., /private/).

#### Example

Here is an example of a *robots.txt* file managed by django-robots:

``` txt title="robots.txt"
User-agent: *
Disallow: /admin/
Disallow: /private/
```

#### Verifying *robots.txt*

To verify that your robots.txt file is correctly configured and accessible:

1. Run the Development Server:

    ``` bash
    make run
    -- or --
    python manage.py runserver
    ```

2. Access robots.txt:
    Open your web browser and navigate to:

    ``` url
    http://127.0.0.1:8000/robots.txt
    ```

3. Check the Response:
    Ensure that the response contains the rules you defined.

#### Unit Testing *robots.txt*

To ensure that your robots.txt file is correctly configured you can run the unit test: *project.apps.common.test_robots.py*

``` bash
make test-common
```

#### Best Practices

- Do Not Expose Sensitive URLs: Avoid listing sensitive URLs in robots.txt as it is publicly accessible.
- Use Strong Authentication: Ensure strong authentication mechanisms for sensitive parts of your site.
- Monitor Access: Regularly monitor access logs for any suspicious activity.

By following these guidelines and using django-robots, you can effectively manage your robots.txt file and control how web crawlers interact with your site.
