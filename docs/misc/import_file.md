# Details on the Process Used to Import Files

*.fit and .gpx files are supported*  

## Big Picture Steps

1. Select File
2. Using the file name pre-check that the file appears to be a valid file type (.fit or .gpx)  
3. Process Input File & return Form obj
    - Open file
    - Determine if file is .fit or .gpx
    - Create `file_data` dict by calling ???fit -- or -- _get_data_from_gpx()
    - Stash original data in form of `file_data` dict in `StashJsonData` model
    - Create `pre_prop_form_data` dict with data from `file_data` dict
    - Create `RideFormFull` obj with data from the `pre_prop_form_data` dict
    - Return RideFormFull obj
4. Display Pre-populated form for user to review, edit, and submit
5. Process form data and save data to Activity Model
    - If form.is_valid() get form.cleaned_data
    - Create and Save an Activity instance with:
        - core_data(ride_name, distance, duration, elevation, calories)
        - summary_data(speed, hr, cadence, power, etc.)
6. Retrieve & Process data from StashJsonData and save RideDetail Model
    - Retrieve data from the StashJsonData model
    - Process data into a standard format used for mapping_data
    - Create and Save an RideDetail instance with:
        - mapping_data
        - original_data
7. check_for_kudos()
8. calculate_beats
9. Redirecto to feed



### Data Notes  

- **file_data** dictionary contains raw data from input file and its content and format varies depending on the input files type and makeup.
- **pre_prop_form_data** dictionary contains data that has be manipulated and should be the same regardless of the input files type or makeup.
- **original_data** field in RideDetail model contains a JSON object of the original data from the input file.  It will differ based on type and makeup.
- **mapping_data** field in RideDetail model contains a JSON object that is specif built for this project and contains multiple waypoints with data such as long, lat, power, speed, cadence, altitude, hr, timestamp, etc.

## Steps Involved

1. Select File

    Display template for user to select file to be imported

    ```py title="rides/urls.py"
    path("rides/select_file/", ImportFromFileView.as_view(), name="select_file"),
    ```

    Calls rides.views.ImportFromFileView

2. Validate File Name

    HTMX function determines if the filename is valid.  Valid filenames end in either .fit or .gpx.  If name is valid the valid message is displayed and submit button is enabled.  If name is not valid a warning message is displayed and submit button remains disabled.

    ```py title="rides/urls.py"
    path("rides/validate_file_name/", validate_file_name, name="validate_file_name"),
    ```

3. Process File - Step 1

    Calls rides.htmx.process_file function.  This is step1 in the file import process.  This function will process the file and return a form pre-populated with the data from the file.  

    The output of this function returns the HTML & Form data to pre populate the form that gets submitting in the Step 2

    ```py title="rides/urls.py"
    path("rides/process_file/", process_file, name="process_file"),
    ```

4. Determine File type

    Calls rides.htmx._get_file_type() to determine file type (.fit or .gpx)

    ```py title="rides.htmx.process_file"
    file_type = _get_file_type(uploaded_file)
    ```

5. Process file and build Form data

    ```py title="rides.htmx._process_file"
    form = _process_file(uploaded_file, file_type, request)
    ```

6. Import File and Return a Dictionary object

    A file_data object is created by calling a file type specific import function

    ```py title="rides.htmx."
    if file_type == "FIT":
        file_data = import_fit_file(file_path)
    elif file_type == "GPX":
        file_data = import_gpx_file(file_path)
    ```

7. Create Form Obj with pre populated data from input file
