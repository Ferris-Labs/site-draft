---
title: "Creating Projects and Linking with GIT"
linkTitle: "Project and Source Code Management"
weight: 201
description: >-
    Managing your project.
---

Before you begin creating your services it is best to create a Project and link a GIT Repository to the project. Since
Ferris uses a GitOps approach this will ensure you can deploy and iterate your code faster.

Follow the steps described below to create your first project and link it to a GIT Repository.

## Create a New Project

1. Click on `Projects` in the left side menu to open drop-down and then on `List Projects`
2. Click on `+Add` to create a new project

{{< blocks/screenshot color="white" image="/images/create_project_git_int.png">}}

3. Name the project
4. Save the new project

{{< blocks/screenshot color="white" image="/images/git_int_created_project.png">}}

## View Project Details

1. Click on the `Magnifying Glass Icon` to open the details page of the project

{{< blocks/screenshot color="white" image="/images/loupe_git_created_project.png">}}

{{< blocks/screenshot color="white" image="/images/git_project_details_page.png">}}

## Add a GitHub Repository to the Project

1. Click on the `Git Repositories Tab`
2. Click on `+Add` to add a SSH repository URL

{{< blocks/screenshot color="white" image="/images/add_git_repo.png">}}

## Copy GitHub Repo

*Note that before adding your GitHub Repository to the platform, a public SSH key needs to be generated.*

1. Login to your GitHub account
2. Go to the Repository you want to add to the project, in this use case `ferris-packages`
3. Click on the `Green Code Button` to display the repository URLs
4. Copy the SSH URL

{{< blocks/screenshot color="white" image="/images/github_copy_ssh_url.png">}}

## Paste SSH URL

1. Paste the copied SSH URL from your repo
2. Click `Save` to set up the repository on the platform
3. When you click `Save` a pop-up will display a platform generated public key. This Key must be added to the GitHub
   Repo in order to allow for syncing the code running on the Platform.

{{< blocks/screenshot color="white" image="/images/create_git_repo.png">}}

*Note that a pair of public and private keys are generated for each repository which is set up on the FerrisFX platform.
The private key is encrypted and stored safely in the database and will never be presented to anyone, whereas the public
key should be copied and added to the git repository in order to provide the FerrisFX access to the repository and the
possibility to clone packages.*

{{< blocks/screenshot color="white" image="/images/public_key_repo.png">}}

## Add the Public Key to GitHub

1. Return to your GitHub account
2. Click on `Settings` in the top menu bar
3. Click on `Deploy Keys`
4. Click on `Add Deploy Key`

{{< blocks/screenshot color="white" image="/images/add_public_key_git.png">}}

5. Paste the generated public key
6. Name the public key
7. Click on `Add Key`

{{< blocks/screenshot color="white" image="/images/save_public_key_git.png">}}

8. Check the saved public key

{{< blocks/screenshot color="white" image="/images/check_saved_key_git.png">}}

## Synchronise the Repository

1. Return to the FerrisFX platform
2. Click the Sync Now button to synchronise the platform with the Git Repository.

{{< blocks/screenshot color="white" image="/images/sync_now_button.png">}}

3. Check the synchronised details page

*Note that the branches (main; dev) were added and the status has changed (synced).*

{{< blocks/screenshot color="white" image="/images/synced_repos.png">}}

Tha main branch is syncronized by default. As you continue developing your project and have multiple branches these can
also be synced separately.

4. Click on the `List Services` tab to verify that the packages were imported

{{< blocks/screenshot color="white" image="/images/list_services_git_import.png">}}

## Change Git Branch on the Platform

*If a user wants to test or work on a specific branch, he can select the branch required to do so. The main branch is
selected by default.*

1. Click on the edit button to open the `Edit Repository` details page

{{< blocks/screenshot color="white" image="/images/edit_repo_branch.png">}}

2. Click in the drop-down to select the branch, in thise case "dev"
3. Click on `Save` to save the selected branch

{{< blocks/screenshot color="white" image="/images/save_branch.png">}}

4. Click on Sync to synchronise the packages from the dev branch

{{< blocks/screenshot color="white" image="/images/sync_dev_branch.png">}}

5. Click on the `List Services` tab to verify the packages have been synced from the dev branch

{{< blocks/screenshot color="white" image="/images/list_services_dev.png">}}

*Note that a public key can be regenerated at any moment if in doubt that someone has access to it. If a new key gets
generated, it needs to get added to GitHub again and synced on the platform afterwards. If the step of adding the key is
missed, the synchronisation will fail. Keys can also be deleted directly on GitHub if the platform access shouldn't be
granted anymore.*