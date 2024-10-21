# Project Overview

## Project Structure

The project is organized into several directories and files, each serving a 
specific purpose. Here's a breakdown of the main components:

### Directory Structure & Key Files


- Root
    - [makefiles/](#makefiles)
    - [project/](#project)
        - [apps/](#apps)
            - [activity/](#activity)
            - [common/](#common)
            - [community/](#community)
            - [dashboard/](#dashboard)
            - [feed/](#feed)
            - [kudos/](#kudos)
            - [pages/](#pages)
            - [profiles/](#profiles)
            - [rides/](#rides)
            - [showcase/](#showcase)
        - [config/](#config)
        - [core/](#core)
            - settings/
            - static/
        - [logs/](#logs)
        - [media/](#media)
        - [static/](#static)
        - [templates/](#templates)
            - account/
            - community/
            - dashboard/
            - feed/
            - [includes/](#includes)
            - kudos/
            - pages/
            - rides/
            - shared/
            - showcase/
        - [tests/](#tests)
            - [_first/](#_first)
            - [apps/](#apps)
                - account/
                - activity/
                - common/
                - community/
                - dashboard/
                - feed/
                - kudos/
                - pages/
                - profile/
                - rides/
                - showcase/
            - [setup.py](#setup.py)
    - [.coveragerc](#coveragerc)
    - [.editorconfig](#editorconfig)
    - [.gitignore](#gitignore)
    - [.pre-commit-config.yaml](#pre-commit-config.yaml)
    - [.pre-commit-quick-config.yaml](#pre-commit-quick-config.yaml)
    - [makefile](#makefile)
    - [poetry.lock](#poetry.lock)
    - [pyproject.toml](#pyproject.toml)
    - [requirements.txt](#requirements.txt)


## Apps

### Activity

The **activity** app is responsible for managing and storing user activities. While the primary activity type handled is rides, the app is designed to be flexible and can be expanded to support additional activity types in the future.

Key components include:

- **Activity Model**: The core model that tracks general information about all user activities.
- **RideDetail Model**: A specialized model that stores extra details specifically for activities of the ride type, allowing for more detailed tracking of cycling events.
- **Admin Configuration**: This app includes admin configuration classes for both the Activity and RideDetail models, enabling efficient management of activities through the Django admin interface.
The app is focused on data modeling and admin management, without including any URLs or views.


### Common


### Community

The **community** app facilitates social interactions between users, focusing on follow relationships and invitations, while providing a frontend for users to discover and view each other's Showcase pages.

Key components include:

- **Models**: The **Follow** and **Invite** models handle relationships between users and manage invitations for following.
- **Views and URLs**: The app includes views and URL configurations for the Community page, allowing users to search for, follow, and interact with other users, with a key emphasis on displaying other users' Showcase pages.
- **Admin Configuration**: Admin configuration classes for the Follow and Invite models allow for managing social interactions via the Django admin interface.

This app serves as the foundation for user interaction, focusing on following users and prominently showcasing their achievements.

### Dashboard

The **dashboard** app provides users with a comprehensive view of their activity data over different time ranges, such as weekly, monthly, and yearly, aggregating statistics and visualizations to track progress and achievements.

Key components include:

- **DashboardWeeklyView**, **DashboardMonthlyView**, **DashboardYearlyView**: These views provide insights into user activity over the respective time periods, displaying aggregated statistics and visualizations.
- **DashboardBaseView**: A base view that supports the other dashboard views by structuring shared functionality and data handling.
- **Helper Functions**: These functions gather context data such as date ranges, ride statistics, beats, vitals, habits, trophies, kudos, and chart data for visualizing activity.

This app is designed to give users detailed feedback on their progress across various time frames.

### Feed

The **feed** app is designed to manage and display user activities in a feed format, offering both a paginated list of activities and detailed views of individual activities without directly managing any models or data.

Key components include:

- **FeedView**: Displays a paginated list of the user's activities, including kudos and beat transaction logs, with HTMX support for infinite scrolling and dynamically loading more activities as the user scrolls.
- **DetailView**: Provides a detailed view of individual activities, including ride details, allowing users to explore specific activities in depth.

This app focuses on presenting user activities rather than managing the underlying data.


### Kudos


### Pages


### Profiles


### Rides


### Showcase


## Key Directories

### makefiles/

### project/

### apps/

### config/

### Core

The **core** app serves as the foundational layer of the project, managing essential configurations and settings. It includes the following key components:

- **Root URL Configuration**: The root urls.py file, which routes all incoming HTTP requests to the appropriate app or view.
- **WSGI/ASGI Files**: Both wsgi.py and asgi.py files are present to enable the project to run under different deployment protocols (WSGI for synchronous and ASGI for asynchronous environments).
- **Settings**: The project settings are modularized using django-split-settings. The core app contains a settings/ folder, which is split into multiple settings files for easier management and customization across different environments.
- **Environment Configuration**: The core app also stores the .env file, where sensitive project environment variables, such as database credentials and secret keys, are securely managed.
- **Static Files**: The app includes a static/ folder that holds static assets like CSS, JavaScript, and image files, which are used throughout the project.

The core app is crucial for the overall configuration and serves as the backbone of the project’s setup and deployment.

### logs/

### media/

### static/

### templates/

#### includes/

### tests/

#### _first/

#### apps/

## Key Files

### tests/setup.py

### .coveragerc

### .editorconfig

### .gitignore

### .pre-commit-config.yaml

### .pre-commit-quick-config.yaml

### makefile

### poetry.lock

### pyproject.toml

### requirements.txt


