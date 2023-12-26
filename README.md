# Logistiko

Toolbox of Github Action reusable workflows.

## All is Github Actions

All in this repository is about Github Actions, and more precisely, it exposes reusable workflows.

To getting started with Github Actions, please, visit :

* The [product launch page](https://github.com/features/actions) ;
* The [developer documentation](https://docs.github.com/fr/actions).

### Free gift

To maintain your Github Actions workflow, you can create, if it's not already done, a `.github/dependabot.yml` and add this content :

```yaml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly" # Check every week, the monday. Can be daily, weekly or monthly
      day: "monday"
      time: "06:00"
      timezone: "Europe/Paris"
    labels:
      - "dependencies:ci"
      - "dependencies:github-actions"
      - "dependencies" # Specify labels to keep organize your Pull Requests
```

Automatically, the bot, called dependabot, will check if some actions, you use in your workflows, can be upgradable and, if it's the case, open a Pull Request with all necessary informations.

More about dependabot features, it's [here](https://docs.github.com/fr/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#about-the-dependabotyml-file).

### Getting started

In order to use these Github Actions reusable workflows, you will need to :

1. Go in your repository settings ;
2. Go to the sections "Actions" > "General" ;
3. Check the "Allow \<YOUR ORG\>, and select non-\<YOUR ORG\>, actions and reusable workflows" ;
4. Add `Nebeto/logistiko/.github/workflows/<WORKFLOW NAME>.yml@main` in the "Allow specified actions and reusable workflows" textarea.

## Reusable worlflows

### security.yml

Scan your code and dependencies about potential vulnerabilities, classified by **low**, **medium**, **high**, or **critical** threats.
Powered by the product [Snyk.io](https://snyk.io).

[![Test security.yml workflow](https://github.com/Nebeto/logistiko/actions/workflows/test-security.yml/badge.svg)](https://github.com/Nebeto/logistiko/actions/workflows/test-security.yml)

#### Integration sample

```yaml
jobs:
  job-1:
    ...
  job-2:
    ...
  security:
    name: Scan my code and dependencies
    uses: Nebeto/logistiko/.github/workflows/security.yml@main
    with:
      working-directory: "frontend-project"
      node-version: "latest"
      scan-mode: "all"
      snyk-project: ${{ vars.SNYK_PROJECT }}
      target: ${{ github.ref_name }}
      severity-threshold: "critical"
      fail-on: "all"
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
      snyk-organization: ${{ secrets.SNYK_ORGANIZATION }}
      snyk-token: ${{ secrets.SNYK_TOKEN }}
```

#### Configuration

* **working-directory** : the directory containing the code sources and dependencies to scan, default to `.`;
* **node-version** : the version of NodeJs used, default to `latest`;
* **scan-mode** : the desired scanning mode, can be `code` (only scan code sources),  `dependencies` (only scan dependencies), or `all`, default to `all` ;
* **snyk-project** : a given name, choose one unique and explicit, **required** ;
* **target** : can be a branch name (like `main`), a tag (like `v1`), default to `main` ;
* **severity-threshold** : the severity threshold, can be `low`, `medium` (includes `low`), `high` (includes `medium`) or `critical` (includes `medium`), default to `critical` ;
* **fail-on** : for `dependencies` scan-mode only, explicit the fail strategy, can be `all`, `upgradable` or `patchable`, default to `all`.

#### Secrets

* **github-token** : the Github token used, can be the default one provided at the execution of your workflow or, as recommended by Github, a custom generated one with at least these rights `TODO`;
* **snyk-organization** : the Snyk organization, can be found from your organization settings > "Organization ID" ;
* **snyk-token** : the Snyk token, can be found from [your personnal account](https://app.snyk.io/account) > "Auth Token".
