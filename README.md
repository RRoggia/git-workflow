# git-workflow
This repository contains the content to be shared at the GS Tech counsil workshop.

Agenda:
* [Version Control System](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#version-control-system)
	* [Centralized](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#centralized-version-control-system)
	* [Distributed](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#distributed-version-control-system)
	* [Comparing Centralized and Distributed](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#cvcs-x-dvcs)
* [Git Workflows](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#git-workflows)
	* [Git Basics](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#git-basics)
	* [Centralized](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#centralized)
	* [Feature branch](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#feature-branch)
	* [Forking](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#forking)
	* [Gitflow](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#gitflow)
		* [Branches](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#branches)


# Version Control System
* **What is it?** Revision control system that ensures archiving, versioning, security and tracking of changes.
* **Why do we need that?** It's a [requirement for the Software Lifecycle product standard](https://wiki.wdf.sap.corp/wiki/display/pssl/SLC-25). To ensure that the source code is available for development and maintenance, that access is restricted to authorized persons, and that SAP knows what was changed in which version and by whom (named person)

Between the SAP's allowed version control systems (VCS). We can categorize then in two categories: Centralized (CVCS) and Distributed (DVCS).

## Centralized version control system
* A single server does the source code version control. This server is the source of truth.
* You must get data from the server. 
* Usually only one person can edit the source code at time. The server has a locking mechanism in place.
* You only have access to the latest version of a file. Not only the full history.
* If server is down, no one is able to collaborate.
* Damages to the server, (and without proper backup) might result to data loss

The image below depicts a centralized version control system.
![Centralized version control system](https://git-scm.com/book/en/v2/images/centralized.png)

#### Example: ABAP Repository
1. User goes to the SE38 transaction
2. User edits the report
3. File is locked for that user do their changes. Other users cannot edit the same report
4. User will only have the latest version of the file

## Distributed version control system
* There is no concept of server, it is actually replaced by several nodes. Each and every node does its own source code version control. There is no source of truth.
* You can get the data from any node.
* Each node is independent, it enables multiple person editing the same files at same time.
* Each node will have the whole history of the source code. Not only the latest version. 
* If a node is down, the others nodes will keep working.
* Damages to the one node, can be backed up by others nodes. Might still result to data loss, but in a minor scale.

The image below depicts a distributed version control system.
![Distributed version control system](https://git-scm.com/book/en/v2/images/distributed.png)

#### Example: Git
1. User A creates a git repository(node) in its local machine
2. User A starts to adding files and modifying files
3. User B clones the git repository(node) from User A and places it in its local machine
4. User B has access to all the changes User A did. And he/she can start to change the source code that will only impact its node.
5. User B pushes his changes to the User A git repository
6. User A reviews and accepts the changes from User B

## CVCS x DVCS
| Behavior                      | Centralized           | Distributed                         |
| ----------------------------- | --------------------- | ----------------------------------- |
| Source of truth               | Yes, the server       | No, several nodes                   |
| Share data between nodes      | No, only the server   | Yes, nodes share data between them  |
| Simultaneous changes to file  | No, server lock files | Yes, has its own source code        |
| Full history of files changes | No, only latest       | Yes, each node has its own history  |
| Synchronization               | No,                   | Yes, nodes requires synchronization |

Based on the table above we can conclude that, **a DVCS is more powerful and flexible than CVCS**. But it's also **more complex** because it requires synchronization between nodes.

Having a **well stablished workflow** for sharing data between repositories **reduces the problems and complexity** usually found in DVCS.

# Git Workflows
Because git is a very flexible tool it enables several types of workflows. The most common are: centralized, Feature Branch and the Gitflow. Before we deep dive in each of these workflows lets just recap some of the git basic concepts.

## Git Basics
* Git repository: a project directory that is under version control. The `.git` folder contains all the files required to manage the version of your source code. You can create a repository by running `git init` or you can clone an existing repository by running `git clone`. 
* Commit: A picture of what all your files look like at that moment and stores a reference to that snapshot.
* Branch: A simply lightweight movable pointer to one of the commits of the repository.
* Remote Branch: A reference (pointer) to a branch in a remote repositories.

## Centralized
One central repository, can accept code, and everyone synchronizes their work with it. There is only one branch called `master` all the changes goes to this branch.

If two developers `clone` from the repository and both make changes, the first developer to push their changes back up can do so with no problems. The second developer must `merge` in the first one's work before pushing changes up, so as not to overwrite the first developer's changes.

![Centralized workflow](https://git-scm.com/book/en/v2/images/centralized_workflow.png)

The centralized approach is simple and practical and works fine for very small teams, but because it only has one branch it has the following problems:
* branch has no protection against broken code
* any broken code pushed to the remote will impact all the nodes synchronized
* development cycle must stop, in order to begin another cicle (release cicle, maintenance cicle)
* non final code must be removed from master branch before release
* code review is not ensured by the workflow

#### Example:
1. Fork this repository.
2. Clone it to your local machine.
3. Use `git log` to compare the remote history, with your local repository history.
4. In your local repository, change the description of the 1st step of this example and `commit` it.
5. Execute the 4th step to the remote repository.
6. Try to push the changes in your local repository to the remote repository. You can use `git push origin master`.

## Forking
Another usage of git that doesn't requires branches is the forking workflow. Each developer forks the "oficial repository", which means each developer will have their own public repository with the same history. The developer then does the required changes and apply it to their fork repository (changing the history). Once the changes are done and available in the developer fork repository, the maintainer of the "oficial repository" can pull the changes if it he/she thinks it fits the repository needs.

![Forking workflow](https://git-scm.com/book/en/v2/images/integration-manager.png)

The main advantage of this approach, is that a developer doesn't need to wait for the "official repository" maintainer to approve their changes. It can keep working with its public repository until the changes are accepted.

## Feature Branch
All feature development should take place in a dedicated branch instead of the `master` branch. These branches are called, `feature`branches and are short-lived branches that you create and use for a single particular feature or related work. In addition, is also common to have one or two long-lived branches that represent a different stage of the development cycle. Once the `feature` branch is finished it's merged into one of the long-lived branch and deleted.

The previous example of two developers applying changes to the same file and having synchronization problems occurs less frequently, since the development is now isolated in branches. It's important to try to make these branches small and short-lived

![Feature Branch workflow](https://git-scm.com/book/en/v2/images/lr-branches-2.png)

The main advantages of the feature branch are:
* Multiple developers working on the same code base but in different branches and without impacting the main code base
* Enables pull requests and code reviews as part of the development process
* Isolation of the development cycle from the other cycles of the project
* Eases and foster the collaboration of code 

Notice although the feature branch workflow adds a lots of advantages, by not knowing when to close, synchronize or split a feature branch, the developer may face several synchronization problems. It also requires more knowledge about the git and its functionalities. Another point to consider, is that the feature branch workflow, doesn't determine when a branch should be merged which leaves space to broken code or unfinished code to be pushed to the long-lived branches. 

#### Example:
1. Fork this repository.
2. Clone it to your local machine.
3. In your local machine. Use the `git branch feature-branch` command to create a branch named feature-branch.
4. Apply changes in the first step of this example and `commit`.
5. Push the `feature-branch` branch to the remote using `git push origin feature-branch`.
6. Check your fork in the remote, and look for your branch.
7. Create a Pull Request to the `master` branch.  
8. Repeat the steps 2, 3, 4, 5 and 6. But create a branch with a different name.

## Gitflow
Gitflow Workflow assigns very specific roles to different branches and defines how and when they should interact. In addition to feature branches, it uses individual branches for preparing, maintaining, and recording releases.

It originated from a [blog post](https://nvie.com/posts/a-successful-git-branching-model/) written in 2010 by Vicent Driessen. This blog post describes how they managed to achieve a successful git workflow.

The gitflow works similarly to the feature branch workflow, the main diference it has very well defined states and available iteractions of each branch. 

### Branches
There are two categories of branches in gitflow: main branches and supporting branches.

#### Main Branches
Gitflow determines two main branches with infinite lifetime:

* `master`: Reflects production ready state
* `develop`: Developments ready for the next release (a.k.a integration branch)

**A new commit to develop represents a new feature is stable and ready for the next release.**

**A new commit to master represents a new production release.**

#### Supporting Branches


The pricture below demonstrate how branches interact with git flow.
![Branches workflow](https://github.wdf.sap.corp/raw/tax-service/txs-core-pipeline-library/dev/docs/_static/Gitflow-Branches.png)

The  full workflow.
![Gitflow](https://nvie.com/img/git-model@2x.png)

## References
* [Atlassian Git workflow comparsion](https://br.atlassian.com/git/tutorials/comparing-workflows)
* [Git Pro book - branching workflow](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows)
* [Git Pro book - Distributed Git](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows)
* [Tax Service implementation of gitflow](https://github.wdf.sap.corp/tax-service/txs-core-pipeline-library)


 
