# Tools and Resources

## Development Environment

### Make File ![makefile](assets/icons/makefile.png){: width="2%"}  

#### Purpose
This Makefile provides convenient commands for managing your Django project using Poetry. It covers installation, Django commands, testing, and pre-commit, linting, and formatting tasks.

#### Poetry Commands
* Install Dependencies <small>(Installs project dependencies using Poetry.)</small>
```bash
make install
```
* Activate Virtual Environment <small>(Activates the Poetry virtual environment.)</small>
```bash
make shell
```
#### Django Commands
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
#### Testing Commands
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
#### Pre-commit, Linting, and Formatting Commands
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

### Poetry ![poetry-python](assets/icons/poetry-python.svg){: width="2%"}  

#### Overview 
This section provides guidance on using Poetry for dependency management within this project. Poetry simplifies the process of managing Python packages and helps maintain a consistent and reproducible development environment.

#### Setup
* Prerequisites <small>(Ensure that Poetry is installed on your machine. You can install it using the following command:)</small>
```bash
pin install poetry
```
* Installation <small>(To install project dependencies using Poetry, run:)</small>
```bash
git clone [repository_url]
cd beats
poetry install --no-root
```
<small>\* the --no-root option installs the project's dependencies defined in pyproject.toml without including the root project itself.</small>

* Virtual Environment <small>(Activate the Poetry virtual environment to work within an isolated environment:)</small>
```bash
poetry shell
```
-- or manually --
```bash
source .venv\bin\activate
```
#### Add Dependencies
<small>To add dependencies to this project execute the following command</small>
```bash
poetry add [dependency_name]
```
<small>This adds the dependency to the pyproject.toml file</small>
```text
[tool.poetry.dependencies]
dependency_name = "^2.1"
```

#### Running commands in poetry shell
<small>Most common command can be executing using make statements. [see Makefile](#make-file) If there are commands that are not included in the make file you can execute
them using the following convention.</small>
```bash
poetry run python your_script.py
poetry run python manage.py shell
poetry run command_name [--options]
poetry run isort file_name.py
```

### pre-commit ![pre-commit](assets/icons/pre-commit.svg){: width="2%"} 
TODO: complete this

### Using the django shell ![django](assets/icons/django-icon.svg){: width=2%"} 

```bash
make dj-shell
```
TODO: complete this

### Linters ![Linters](assets/icons/linter.png){: width="2%"} 
TODO: complete this

### EditorConfig ![editorconfig](assets/icons/editorconfig.png){: width="2%"} 
TODO: complete this

### Coverage ![Coverage](assets/icons/coverage.png){: width="2%"}
TODO: complete this