# Adding Kudos to the Application

<hr style="border: 2px solid black;">

## How to Add Kudos

There are two main ways to add kudos to the application:  
1. **Simple kudos** using a database query in kudos.yaml  
2. **Complex kudos** using a custom function in checks.py  

<hr style="border: 1px solid black;">

## Method 1: Adding Simple Kudos

For simple kudos that can be determined using a straightforward database query or condition, you can add an entry directly in the kudos.yaml file. 

### Steps:   
1. **Open** the project/config/kudos.yaml file.   
2. **Add** a new entry under the kudos section with a unique key for your kudo.   
3. **Fill in** the required fields for the kudo.  

#### Example:

```yaml
kudos:
  your_new_kudo_name:
    include_in_check: true
    beats: 50
    code: |
      if Activity.objects.filter(user=user, activity_type="ride").count() >= 10:
        achieved = True
      else:
        achieved = False
    kudos_type: badge
    display_type: user
    name: Ten Rides Badge
    icon_family: fa
    icon_name: fa-bicycle
    style:
      size: 3em
      color: ForestGreen
```
#### Required Fields:   
- include_in_check: Set to true if this kudo should be checked for each activity.  You can set this to false for kudos that are only awarded under specific conditions (e.g. New User Kudos)
- beats: The number of beats awarded for this kudo.   
- code: A Python code snippet that sets the achieved variable to True or False.   
- kudos_type: Can be "trophy", "badge", or "streak".    
- display_type: Can be "user", "single", "multiple", or "streak".    
- name: The display name of the kudo.   
- icon_family: The icon family (e.g., "fa" for Font Awesome, "bi" for Bootstrap Icons).   
- icon_name: The specific icon name.   
- style: A dictionary containing size and color for the icon.   

<hr style="border: 1px solid black;">

## Method 2: Adding Complex Kudos

For more complex kudos that require advanced logic or multiple database queries, you'll need to create a custom function in `checks.py` and reference it in `kudos.yaml`.  

### Steps:   
1. **Open** the project/apps/kudos/checks.py file.  
2. **Define** a new function for your kudo check.  
3. **Open** the project/config/kudos.yaml file.  
4. **Add** a new entry referencing your custom function.  

#### Examples:

```python title="checks.py"
def check_complex_kudo(user, activity, config):
    # Your complex logic here
    # ...
    if complex_condition_met:
        return True, {"additional_info": "Some details"}
    else:
        return False, None
```

```yaml title="kudos.yaml"
kudos:
  complex_kudo_name:
    include_in_check: true
    beats: 75
    code: "function:check_complex_kudo"
    kudos_type: trophy
    display_type: single
    name: Complex Achievement Trophy
    icon_family: bi
    icon_name: bi-award
    style:
      size: 4em
      color: Purple
```

#### Function Requirements:  
- The function should take three parameters: user, activity, and config.  
- It should return a tuple: (achieved, details).  
    - achieved is a boolean indicating if the kudo was earned.   
    - details is either None or a dictionary with additional information.    

#### How It Works:  
The check_for_kudos function in views.py processes each kudo defined in kudos.yaml:  
1. It loads the kudo configuration from kudos.yaml.    
2. For each kudo, it checks if include_in_check is True.  
3. It then executes the code for the kudo:  
    - If the code is a Python snippet, it's executed directly.  
    - If the code starts with "function:", it calls the corresponding function in `checks.py`.  
4. If the kudo is achieved, it creates a new `Kudo` object and associates it with the user and activity. 

<hr style="border: 2px solid black;">

## Important Files / Functions

<hr style="border: 1px solid black;">

### Kudos.yaml

- kudos.yaml contains the configuration for the kudos system.  It is used to define the kudos that can be awarded to users.
- kudos.yaml is located @ **project/config/kudos.yaml**
- The location for this file is defined in **settings.CONFIG_PATH**

#### Examples:
```yaml title="Generic Example with explanations"
 kudo_name:
   include_in_check: true/false
   code:  provide an if statement or function name to check if the kudo is
          achieved if an if statement is provided, then the if statement will
          be evaluated or if a function name is provided, then the function
          will be called.
   kudos_type: trophy/badge/streak
   name: Name of the kudo (as displayed within the app)
   icon_family: fa/bi (Font Awesome, Bootstrap Icons, or others may be added
                in the future)
   icon_name: Name of the icon to be used
   style:  dictionary containing the style of the icon
     size: size of the icon
     color: color of the icon
```

```yaml title="Example of kudo with if/then statement"
metric_century_trophy:
  include_in_check: true
  code: |
    if activity.core_data["distance"] >= 100:
      achieved = True
    else:
      achieved = False
  kudos_type: trophy
  name: Metric Century Trophy
  icon_family: fa
  icon_name: fa-star
  style:
    size: 3em
    color: MidnightBlue
```  
```yaml title="Example of kudo with function"
two_hundred_km_in_a_week_trophy:
  include_in_check: true
  code: "function:check_two_hundred_km_in_a_week"
  kudos_type: trophy
  name: 200 km in a week
  icon_family: bi
  icon_name: bi-patch-check-fill
  style:
    size: 3em
    color: Gold
```

