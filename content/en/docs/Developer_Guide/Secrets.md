---
title: "Secrets"
linkTitle: "Secrets"
description: >-
  How to integrate sensitive configurations(Secrets) within your services

---
Secrets are sensitive configuration information which you wish to use within your service. These may be a single attribute(such as a password) structures with multiple attributes.

Secrets are the ability to deal with sensitive data through scripts (secrets.json) needed for package execution, such as:

- Database Passwords 
- Secret Keys 
- API Keys
- any other sensitive data

Secrets aren't visible to any users and are passed encrypted to the actual script at the predefined package execution time. Once the script (secrets.json) is uploaded to the platform, the data is read and securely (double encryption) stored in the database.

## Secret Scopes

The DX platform supports the following scopes for a secret.

| Scope            | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| Service secrets  | Service Scope secrets are only available to the specific service within which the secret was defined. They are managed by uploading a secrets.json file on the service management UI. While they can also by synced from GIT, this is not a preferred approach in order to avoid having secrets in git. |
| Project Secrets  | Secrets that are accessible to any service within a specific project. These are created by uploading a JSON file on the project secrets tab on the UI. |
| Platform Secrets | Secrets that are accessible to any service running on the platform. These are created by uploading JSON file on the Vault->Secrets page. |

*When accessing secrets using `ferris_ef.context.secrets.get('secret_name')` it will first lookup for `secret_name` within service secrets, then project and finally platform*



### Accessing secrets

With `ferris_ef.context.secrets` you can access secrets stored on at the platform, project or service scope.   



```python
from ferris_ef import context
context.secrets.get('secret_name')
```



This command will first lookup for secret named `secret_name` within package secrets (defined in `secrets.json` file of the package). If such key doesn't exist it will lookup for it within project secrets, and finally within platform's secrets. If secret with such name doesn't exist `None` will be returned.

Can be accessed using `ferris_ef.context.secrets.get('secret_name'). Can be set using `context.secrets.set("secret_name", {"somekey":"someval"}, "project")`

Can be accessed using `ferris_ef.context.secrets.get('secret_name')`. Can be set using `context.secrets.set("secret_name", {"somekey":"someval"}, "platform")`

### Setting secrets

Using `ferris_ef.context.secrets.set(name, value, context)` method you can set secrets on project and platform level.   

```python
from ferris_ef import context

context.secrets.set(name="platform_secret", value={"somekey":"someval"}, context="platform")
```

| Parameter | Description                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| name | Name of the secret to be set. If secret with the same name already exist it will be updated |
| value | Value of the secret that should be set |
| context | Context of the secret. Possible values are `platform` and `project` |



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