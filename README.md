# Add Issue Link
A GitHub Action for [Linking a pull request to an issue](https://help.github.com/en/enterprise/2.17/user/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue).

## :arrow_forward: Usage
this action add texts like this into the head of your Pull Request description when it is opened.

```
# Issue
- Resolve #2
```

- Result example
![Linking a pull request to an issue](readmeImages/pull-request.png)

### Create a workflow

Add `.github/workflows/issue-reference.yml` with the following:

```yml
name: 'Issue Link'
on:
  pull_request:
    types: [opened]

jobs:
  issue-link:
    runs-on: ubuntu-latest
    steps:
      - uses: tkt-actions/add-issue-links@v1.0.0
        with:
          repo-token: "${{ secrets.GITHUB_TOKEN }}"
          branch-prefix: "issue-"
```

### Set up required parameters
Need to contain the required parameters on the workflow file.

- `repo-token` A token for the repository. Can be passed in using `{{ secrets.GITHUB_TOKEN }}`
- `branch-prefix` A prefix of the branch name for finding a related issue (e.g `issue-`).

### Add a comment contained a link for a related issue
Create a branch based on the pattern of the branch name (`[branch prefix][issue number][you can put any texts]`) set up on `.github/workflows/issue-reference.yml`.

For example, if `branch-prefix` is `issue-`, create a branch like `issue-8_create-action`.

When pushing your changes to the repository and creating a pull request, a workflow runs automatically.

## :memo: Licence
MIT