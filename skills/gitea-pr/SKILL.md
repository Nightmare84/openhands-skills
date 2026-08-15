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
