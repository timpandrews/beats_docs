# Dependency Management (Poetry)

## Overview 
This section provides guidance on using Poetry for dependency management within this project. Poetry simplifies the process of managing Python packages and helps maintain a consistent and reproducible development environment.

![Poetry](../assets/icons/poetry-python.svg){: width="25%"}

 - Poetry ![poetry-python](../assets/icons/poetry-python.svg){: width="2%"}   
<small>Poetry is a Python dependency management and packaging tool. It simplifies the process of managing project dependencies, creating virtual environments, and packaging Python projects for distribution. Poetry uses a pyproject.toml file to define dependencies and project settings, making it a modern and user-friendly tool for Python developers.</small>   
<a href="https://python-poetry.org/" target="_blank">Poetry.org</a> |
<a href="https://github.com/python-poetry/poetry" target="_blank">:fontawesome-brands-github: GitHub</a>



## Setup
* Prerequisites <small>(Ensure that Poetry is installed on your machine. You can install it using the following command:)</small>
```bash
pip install poetry
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