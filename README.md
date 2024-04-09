
<div align="center">
  <a href="https://github.com/descope/project-cicd-template">
    <img src="https://github.com/descope/project-cicd-template/blob/main/.github/images/descope-logo.png" alt="Descope Logo" width="128" height="128">
  </a>

  <h3 align="center">Descope CI/CD Template</h3>

  <p align="center">
    A template repo for managing your Descope project using snapshots
  </p>
</div>

<br />

## About

This template repository provides a working example of how to use the snapshot export and import features to deploy changes to your production Descope project.

You can use this repo to:

* Keep a source controlled copy of your project settings and configurations
* Use a workflow to export snapshots from a staging project and create a pull request
* Code review changes in pull requests before they are approved and merged
* Automatically deploy changes after pull requests are merged to import them into your production project
* Customize the workflows as you see fit

<br />

## Getting Started

You can press the [Use this template](https://github.com/new?owner=descope&template_name=project-cicd-template&template_owner=descope) button to create a copy of this repository for use with your Descope project in your own GitHub account. You can of course also clone or fork the repo.

### Prerequisites

If you're already using Descope you'll need some information from the [Descope console](https://app.descope.com), otherwise you can [start using Descope](https://www.descope.com/sign-up) in less than a minute.

1. You'll need a Descope project and its `Project ID`, which you can find in the [Project page](https://app.descope.com/settings/project) in the Descope console.
2. The instructions below assume you have another Descope project, and they'll be referred to as the `staging` and `production` projects.
3. You'll also need to generate a management key in the [Company page](https://app.descope.com/settings/company/managementkeys).

<div align="center">
  <img src="https://github.com/descope/project-cicd-template/blob/main/.github/images/readme-project.png" alt="Project details" width="500">
</div>

### Configuration

The workflows need a Descope management key so they can call the snapshot export and import APIs. They also need to know which Descope projects they're working with. The easiest way to do this is to set these values as secrets and variables in our GitHub repository.

1. In your repo's `Settings` page, go to `Secrets and variables` and add a repository secret called `MANAGEMENT_KEY` with the value of the key created above.
- Optional: Suppose you have restricted the management key access to your production project, creating a management key within the Descope console that only has access to the production project. In that case, you can also add `PROD_MANAGEMENT_KEY` as a secret. If `PROD_MANAGEMENT_KEY` is configured, it will be used for production actions, and `MANAGEMENT_KEY` will be used for staging actions
2. Switch to the `Variables` tab.
3. Create a repository variable called `PRODUCTION_PROJECT_ID` variable and set it to the `Project ID` of your `production` Descope project.
4. Do the same thing with a `STAGING_PROJECT_ID` variable and set it to the `Project ID` of your `staging` Descope project.

<br />
<img src="https://github.com/descope/project-cicd-template/blob/main/.github/images/readme-secrets.png" alt="Secrets panel">
<br />
<img src="https://github.com/descope/project-cicd-template/blob/main/.github/images/readme-variables.png" alt="Variables panel">
<br />

### Permissions

The workflows need to be allowed to create pull requests and update the repository.

1. In your repo's `Settings` page, go to `Actions` and select `General` on the side panel.
2. Scroll to the `Workflow permissions` section.
3. Make sure the `Read and write permissions` option is selected.
4. Make sure the `Allow GitHub Actions to create and approve pull requests` option is checked.

<div align="center">
  <img src="https://github.com/descope/project-cicd-template/blob/main/.github/images/readme-permissions.png" alt="Pull request" width="500">
</div>
<br />

## Usage

At first, the repository will be empty. We'll want to get the current of the Descope project into the repository.

1. Go to the `Actions` page in your repo.
2. Select the `Create Pull Request from Staging Project` workflow.
3. Press the `Run workflow` button and confirm.
4. After a short while a new Pull Request will be created.
5. You can confirm that the added files contain your `staging` project's settings and configurations.
6. Approve and merge the Pull Request to trigger an automatic deployment into your `production` project.

You should now see a `ProjectSnapshot` folder in the repo with files representing all the settings and configurations of your project. Note that the path where the files are stored can be customized in the workflow files.

<div align="center">
  <img src="https://github.com/descope/project-cicd-template/blob/main/.github/images/readme-snapshot.png" alt="Pull request" width="500">
</div>
<br />

You can now try to introduce a small change to your `staging` project by going to the Descope console and changing a setting. After that you can repeate the steps above and observe that the diff in the created Pull Request reflects the change that you made.

<div align="center">
  <img src="https://github.com/descope/project-cicd-template/blob/main/.github/images/readme-pullreq.png" alt="Pull request" width="500">
</div>
<br />
