---
name: gitea-pr
description: Efficient workflow for creating pull requests in Gitea repositories
---

# Gitea Pull Requests

When working with a repository hosted on Gitea:

- If the target branch is protected, never attempt to push directly to it.
- Create the feature branch before committing changes.
- Commit the changes to the feature branch.
- Push the feature branch to the remote repository.
- Create the pull request directly using the Gitea API.
- Do not open the Gitea web UI to create a pull request.
- Do not navigate to `/pulls/new`.
- Do not attempt browser login for pull request creation.
- Do not spend time inspecting the pull request web page before creating it.
- Use the existing authentication available to the agent.
- Only use the browser UI as a fallback if the Gitea API method fails.
- After creating the pull request, verify that it was created successfully and report its number and URL.

Preferred workflow:

1. Check git status and current branch.
2. Determine the target branch.
3. Create a feature branch if the target branch is protected.
4. Make and commit the requested changes.
5. Push the feature branch.
6. Create the pull request through the Gitea API.
7. Report the pull request URL and number.

