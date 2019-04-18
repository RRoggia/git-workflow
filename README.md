# git-workflow

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

[!Centralized version control system](https://git-scm.com/book/en/v2/images/centralized.png)

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

[!Distributed version control system](https://git-scm.com/book/en/v2/images/distributed.png)

#### Example: Git
1. User A creates a git repository(node) in its local machine
2. User A starts to adding files and modifying files
3. User B clones the git repository(node) from User A and places it in its local machine
4. User B has access to all the changes User A did. And he/she can start to change the source code that will only impact its node.
5. User B pushes his changes to the User A git repository
6. User A reviews and accepts the changes from User B



    


 