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
