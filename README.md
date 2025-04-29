# Generate-Changelog-Workflow

## Automated Changelog Generation

This repository contains a GitHub Actions workflow that automatically generates and updates a CHANGELOG.md file based on conventional commits when pull requests are merged into the main branch.

## Overview

The workflow leverages conventional commits and the conventional-changelog-cli tool to create a standardized, readable changelog that documents all significant changes to the codebase.

## How It Works

1. When a pull request is merged into the main branch, the GitHub Actions workflow is triggered.
2. The workflow checks out the repository with full git history.
3. It sets up Node.js and installs the conventional-changelog-cli tool.
4. The workflow generates or updates the CHANGELOG.md file based on the commit history.
5. If changes are detected, it commits the updated changelog file back to the repository.

## Prerequisites

- Your project must use [Conventional Commits](https://www.conventionalcommits.org/) format for commit messages.
- GitHub Actions must be enabled for your repository.
- Your repository must have a branch named `main`.

## Setup Instructions

1. Add the workflow file to your repository:
    - Create a directory: `.github/workflows/`
    - Copy the `generate-changelog.yml` file into this directory

2. Customize the user credentials in the workflow file:
   ```yaml
   git config --local user.email "team@yourcompany.com"
   git config --local user.name "Your Team Name"
   ```

3. Push these changes to your repository.

4. (Optional) Add a badge to your main README.md:
   ```markdown
   ![Changelog](https://github.com/your-org/your-repo/actions/workflows/generate-changelog.yml/badge.svg)
   ```

## Branch Strategy

This workflow is designed for a development process that follows this pattern:

1. Feature branches are created and worked on.
2. Pull requests merge feature branches into a `staging` branch.
3. After testing on the staging branch, another pull request merges `staging` into `main`.
4. The changelog is generated when the PR from `staging` to `main` is merged.

## Configuration Options

The workflow uses the Angular preset for conventional commits by default. You can modify this by changing the preset in the workflow file:

```yaml
conventional-changelog -p [preset] -i CHANGELOG.md -s -r 0
```

Available presets include:
- `angular` (default)
- `atom`
- `codemirror`
- `conventionalcommits`
- `ember`
- `eslint`
- `express`
- `jquery`
- `jshint`

## Limitations

- The workflow only generates changelogs for commits that follow the conventional commits format. Non-conforming commits will not be included.
- The workflow does not automatically bump version numbers in package.json or create git tags (commented code is provided for this option).
- GitHub Actions runners need write permissions to the repository to push the updated changelog.
- If the CHANGELOG.md file is edited manually, these changes might be overwritten when the workflow runs again.

## Troubleshooting

### Workflow Doesn't Run

- Check that your PRs are being merged into the `main` branch.
- Verify that the workflow file is correctly placed in `.github/workflows/`.
- Ensure that GitHub Actions is enabled for your repository.

### Changelog Not Updated

- Verify that your commits follow the conventional commits format.
- Check the GitHub Actions logs for any errors.
- Ensure that the GitHub Actions runner has write permissions to the repository.

### Permission Issues

If you encounter permission issues when pushing changes, consider:

1. Using a GitHub App for authentication
2. Creating a dedicated service account with appropriate permissions
3. Modifying the workflow to create a pull request instead of directly pushing changes

## Contributing

To contribute to this workflow:

1. Create a feature branch from `main`
2. Make your changes
3. Create a pull request to merge your changes into `staging`
4. After testing, create another pull request to merge from `staging` to `main`

## License

This workflow is provided under the [MIT License](LICENSE).

## Additional Resources

- [Conventional Commits Specification](https://www.conventionalcommits.org/)
- [conventional-changelog-cli Documentation](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-cli)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)