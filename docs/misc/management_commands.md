# Django Management Commands

## Overview
This document outlines the available Django management commands in the project.

## Commands

### **:octicons-terminal-24: check_levels**

Django management command to check if the Levels Model is populated."""

### **:octicons-terminal-24: delete_stash_json_data**

A Django management command to clear all entries from the StashJsonData model.

This command deletes all data from the StashJsonData table, which temporarily stores JSON data for user review before import or discard. It ensures cleanup of leftover data, which may remain due to interruptions in the process. The command will also report the number of entries deleted and is included with commands executed alongside migrate to maintain database consistency.

### **:octicons-terminal-24: migrate_kudo_name_data**

A Django management command to update the name and display_name fields in the Kudo model, ensuring consistent naming conventions and proper display values.

#### Description
This command processes a predefined list of kudo name mappings to update existing records in the database. Each mapping consists of:
- Current name: The existing value in the database
- New name: The standardized internal name (typically snake_case)
- Display name: The user-friendly name for UI display

The command supports a dry-run mode for testing changes before applying them to the database.

#### Basic Execution
To run the migration and update the database:

```bash
poetry run python manage.py migrate_kudo_names
```

#### Dry Run
To preview changes without modifying the database:

```bash
poetry run python manage.py migrate_kudo_names --dry-run
```

#### Options
- `--dry-run`: Execute the command without making changes to the database. Shows what changes would be made.

#### Notes
- Always run with `--dry-run` first to verify the expected changes
- The command will only update records where the current name matches exactly
- Updates are performed in a single transaction per mapping
- Command progress is logged to stdout

### **:octicons-terminal-24: send_test_email**

A Django management command to send test emails for various django-allauth email templates.

This command allows developers to test and verify email templates such as account_already_exists, email_confirmation, password_reset, and more. Each email type has a shorthand for quick usage. It is useful during development to ensure templates are functioning and formatted correctly.

#### Supported Email Types
- account_already_exists (shorthand: exists)
- email_confirmation (shorthand: confirm)
- email_confirmation_signup (shorthand: signup)
- password_reset (shorthand: reset)
- unknown_account (shorthand: unknown)

#### Usage

```bash
poetry run python manage.py send_test_email <email_type>
```

#### Examples

```bash
poetry run python manage.py send_test_email account_already_exists
poetry run python manage.py send_test_email confirm
```

### **:octicons-terminal-24: sync_filename_data**

A Django management command to sync the FileRideNameData model with data from a YAML file.

This command reads a YAML file (file_ride_name_data.yaml) to update the FileRideNameData model. It adds new entries from the file that are missing in the database and removes entries from the database not found in the file. Useful for keeping the model's data in sync with the YAML configuration.

#### Key Features

- Add New Entries: Inserts records from the YAML file that are missing in the database.
- Remove Stale Entries: Deletes records in the database that are no longer present in the YAML file.

#### Usage
Run the command using the Django management CLI:

```bash
poetry run python manage.py sync_filename_data
```

### **:octicons-terminal-24: sync_kudos_config**

A Django management command that syncs kudos data from a YAML file to the database.

This command reads the kudos.yaml file, clears existing kudo entries in the
database, and populates the database with the new data from the YAML file. The
YAML file is considered the master source of truth for the kudo configurations.

### **:octicons-terminal-24: test_convert_filename_to_ridename**

A utility to test the get_ride_name_from_file_name function by verifying its output against a set of predefined test cases.

The script creates a list of test cases, each consisting of a file name and its corresponding expected ride name. For each test case, the function is executed, and the input file name, the output ride name from the function, and the expected ride name are printed to the console. This process ensures that the function behaves as expected and highlights any discrepancies for further debugging.

### **:octicons-terminal-24: test_user_creation**

A management command to test the user creation process and inspect the emails generated during registration.

This command uses Django's test client to simulate a user registration process and verifies its success. It also checks the emails generated during the process to ensure proper functionality. An optional flag allows for the deletion of the test user after the test is complete, ensuring a clean database.

#### Usage

To create a test user:

```bash
poetry run python manage.py test_user_creation
```

To delete the test user after the test:

```bash
poetry run python manage.py test_user_creation --delete
```
