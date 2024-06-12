# Add a Kudos

## Kudos.yaml

- kudos.yaml contains the configuration for the kudos system.  It is used to define the kudos that can be awarded to users.
- kudos.yaml is located @ **project/config/kudos.yaml**
- The location for this file is defined in **settings.CONFIG_PATH**

**Instructions:**
```yaml
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

**Examples**
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

## check_for_kudos()
- This function can be found at: **project.apps.kudos.views**  
- Kudos are checked when the check_for_kudos() function is called.

The check_for_kudos() function checks and awards kudos to a user based on the given activity.

This function reads the kudo configuration from a `kudos.yaml` file, then
loops through each kudo in the configuration to determine if the given activity
meets the criteria for any kudo. If a kudo's criteria are met, the kudo is created
and associated with the user and activity.

The kudo criteria can be specified as either inline code or a function reference.
The function reference should be in the format `function:function_name`, and the
function should be defined in the `project.apps.kudos.checks` module. The function
should return a boolean indicating whether the criteria are met, and optionally a
dictionary with additional details.

## get_kudos_config()  
- the get_kudos_config() function is used to read in the kudos.yaml file and retrieve 
each kudo configuration.  It returns dict_items of configuration..
- The get_kudos_config() function is located at: **project.apps.common.tools**