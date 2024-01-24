# BEATS_TOOLS

This Python CLI Application is used to build and execute custom admin tools for the Beats Django Web Project.  

Currently tools include a convert_strava_csv_to_beats_yaml tool.  Data from the activities.csv file provided by Strava can be converted into a YAML file that can be imported into the Beats Project Database use Django Admin and an Import function provided by the 
django-import-export library. 

<a href="https://github.com/timpandrews/beats_tools" target="_blank">:fontawesome-brands-github: GitHub Repository</a>

Tools Available:  
  - [convert_strava](#convert-strava-tool)

## Usage

### Installation

1. Clone the repository:

    ```bash
    git clone [repository_url]
    ```

2. Navigate to the Project directory

    ```bash
    cd beats_tools
    ```

3. Create and activate a virtual environment

    ```bash
    python3 -m venv _env
    source _env/bin/activate
    ```

4. Install dependencies
    ```bash
    pip install -r requirements.txt
    ```

### Running the Application

1. Open a terminal.
2. Navigate to the directory containing the `tool.py` file.
3. Execute command at command line

#### Command Line

- help (will list commands available):

    ```bash    
    python tools.py --help
    ```

### Tools

#### Convert Strava Tool
Takes Activities.CSV that Strava will provide when you request your data history, and
a userID that can be found in the Beats DjangoAdminSite-UserModel and
creats a .YAML file ready for import into Beats.  Import can be done using the Beats
DjangeAdminSite-ActivityModel using the import tools that is provided by the
django-import-export library.

```bash
python tools.py convert_strava --help
python tools.py convert_strava [-h] [--user_id USER_ID] [input] [output]
```
i.e.
```bash
python tools.py convert_strava --user_id 123 activities.csv output.yaml
```
