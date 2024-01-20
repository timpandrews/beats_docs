# BEATS_TOOLS

This Python application is used to build and execute custom admin tools for the Beats Django Web Project.  Currently tools include a convert_strava_csv_to_beats_yaml tool.  Data from the 
activities.csv file provided by Strava can be converted into a YAML file that can be imported into 
the Beats Project Database use Django Admin and an Import function provided by the 
django-import-export library. 

The tools is command-line interface to define the command, input file, output file, and user ID.

<a href="https://github.com/timpandrews/beats_tools" target="_blank">:fontawesome-brands-github: GitHub Repository</a>

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

- help:

    ```bash    
    python tools.py --help
    ```

- convert Strava CVS file to Beats YAML file:

    ```bash
    python tools.py convert --user_id [user_id] [input_file] [output_file] 
        -- or --
    python tools.py convert [input_file] [output_file] --user_id [user_id]
    ```