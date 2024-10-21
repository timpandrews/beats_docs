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

### Main Commands

- `help`: List all available commands  
  Usage: `make help`

### Testing Commands

- `test`: Run all tests  
  Usage: `make test [v=0|1|2|3]`
  Example: `make test v=2`

- `tests`: Alias for `test`  
  Usage: `make tests [v=0|1|2|3]`

- `test-account`: Run tests for the account app  
  Usage: `make test-account [v=0|1|2|3] [path=<test_path>]`  
  Example: `make test-account v=2 path="test_views.py::TestAccountView"`  

- `test-activities`: Run tests for the activities app  
  Usage: `make test-activities [v=0|1|2|3] [path=<test_path>]`  

- `test-common`: Run tests for the common app  
  Usage: `make test-common [v=0|1|2|3] [path=<test_path>]`  

- `test-community`: Run tests for the community app  
  Usage: `make test-community [v=0|1|2|3] [path=<test_path>]`  

- `test-core`: Run tests for the core app  
  Usage: `make test-core [v=0|1|2|3]`  

- `test-first`: Run special tests in '_first' folder  
  Usage: `make test-first [v=0|1|2|3]`  

- `test-dashboard`: Run tests for the dashboard app  
  Usage: `make test-dashboard [v=0|1|2|3] [path=<test_path>]`  

- `test-feed`: Run tests for the feed app  
  Usage: `make test-feed [v=0|1|2|3] [path=<test_path>]`  

- `test-kudos`: Run tests for the kudos app  
  Usage: `make test-kudos [v=0|1|2|3] [path=<test_path>]`  

- `test-pages`: Run tests for the pages app  
  Usage: `make test-pages [v=0|1|2|3] [path=<test_path>]`  

- `test-profile`: Run tests for the profile app  
  Usage: `make test-profile [v=0|1|2|3] [path=<test_path>]`  

- `test-rides`: Run tests for the rides app  
  Usage: `make test-rides [v=0|1|2|3] [path=<test_path>]`  

- `test-showcase`: Run tests for the showcase app  
  Usage: `make test-showcase [v=0|1|2|3] [path=<test_path>]`  

- `testcase`: Run tests in the testcases folder  
  Usage: `make testcase [v=0|1|2|3]`  

- `test-coverage`: Run tests with coverage and generate report  
  Usage: `make test-coverage`

### Linting and Formatting Commands

- `install-pre-commit`: Install pre-commit hooks  
  Usage: `make install-pre-commit`

- `update`: Update environment, run migrations, and install pre-commit hooks  
  Usage: `make update`  

- `lint`: Run quick linting with isort, ruff, and black  
  Usage: `make lint`

    _Note: This command can be run frequently, as it only runs linting tools that
    will execute quickly to ensure code quality without slowing down your workflow._

- `pre-commit`: Run pre-commit checks on all files  
  Usage: `make pre-commit`

    _Note: This command should be run before making major commits, completing
    branches, or submitting a pull request. It ensures all linting tools are
    executed and updates poetry.lock and requirements.txt files for
    consistency._

- `black`: Run black to format code  
  Usage: `make black`  

- `isort`: Run isort to sort imports  
  Usage: `make isort`  

- `ruff`: Run ruff to enforce Python style and linting  
  Usage: `make ruff`  

- `ruff-fix`: Run ruff with fix option to automatically correct issues  
  Usage: `make ruff-fix`  

### Django Commands

- `run`: Run the Django development server  
  Usage: `make run [v=0|1|2|3]`  

- `superuser`: Create a Django superuser  
  Usage: `make superuser`  

- `migrations`: Create new Django migrations  
  Usage: `make migrations`  

- `migrate`: Apply Django migrations  
  Usage: `make migrate`  

- `collectstatic`: Collect static files for Django  
  Usage: `make collectstatic`  

- `dj-shell`: Start a Django shell  
  Usage: `make dj-shell`  

- `manage`: Run a Django management command  
  Usage: `make manage [cmd=<command>] [args=<arguments>]`  
  Example: `make manage cmd=commandname args=arg1,arg2`  

### Poetry Commands

- `install`: Install dependencies using Poetry  
  Usage: `make install`  

- `shell`: Start a Poetry shell  
  Usage: `make shell`  

### Miscellaneous Commands

- `check-filenames`: Check and convert filenames to ride names  
  Usage: `make check-filenames`  

- `test-email`: Send a test email  
  Usage: `make test-email type=<email_type>`  
  Example: `make test-email type=welcome`  

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
