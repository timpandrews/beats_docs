# Installation Guide - Development Environment
<small>\* TODO: This process has not been tested</small>

1. Clone the Repository:
    ```bash
    git clone [repository_url]
    ```
2. Navigate to the Project Directory:
    ```bash
    cd beats
    ```
3. Install Dependencies with Poetry:  
    <small>\* install poetry if necessary <a href="https://python-poetry.org/docs/#installation" target="_blank">Poetry</a></small>
    ```bash
    pip install poetry
    ```
    ```bash
    poetry install
    ```
4. Activate the Virtual Environment:
    ```bash
    poetry shell
    ```
5. Apply Database Migrations:
    <small>\* using makefile target</small>
    ```bash
    make migrations
    ```
6. Run the Development Server:
    <small>\* using makefile target</small>
    ```bash
    make run
    ```
    local server url: 127.0.0.1:8000



This project was setup using a combination of the the process I defined in the following 
gist as well new tools such as poetry, makefiles and pre-commit (and associated linting tools)
that are described in the followign youtube tutorial.

<a href="https://www.youtube.com/watch?v=DaxcmbWcdTA&list=PL6gx4Cwl9DGDYbs0jJdGefNN8eZRSwWqy" target="_blank">:fontawesome-brands-youtube: Pro Django - Tutorial</a> | <a href="https://gist.githubusercontent.com/timpandrews/0d71f20eaaef05cd73b36ba70b4c3093/raw/e685eae773d75ad1d3ce9dbf120b62e6fdf627b0/gistfile1.md" target="_blank">:octicons-logo-gist-16: Setting up a new project</a>