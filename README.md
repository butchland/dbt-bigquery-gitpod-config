# dbt-bigquery-gitpod-config
> A gitpod config for using dbt-bigquery in vscode

## Introduction

This repository documents how you can use `dbt` with `BigQuery` in [Gitpod](https://www.gitpod.io/)'s web-based VS Code environment. It leverages the [vscode-dbt-bigquery-power-user](https://marketplace.visualstudio.com/items?itemName=butchland.vscode-dbt-bigquery-power-user) VS Code extension to provide a powerful online coding environment using `dbt` that almost matches a desktop VS Code experience.


## Requirements

* a dbt project using BigQuery that is version controlled in any repo supported by [gitpod](https://gitpod.io/workspaces/) ([Github](https://github.com/), [Gitlab](https://gitlab.com/), [Bitbucket](https://bitbucket.org/))
* a service account file for the bigquery project. _To create a service account file, see the [Creating and Managing service account keys](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) page._
* a [Gitpod account](https://gitpod.io/workspaces/)

_This assumes you already have a git repository account as well as a BigQuery GCP project as well
as an initial dbt project provisioned (dbtCloud account optional). For instructions to setup `dbt` and BigQuery, please see the [dbt setup documentation](https://docs.getdbt.com/tutorial/setting-up)_ 


## Usage

* To start configuring your dbt-bigquery project to run on gitpod, you can install a [Chrome](https://chrome.google.com/webstore/detail/gitpod-always-ready-to-co/dodmmooeoklaejobgleioelladacbeki)/[Brave](https://chrome.google.com/webstore/detail/gitpod-always-ready-to-co/dodmmooeoklaejobgleioelladacbeki)/[Firefox](https://addons.mozilla.org/en-US/firefox/addon/gitpod/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search)
extension called Gitpod that displays a **Gitpod** button on your repo's web page. _As an alternative, you can just open a link [https://gitpod.io/#\<your-repo-url\>](https://gitpod.io/#your-repo-url)._

* Then, in the terminal of the vscode editor, run the following command:
```
curl -s https://raw.githubusercontent.com/butchland/dbt-gitpod-config/main/scripts/loadconfig | bash
```
This will copy over the following files from the `config` directory:
* `.gitpod.yml`
* `gitpod-dbt-profiles.yml`
* `gitpod-vscode-settings.json`
* `requirements.txt`
* `.gitignore` - (optional, will only copy if it doesn't exist yet)

This assumes of course, that you haven't configured your gitpod configuration file `.gitpod.yml` in your project yet.

_If you have an existing `.gitpod.yml` file, rename it temporarily to something else before running the previous `curl` command (make sure to merge the contents of the original `.gitpod.yml` you renamed with the `.gitpod.yml` that was copied over by the `curl` command afterwards)._ 

Then in the **Gitpod Variables** page [gitpod.io/variables](https://gitpod.io/variables), create a new variable named `CREDENTIALS_JSON` with the scope for your `username/<project-name>`. Copy the entire contents of the service account json file into the value field for the variable.

If you already have an existing `.gitignore` file, make sure the following entries are added to it:
* `.credentials`
* `.vscode`
* `venv`

After running script, you should now commit these new files to your version control and push the changes to the remote repository. You can then delete the gitpod workspace and create a new workspace by either clicking the Gitpod button or opening the link [https://gitpod.io/#\<your-repo-url\>](https://gitpod.io/#your-repo-url). 

The new `gitpod.yml` configuration will then update the `.vscode/settings.ini` for vscode's dbt integration and also setup `dbt_profiles.yml` for your bigquery project in the `$HOME/.dbt` folder (which are not persisted across sessions in the gitpod environment).

You can edit these configuration files to further customize your gitpod environment.

If you have issues and suggestions please file an issue in the github issue tab.  