# Generate Release Tag

A GitHub Action to create a new Git tag, generate release notes, and create a GitHub release.

## Overview

This action automates the process of tagging a release, generating release notes, and creating a GitHub release. It helps streamline the release management process by handling these tasks within a GitHub Actions workflow.

## Features

- **Create a new Git tag** with a specified tag number.
- **Generate release notes** based on the new tag and the previous tag.
- **Create a GitHub release** using the generated notes.

## Inputs

### `release-tag-number`

- **Description**: The tag number for the new release.
- **Required**: `true`
- **Default**: `v1.0.0`

### `user-email`

- **Description**: The email address used for Git configuration.
- **Required**: `true`

### `user-name`

- **Description**: The name used for Git configuration.
- **Required**: `true`

### `github-token`

- **Description**: A GitHub token used for authentication and authorization.
- **Required**: `true`

## Usage

To use this action in your workflow, you need to define a job in your `.github/workflows` file. Here’s an example of how to set it up:

```yaml
name: Create and Release Tag

on:
  workflow_dispatch:
    inputs:
      release-tag-number:
        description: 'Enter the release-tag number'
        required: true

jobs:
  create-tag:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      deployments: write

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Generate Release Tag
        uses: mokhlesurr031/github-manual-release@v2.0.2
        with:
          release-tag-number: ${{ github.event.inputs.release-tag-number }}
          user-email: ${{ secrets.USER_EMAIL }}
          user-name: ${{ secrets.USER_NAME }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Example

For a practical example, assume you want to create a new release tag `v1.2.3` and generate release notes for it. You would trigger the workflow with the `release-tag-number` input set to `v1.2.3`.

## Notes

- Ensure that you have set up the `USER_EMAIL` and `USER_NAME` secrets in your repository settings for this action to work correctly. You don't need to set `GITHUB_TOKEN` manually cause it is there by default github configurations.
- This action assumes you are using the `main` branch for tagging and release creation.

## Contributing

If you would like to contribute to this action, please open an issue or a pull request on the [repository](https://github.com/mokhlesurr031/github-manual-release).

---

Feel free to customize the README to better fit your needs or to reflect any additional features or instructions specific to your action.



## Github Repository
And this repo contains the test of this action => [Test Repo for Github Manual Release](https://github.com/mokhlesurr031/test-github-manual-release)
