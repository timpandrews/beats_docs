# Makefile Documentation

## Introduction to Makefiles

Makefiles are used to automate and simplify complex build processes and task execution in software projects. They define a set of rules and dependencies that allow developers to run common tasks with simple commands.

In our project, we use Makefiles to streamline various development tasks, including running tests, linting code, managing the Django application, and handling Poetry dependencies.

## Makefile Organization

Our project's Makefiles are organized as follows:

1. `Makefile`: The main Makefile that includes other specific Makefiles.
2. `makefiles/django.mk`: Contains Django-related commands.
3. `makefiles/linting.mk`: Includes linting and code formatting commands.
4. `makefiles/testing.mk`: Defines various testing commands.
5. `makefiles/poetry.mk`: Manages Poetry-related tasks.
6. `makefiles/misc.mk`: Contains miscellaneous utility commands.

This modular structure allows for better organization and easier maintenance of our build processes.

## Available Targets

Here's a list of the main targets (commands) available in our Makefiles:

### Django Commands
- `run`: Run the Django development server
- `superuser`: Create a Django superuser
- `migrations`: Create new Django migrations
- `migrate`: Apply Django migrations
- `collectstatic`: Collect static files for Django
- `dj-shell`: Start a Django shell
- `manage`: Run a Django management command

### Linting and Formatting
- `install-pre-commit`: Install pre-commit hooks
- `update`: Update environment, run migrations, and install pre-commit hooks
- `lint`: Run quick linting with isort, ruff, and black
- `pre-commit`: Run pre-commit checks on all files
- `black`: Run black to format code
- `isort`: Run isort to sort imports
- `ruff`: Run ruff to enforce Python style and linting
- `ruff-fix`: Run ruff with fix option to automatically correct issues

### Testing
- `test` or `tests`: Run all tests
- `test-account`: Run tests for the account app
- `test-activities`: Run tests for the activities app
- `test-common`: Run tests for the common app
- `test-community`: Run tests for the community app
- `test-core`: Run tests for the core app
- `test-dashboard`: Run tests for the dashboard app
- `test-feed`: Run tests for the feed app
- `test-kudos`: Run tests for the kudos app
- `test-pages`: Run tests for the pages app
- `test-profile`: Run tests for the profile app
- `test-rides`: Run tests for the rides app
- `test-showcase`: Run tests for the showcase app
- `test-coverage`: Run tests with coverage and generate report

### Poetry Commands
- `install`: Install dependencies using Poetry
- `shell`: Start a Poetry shell

### Miscellaneous
- `help`: Display available commands
- `check-filenames`: Check and convert filenames to ride names
- `test-email`: Send a test email

## Running Makefile Commands

To run a Makefile command, open your terminal, navigate to the project root directory, and use the following syntax:

``` cmd
make <target>
```

For example:

- To run the Django development server:  

    ``` cmd
    make run
    ```

- To run all tests:
  
    ``` cmd
    make test
    ```

- To apply Django migrations:
  
    ``` cmd
    make migrate
    ```

Some commands accept additional parameters. For example:

- To run tests with a specific verbosity level:

    ``` cmd
    make test v=2
    ```

- To run a specific Django management command:

    ``` cmd
    make manage cmd=createsuperuser
    ```

- To run a specific Test at a specific verbosity level:

    ``` cmd
    make test-community path="test_views.py::TestCommunityView" v=2
    ```

You can always use the `help` target to see a list of available commands:

``` cmd
make help
```

This will display a list of targets with brief descriptions, helping you find the right command for your task.
