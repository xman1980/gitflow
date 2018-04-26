This document describes the version control system configuration. The main aims are:

* Frequent releases (up to every day)
* Capability for manual and automated testing
* An easy process of releasing the code


Task Management
-------------------

* Task management and tracking is being done with YouTrack.
* Every task has a unique identifier that is used in the description of every COMMIT.
* A separate branch is created for every unique task ID.



Permanent Branches
------------------

* There are two branches that are permanent: `master` and `development`.
* `master` branch contains a stable and tested code. This branch’s code is always ready for a deployment to a Production.
* `development` branch contains a code ready for testing.
* It is not allowed to commit directly into `development` and `master` branches. All commits should be made into the `feature-branches`.


Branch naming
------------------------------

* For every task there is a separate branch. All work related to this task (including bug fixing) is performed inside that branch.
* Naming convention for such branches:


### `<type>/<name>`

#### `<type>`
```
bug       - Code changes linked to a known issue.
feature   - New feature.
hotfix    - Quick fixes to the codebase.
junk      - Experiments (will never be merged).
```

#### `<name>`
Should contain numeric ID of task,
always use dashes to seperate words, and keep it short.

#### Examples
```
feature/3433-short-summary
hotfix/4353-dockerfile-base-image
bug/1234-login-ie
```
* Feature-branches branch off of `master`. This is important as the code in the `development` branch may not be tested yet and still have critical bugs.
* For features/hotfixes/bugs testing use QA environment, all correct named branches will be automatically deployed to it.
* You can manually reset QA environment to `development` branch after testing.
* When the work on a task is finalized, the feature-branch is merged into the `development`, and the new version is then deployed to the development environment.
* In case there is an additional work to be done on a task all the changes are done right in the same feature-branch. It is then being merged into the `development`. No changes are allowed directly in the development as they will not get into the master branch.
* After a task is ready and tested the feature-branch is ready to be merged into the `master` for releasing.


Commits
-------

* A commit description should contain an ID of a task, which it relates to.
* The ID of a task should be preceded with the ‘#’ (without apostrophes) — that is for systems to understand the relation (the Bitbucket may create a link to the related issue).
* An example of a commit description: #84 changed something to something.


Releasing
-----

* The release will contain all the completed AND tested tasks (marked as ‘Done’). (Note: if a task is marked as ‘Resolved’ it has not been tested yet.)
* If a task has a dependency on another task (DEPENDS ON), it will not get into the release..
* All the branches eligible for the release are merged into the `master`, then the `master` is deployed to the Production.
* A new version of the `master` branch may need to be merged into into the feature-branches being not Done to allow fewer conflicts in the future.


