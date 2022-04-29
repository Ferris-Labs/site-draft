---
title: "Secrets"
linkTitle: "Secrets"
description: >-
  How to integrate different Secrets(sensitive data) throughout the Ferris Platform.

---

> ADDED BY NIKOLA

### Service secrets

Uploaded/synced with rest of service scripts as `secrets.json` file. Stored encrypted in database and are passed to the scripts at run time.

### Project Secrets

Created by uploading JSON file on the project secrets tab on the UI.

Can be accessed using `ferris_ef.context.secrets.get('secret_name')`

Can be set using `context.secrets.set("secret_name", {"somekey":"someval"}, "project")`


### Platform Secrets

Created by uploading JSON file on the Vault->Secrets page.

Can be accessed using `ferris_ef.context.secrets.get('secret_name')`

Can be set using `context.secrets.set("secret_name", {"somekey":"someval"}, "platform")`


*When accessing secrets using `ferris_ef.context.secrets.get('secret_name')` it will first lookup for `secret_name` within service secrets, then project and finally platform*


> END OF ADDED BY NIKOLA  


Secrets are the ability to deal with sensitive data through scripts (secrets.json) needed for package execution, such as:

- Database Passwords 
- Secret Keys 
- API Keys
- any other sensitive data

Secrets aren't visible to any users and are passed encrypted to the actual scrypt at the predefined package execution time. Once the script (secrets.json) is uploaded to the platform, the data is read and securely (double encryption) stored in the database. 

## Create a new package

Note that the package creation was presented in another submenu of the User Guide, so only the needed parameters will be filled in the package to showcase the Secrets functionality.

1. Click on Executions in the left side menu and on Packages

2. Click on Add to create a new package

{{< blocks/screenshot color="white" image="/images/create_package_secrets.png">}}

3. Name the package
4. Click on choose file and add the python scrypt (test_secrets.py)
5. Click on Add more scripts and click on choose file to add the JSON script (secrets.json)
6. Click on Save to save the package

{{< blocks/screenshot color="white" image="/images/save_package_secrets.png">}}

##### test_secrets.py script

This is an example script that shows how secrets from the `secrets.json` file can be accessed from a script at execution time using the `get_secret()` helper function from the `ferris_ef` package.

```python
from ferris_ef import get_secret, get_param

print(f"DB NAME: {get_secret('DB_NAME')}")
print(f"DB PASS: {get_secret('DB_PASS')}")

print(f"PACKAGE NAME: {get_param('package_name')}")
```

##### secrets.json script

The `secrets.json` file contains sensitive key/value pairs that can be accessed in scripts at execution time. Those values are stored double encrypted in database and can be only accessed within the executing script.

```json
{
    "DB_NAME": "test_db",
    "DB_PASS": "supersecretpas$"
}
```

## Check Created Package

1. Click on the magnifying glass to open the package details page

{{< blocks/screenshot color="white" image="/images/check_package_secrets.png">}}

2. Check the scripts attached

Note that only the `test_secrets.py` script is viewable and downloadable. The `secrets.json` script will never be stored anywhere. 

3. Click on run to execute trigger the execution of the package

Once the file is uploaded to the platform, it gets read and all secrets contained in that file will be encrypted with the encryption key that is generated for each package and stored into the database (in this case PostgreSQL). Once the package is ran, it will trigger an event with encypted secrets. At the moment it arrives to the executor for execution, the executor will decrypt the keys and send them to the scripts.

{{< blocks/screenshot color="white" image="/images/check_script_run_execution_secrets.png">}}

After hitting the run button (manual package execution) the user will be automatically redirected to the details page of the package execution (List Package Executions tab)

4. Click on the magnifying glass to open the package execution details page

{{< blocks/screenshot color="white" image="/images/package_execution_secrets.png">}}

5. Click on List Steps tab to open the package execution steps details page

{{< blocks/screenshot color="white" image="/images/details_page_package_execution_secrets.png">}}

6. Click on Show Results to open and see the decrypted secrets

{{< blocks/screenshot color="white" image="/images/package_exec_steps_secrets.png">}}

{{< blocks/screenshot color="white" image="/images/show_results_decrypted_secrets.png">}}