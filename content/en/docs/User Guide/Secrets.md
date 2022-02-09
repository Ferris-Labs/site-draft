---
title: "Secrets"
linkTitle: "Secrets"
weight: -9
description: >-
  How to integrate different Secrets(sensitive data) throughout the Ferris Platform.

---

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

![](/images/create_package_secrets.png)

3. Name the package
4. Click on choose file and add the python scrypt (test_secrets.py)
5. Click on Add more scripts and click on choose file to add the JSON script (secrets.json)
6. Click on Save to save the package

![](/images/save_package_secrets.png)

##### test_secrets.py script

"Text will be added later"``

```python
import os

import sys, json
from ferris_ef import get_secret, get_param

print(f"DB NAME: {get_secret('DB_NAME')}")
print(f"DB PASS: {get_secret('DB_PASS')}")

print(f"PACKAGE NAME: {get_param('package_name')}")

fa = json.loads(sys.argv[1])
secrets = fa['secrets']

for k, v in secrets.items():
    print(f"{k} -> {v}")


print(os.environ)
```

##### secrets.json script

"Text will be added later"

```json
{
    "DB_NAME": "test_db",
    "DB_PASS": "supersecretpas$"
}
```

## Check Created Package

1. Click on the magnifying glass to open the package details page

![](/images/check_package_secrets.png)

2. Check the scripts attached

Note that only the `test_secrets.py` script is viewable and downloadable. The `secrets.json` script will never be stored anywhere. 

3. Click on run to execute trigger the execution of the package

Once the file is uploaded to the platform, it gets read and all secrets contained in that file will be encrypted with the encryption key that is generated for each package and stored into the database (in this case PostgreSQL). Once the package is ran, it will trigger an event with encypted secrets. At the moment it arrives to the executor for execution, the executor will decrypt the keys and send them to the scripts.

![](/images/check_script_run_execution_secrets.png)

After hitting the run button (manual package execution) the user will be automatically redirected to the details page of the package execution (List Package Executions tab)

4. Click on the magnifying glass to open the package execution details page

![](/images/package_execution_secrets.png)

5. Click on List Steps tab to open the package execution steps details page

![](/images/details_page_package_execution_secrets.png)

6. Click on Show Results to open and see the decrypted secrets

![](/images/package_exec_steps_secrets.png)

![](/images/show_results_decrypted_secrets.png)