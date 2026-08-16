---
name: gitea-pr
description: Workflow for repositories hosted on the user's Gitea server
---

# Gitea Workflow

The user's Git server is Gitea.

Gitea server:
http://192.168.0.8:3000

Important:
- Do NOT assume the server is Forgejo.
- Do NOT use forgejo.mt-projects.com.
- Do NOT invent or assume a FORGEJO_TOKEN environment variable.
- Do NOT attempt to authenticate through a browser.
- Use the existing Git credentials configured in the environment for Git operations.

Repository workflow:

1. If `/workspace/project` already exists and is a Git repository, inspect it before attempting to clone the repository again.
2. Do not clone a repository again if `/workspace/project` is already the requested repository.
3. Check the current Git remote with `git remote -v`.
4. If the remote points to the user's Gitea server, use it.
5. For protected `master` or `main` branches, never push directly to that branch.
6. Create the feature branch before making the commit.
7. Commit the requested changes to the feature branch.
8. Push the feature branch to Gitea.
9. Create the pull request using the Gitea API.
10. Do NOT open the Gitea web UI to create a pull request.
11. Do NOT navigate to `/pulls/new`.
12. Do NOT attempt browser login for pull request creation.
13. Do not spend time looking for browser credentials when Git credentials are already available.
14. After creating the pull request, report its number and URL.

For an existing repository, the preferred workflow is:

git status
git remote -v
git branch --show-current
git fetch
create feature branch if necessary
make changes
git add
git commit
git push
create PR through Gitea API

CRITICAL:
Never invent changes for the purpose of creating a pull request.
If the user asks to create a pull request but does not specify changes, inspect the repository for existing user changes first.
If there are no user-requested changes and no uncommitted changes or commits that need to be submitted, DO NOT create or modify any files.
Do NOT create README.md, CHANGELOG.md, documentation, tests, comments, formatting changes, or any other artificial changes just to make the pull request possible.
In this situation, stop and ask the user what changes should be included in the pull request.
A pull request is a mechanism for submitting actual requested changes. It is not a task to generate arbitrary changes merely to produce a pull request.

# CRITICAL PR RULE
Never create a pull request merely because the user asked "create a pull request".
Before creating a PR, determine exactly which changes the user wants included.
If the user has not specified any changes:
- Do not create or modify any files.
- Do not create a feature branch.
- Do not reuse an existing feature branch.
- Do not reuse an existing pull request.
- Do not create documentation, README files, CHANGELOG files, tests, comments, or any other changes.
- Do not use changes from previous agent sessions.
- Do not assume that an existing branch contains changes requested by the current user.
- Ask the user what changes should be included in the pull request.
An existing branch is NOT evidence that its changes belong to the current task.
An existing pull request is NOT evidence that it should be reused.
Only changes explicitly requested by the current user, or changes already made by the user during the current task, may be included in the pull request.

# EXISTING BRANCHES
Before using any existing feature branch, determine whether it was created as part of the current task.
Never automatically reuse branches such as update-documentation, feature/*, fix/*, etc.
If the branch was created by a previous task or previous agent session, do not use it for the current PR.
If there are no current-task changes, stop and ask the user what should be changed.
