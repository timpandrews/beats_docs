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
* Run Django Development Server <small>(Runs the Django development server on 127.0.0.1:8000.)</small>
```bash
make run-server
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
make test-dashboard
make test-feed
make test-kudos
make test-pages
make test-rides
```
* Run Tests with Verbosity <small>(Runs tests with higher verbosity.)</small>
```bash
make test-v2
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
