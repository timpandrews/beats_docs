# Tools and Resources

## Development Environment


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


### Linters ![Linters](assets/icons/linter.png){: width="2%"} 
TODO: complete this

### EditorConfig ![editorconfig](assets/icons/editorconfig.png){: width="2%"} 
TODO: complete this

### Coverage ![Coverage](assets/icons/coverage.png){: width="2%"}
TODO: complete this