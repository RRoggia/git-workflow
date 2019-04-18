# git-workflow
This repository contains the content to be shared at the GS Tech counsil workshop.

Agenda:
* [Version Control System](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#version-control-system)
    * [Centralized](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#centralized-version-control-system)
    * [Distributed](https://github.wdf.sap.corp/GS-Tech-Council/git-workflow#distributed-version-control-system)
    * Comparing Centralized and Distributed


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


    


 
