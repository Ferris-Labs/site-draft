---
title: "Secrets"
linkTitle: "Secrets"
weight: 205
description: >-
  How to integrate sensitive configurations(Secrets) within your services

---
Secrets are sensitive configuration information which you wish to use within your service. These may be a single attribute(such as a password) structures with multiple attributes.

Secrets are the ability to deal with sensitive data through scripts (secrets.json) needed for service execution, such as:

- Database Passwords 
- Secret Keys 
- API Keys
- any other sensitive data

Secrets aren't visible to any users and are passed encrypted to the actual script at the predefined service execution time. Once the script (secrets.json) is uploaded to the platform, the data is read and securely (double encryption) stored in the database.

## Secret Scopes

The DX platform supports the following scopes for a secret.

| Scope            | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| Service secrets  | Service Scope secrets are only available to the specific service within which the secret was defined. They are managed by uploading a secrets.json file on the service management UI. While they can also by synced from GIT, this is not a preferred approach in order to avoid having secrets in git. |
| Project Secrets  | Secrets that are accessible to any service within a specific project. These are created by uploading a JSON file on the project secrets tab on the UI. |
| Platform Secrets | Secrets that are accessible to any service running on the platform. These are created by uploading JSON file on the Vault->Secrets page. |

*When accessing secrets using `ferris_ef.context.secrets.get('secret_name')` it will first lookup for `secret_name` within service secrets, then project and finally platform*

##### The secrets.json File

To add service scope secrets you can upload a `secrets.json` file.

Those values are stored double encrypted in database and can be only accessed within the executing script. A sample `secrets.json`

```json
{
    "DB_NAME": "test_db",
    "DB_PASS": "supersecretpas$"
}
```

### Accessing secrets

With `ferris_ef.context.secrets` you can access secrets stored on at the platform, project or service scope.   



```python
from ferris_ef import context
context.secrets.get('secret_name')
```



This command will first lookup for secret named `secret_name` within service secrets (defined in `secrets.json` file of the service). If such key doesn't exist it will lookup for it within project secrets, and finally within platform's secrets. If secret with such name doesn't exist `None` will be returned.

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



## Create a new service

Note that the service creation was presented in another submenu of the User Guide, so only the needed parameters will be filled in the service to showcase the Secrets functionality.

1. Click on Executions in the left side menu and on services

2. Click on Add to create a new service

{{< blocks/screenshot color="white" image="/images/create_service_secrets.png">}}

3. Name the service
4. Click on choose file and add the python scrypt (test_secrets.py)
5. Click on Add more scripts and click on choose file to add the JSON script (secrets.json)
6. Click on Save to save the service

{{< blocks/screenshot color="white" image="/images/save_service_secrets.png">}}

##### test_secrets.py script

This is an example script that shows how secrets from the `secrets.json` file can be accessed from a script at execution time using the `get_secret()` helper function from the `ferris_ef` service.

```python
from ferris_ef import get_secret, get_param

print(f"DB NAME: {get_secret('DB_NAME')}")
print(f"DB PASS: {get_secret('DB_PASS')}")

print(f"service NAME: {get_param('service_name')}")
```