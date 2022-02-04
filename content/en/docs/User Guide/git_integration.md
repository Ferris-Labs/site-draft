---
title: "GitHub Integration"
linkTitle: "GitHub Integration"
weight: -10
description: >-
  How to integrate a GitHub Repository with the Ferris Platform.
---

The GitHub Integration is the capability to generate a connection from a git repository with projects and synchronise the Packages from the Executor with the git repository, with the goal to execute it through the FerrisFX Platform. It provides another, more fluent way for connecting scripts with the FerrisFX Platform without the necessity to upload files directly to the platform.

A new Project will be created to showcase the capabilty of the git integration:

#### Create a new project

1. Click on Projects in the left side menu to open drop-down and then on List Projects
2. Click on +Add to create a new project

![](/images/create_project_git_int.png)

3. Name the project
4. Save

![](/images/git_int_created_project.png)

#### Check the created project

1. Click on the magnifying glass to open the details page of the project

![](/images/loupe_git_created_project.png)

![](/images/git_project_details_page.png)

#### Add a GitHub Repository to the created project

1. Click on Git Repositories
2. Click on +Add 

![](/images/add_git_repo.png)

#### Copy GitHub Repo

*Note that before adding your GitHub Repository to the platform, a public SSH key needs to be generated.*

1. Login to your GitHub account
2. Go to the Repository you want to add to the project, in this use case "ferris-packages"
3. Click on the the green Code button to showcase the repository URLs
4. Copy the SSH URL

![](/images/github_copy_ssh_url.png)

#### Paste SSH URL

1. Paste the copied SSH URL from your repo
2. Click save to create the repository on the platform

![](/images/create_git_repo.png)

*Note that a pair of  public and private keys are generated for each repository which is safed on the FerrisFX platform. The private key is encrypted and stored safely in the database and will never be presented to anyone, whereas the public key should be copied and added to the git repository in order to provide the FerrisFX access to the repository and the possibility to clone packages.*

![](/images/public_key_repo.png)

#### Add the public key to GitHub

1. Return to your GitHub account
2. Click on Settings in the top menu bar
3. Click on deploy keys
4. Click on Add deploy key

![](/images/add_public_key_git.png)

5. Paste the generated public key
6. Name the public key
7. Click on Add key 

![](/images/save_public_key_git.png)

8. Check the saved public key

![](/images/check_saved_key_git.png)

#### Synchronise the repository

1. Return to the FerrisFX platform
2. Click the Sync Now button to synchronise the platform with the GitHub

![](/images/sync_now_button.png)

3. Check the synchronised details page

*Note that the branches were added and the status has changed.*

![](/images/synced_repos.png)