<hr style="border: 1px solid black;">

### check_for_kudos()

The check_for_kudos function is located in the project/apps/kudos/views.py file. This function serves as the main entry point for evaluating and awarding kudos to users based on their activities.

#### Purpose:
The primary purpose of check_for_kudos is to determine whether a user has earned any kudos for a given activity. It acts as a bridge between the activity data and the kudo definitions, applying the criteria specified in the kudos.yaml configuration file to decide if a kudo should be awarded.

#### Functionality:
- Reads the kudo configuration from the kudos.yaml file.
- Iterates through each kudo definition in the configuration.
- Evaluates whether the given activity meets the criteria for each kudo.
- Awards kudos to the user when criteria are met.
- Handles both simple (inline code) and complex (function-based) kudo checks.

#### How It's Called:
This function is typically called after a new activity is created or updated. It would be invoked in views or background tasks that process user activities.

```python
# After creating or updating an activity
check_for_kudos(user, activity)
```

#### Key Features:
- Supports excluding specific kudos from being checked (useful for combined activities).
- Dynamically imports and executes complex check functions from project.apps.kudos.checks.
- Logs various stages of the kudo checking process for debugging and monitoring.
- Handles both inline code and function-based kudo criteria.

#### Parameters:
- *user*: The user for whom kudos are being checked.
- *activity*: The activity being evaluated for kudos.
- *excluded_kudos*: An optional list of kudo names to exclude from checking.

#### Integration:
This function integrates closely with:  
- The **kudos.yaml** configuration file.  
- The **checks.py** module for complex kudo evaluations.  
- The logging system for tracking the kudo checking process.  

By centralizing the kudo checking logic in this function, the application maintains a consistent approach to awarding kudos across different types of activities and achievements.

<hr style="border: 1px solid black;">

### checks.py

The checks.py file is located in the project/apps/kudos/ directory. This file contains the logic for evaluating complex kudos that require more sophisticated checks than simple database queries.

#### Purpose and Functionality:
- Houses functions that determine whether a user has earned specific kudos based on their activities.
- Each function in this file corresponds to a complex kudo check defined in the kudos.yaml configuration.
- These functions analyze user activities, streaks, and other relevant data to decide if a kudo should be awarded.

#### Structure and Design:
- Contains main check functions for different types of kudos (e.g., streaks, distance milestones).
- Includes helper functions to support the main checks, handling common tasks like age calculation or streak management.
- Utilizes Django models, particularly Activity and Kudo, to interact with the database.

#### Integration with the Kudos System:
- Functions in this file are called by the check_for_kudos function in views.py.
- They are referenced in the kudos.yaml file using the function: prefix in the code field of kudo definitions.

#### Function Signature and Return Values:
- Most functions follow a standard signature: def check_function_name(user, activity, config):
- They typically return a tuple: (achieved, details), where achieved is a boolean and details is a dictionary or None.

#### Key Features:
- Implements complex logic for kudos that can't be determined by simple database queries.
- Handles time-based calculations, often using the pendulum library for advanced date and time operations.
- Includes logging for tracking important events and potential issues.
- Manages edge cases and ensures data integrity (e.g., preventing duplicate kudos).

#### Extensibility:
- New complex kudo checks can be added to this file, following the established patterns and conventions.
- Developers can create custom logic for new types of achievements or milestones.
- By centralizing complex kudo checks in checks.py, the application maintains a clean separation of concerns and allows for easy addition and modification of kudos logic.

<hr style="border: 1px solid black;">

### get_kudos_config() 

The `get_kudos_config()` function is a crucial utility that retrieves the kudos configuration for the project from a YAML file.

#### Purpose
- Loads and returns the kudos configuration from `kudos.yaml`
- Centralizes configuration access for consistency across the project

#### Location
- File: `project/apps/common/utils/config.py`
- Module: `project.apps.common.utils.config`

#### Usage
- Primary caller: `check_for_kudos()` function in `project/apps/kudos/views.py`
- Used in kudos-related operations throughout the project

#### Functionality
1. Constructs the path to `kudos.yaml` using `settings.CONFIG_PATH`
2. Opens and reads the YAML file
3. Loads the YAML content into a Python dictionary
4. Extracts and returns the 'kudos' section as `dict_items`

#### Returns
- `dict_items`: Key-value pairs of kudos configurations

The `get_kudos_config()` function ensures that all parts of the project have access to the latest kudos configuration, facilitating consistent kudos checking and awarding processes.

<hr style="border: 1px solid black;">