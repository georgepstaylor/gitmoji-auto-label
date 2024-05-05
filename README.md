# gitmoji-auto-label

A simple action to automatically label PRs based on the gitmoji used in the title.

Note: GitHub _requires_ more than just the gitmoji in the title, so this action will create the labels
as `<gitmoji>_gitmoji` for example `✨_gitmoji` or `🐛_gitmoji` etc.

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

### Using this action to assist with GitHub automated release notes

_Ensure you set this action job as a required check for your PRs, otherwise PRs could be merged without the correct labels_

Optionally you can use this action in conjunction with [georgepstaylor/gitmoji-release-action](https://github.com/georgepstaylor/gitmoji-release-action) to automatically generate releases and release notes based on the gitmoji labels.

Likewise, you can create releases using the GitHub UI and the release notes will be generated based on the gitmoji labels if you use the following configuration:

See: 
- https://docs.github.com/en/repositories/releasing-projects-on-github/automatically-generated-release-notes
- https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository

```yaml
# .github/release.yml
changelog:
  exclude:
    labels:
      - ignore-for-release
    authors:
      - octocat
  categories:
    - title: Exciting New Features and Enhancements ✨
      labels:
        - ✨_gitmoji
        - ⚡_gitmoji
        - 🚀_gitmoji
        - 🎉_gitmoji
        - 🥚_gitmoji
    - title: Security Fixes 🔒
      labels:
        - 🔒_gitmoji
        - 🛡️_gitmoji
        - 🛂_gitmoji
        - 🔐_gitmoji
    - title: Bug Fixes 🐛
      labels:
        - 🐛_gitmoji
        - 🚑_gitmoji
        - 🩹_gitmoji
    - title: Documentation 📚
      labels:
        - 📚_gitmoji
        - 📝_gitmoji
        - 💡_gitmoji
        - 📄_gitmoji
    - title: Typo Corrections 📝
      labels:
        - 📝_gitmoji
        - 📚_gitmoji
    - title: Breaking Changes 💥
      labels:
        - 💥_gitmoji
    - title: Refactor ♻️
      labels:
        - ♻️_gitmoji
        - ⚰️_gitmoji
        - 🗑️_gitmoji
        - 🚚_gitmoji
    - title: Work In Progress 🚧
      labels:
        - 🚧_gitmoji
        - 🍺_gitmoji
        - 💩_gitmoji
    - title: Dependency Updates 📦
      labels:
        - ➕_gitmoji
        - ➖_gitmoji
        - 📌_gitmoji
        - ⬆️_gitmoji
        - ⬇️_gitmoji
    - title: Other Changes
      labels:
        - "*"

```