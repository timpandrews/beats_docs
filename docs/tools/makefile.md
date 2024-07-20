# Make File ![makefile](../assets/icons/makefile.png){: width="3%"}  

## Purpose
This Makefile provides convenient commands for managing your Django project using Poetry. It covers installation, Django commands, testing, and pre-commit, linting, and formatting tasks.

### Poetry Commands
* Install Dependencies <small>(Installs project dependencies using Poetry.)</small>
```bash
make install
```
* Activate Virtual Environment <small>(Activates the Poetry virtual environment.)</small>
```bash
make shell
```
### Django Commands
* Run Django Development Server <small>(Runs the Django development server on 127.0.0.1:8000.)</small> - <small>Optionally set the verbosity level</small>
```bash
make run
make run v=2  
```
* Create Superuser <small>(Creates a superuser for the Django project.)</small>
```bash
make superuser
```
* Create Migrations <small>(Creates database migrations.)</small>
```bash
make migrations
```
* Apply Migrations <small>(Applies database migrations.)</small>
```bash
make migrate
```
* Collect Static Files <small>(Collects static files for the project.)</small>
```bash
make collectstatic
```
* Django Shell <small>(Open in python shell with project environment in plass)</small>
```bash
make dj-shell
```
* Run Manage.py - <small>optionnaly apply argument for management command and additonal args</small>
```bash
make manage
make manage cmd=migrate
make manage cmd=createsuperuser args="--username admin --email admin@example.com"
```
### Testing Commands
* Run All Tests <small>(Runs all tests for the Django project.)</small>
```bash
make test
```
* Run Specific Tests <small>(Runs tests for specific Django apps.)</small>
```bash
make test-account
make test-activities
make test-common
make test-core
make test-first
make test-dashboard
make test-feed
make test-kudos
make test-pages
make test-profile
make test-rides
make test-showcase
```
* Run Tests and set Verbosity Level
```bash
make test v=1
make test-account v=2
make test-activities v=3
...
```
* Run Tests with Coverage <small>(Runs tests with coverage and generates a coverage report.)</small>
```bash
make test-coverage
```
### Pre-commit, Linting, and Formatting Commands
* Install Pre-commit Hooks <small>(Installs pre-commit hooks for linting and formatting.)</small>
```bash
make install-pre-commit
```
* Update Project <small>(Updates the project by installing dependencies, applying migrations, and installing pre-commit hooks.)</small>
```bash
make update
```
* Lint Code <small>(Runs linting checks on all project files.)</small>
```bash
make lint
```
* Format Code with Black <small>(Formats code using Black.)</small>
```bash
make black
```
* Sort Imports with isort <small>(Sorts imports using isort.)</small>
```bash
make isort
```
* Run Ruff Linter <small>(Runs Ruff linter.)</small>
```bash
make ruff
```
* Fix Ruff Linter Issues <small>(Fixes issues reported by the Ruff linter.)</small>
```bash
make ruff-fix
```
### Custom Commands
* Run send_test_email custom command - <small>With provided email type</small>
```bash
make test_email type=email_confirmation
make test_email type=password_reset
```
<small>Supported email types:
    - account_already_exists (shorthand: exists)
    - email_confirmation (shorthand: confirm)
    - email_confirmation_signup (shorthand: signup)
    - email_verification (shorthand: verify)
    - password_reset (shorthand: reset)
    - unknown_account (shorthand: unknown)</small>  

* Run check-filenames custom command  
```bash
make check-filenames
```
