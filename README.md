# gitmoji-auto-label

A simple action to automatically label PRs based on the gitmoji used in the title.

## Usage
```yaml
name: Create gitmoji label
on:
  pull_request:
    types: [opened, edited, reopened, synchronize]
jobs:
  create-gitmoji-label:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    steps:
      - name: Enforce gitmoji PR title
        uses: georgepstaylor/gitmoji-auto-label@v0.0.1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Using the above example verbatim, you can use the job title `gitmoji-pr-title` as a required check.