---
title: "Project and Code Structure"
linkTitle: "Project and Code Structure"
weight: 202
description: >-
    Structure and Artefacts of a Service
---

The following section provides a better understanding of the various artefacts of a service.

## Understanding Projects

Within the DX Platform the Project is a collection of Services. Projects do not have a functional role they are
primarily to help in organising collections of services either because they are related functionally, or serve a
specific solution domain or are accessed by a sepcific group of users.

A project may be linked to multiple git repositories. With each repository consiting of a number of services.

## Repository Structure

The DX platform considers each directory within a Repository as a distinct service. Any files in the root directory of a
Repository are ignored.

## Service Artefacts

A service is a collection of scripts, modules and assets such as additional configuration files.

The following are the types of supported artefacts and their roles.

| Artefact Type              | Description                                                                                                                                                                                                                                    |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *.py                       | Python scripts. A service may consist of any number of python scripts. If there are multiple scripts they are run in the sequence defined in the `manifest.json`file. Python scripts which define classes and static methods may also be used. |
| *.sql                      | A file containing SQL statements which will be executed against the default DB defined in the platform. The .sql files also support 'jinja' like notation which can be used to extract parmeter or embed program logic within the .sql file    |
| manifest.json              | The `manifest.json`file helps describe the service to the platform as well as other users. It follows a pre-defined structure. It is describe in detail in the section `Manifest File`.                                                        |
| config.json                | A JSON file which defines the service configuration. These are stored within consul once they are imported into the platform. The configuration values can be retrieved by using the 'context' of the service using the ferris_ef module.      |
| secrets.json               | A file which defines the secrets accessible within a specific service.                                                                                                                                                                         |
| *.txt, *.json, *.jinja etc | Assests used by the Service.                                                                                                                                                                                                                   |

## Structuring Packages Within The GIT Repository

Each directory within the git repo is considered a package by FX. As there is no way to control the sequence of script
execution within the repository based backages please ensure that your scripts either do not require a specific run
sequence or ensure that only a single script needs to be called ( other functionality can be called from teh entry point
script)

The configurations are loaded from the config.json file. If secrets.json file exists in the git repo then it will be
loaded and discarded ( but will remain in the GIT Repository)