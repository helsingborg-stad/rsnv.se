# Municipio Deployment
This repository simplifies the deployment for users of Municpio. Simply fork this repository and setup deployment detials for your hosting environment and deploy whenever it suits you. 

This will enshure that deployments can be made by fetching the upstream of the forked repository without any technical knowledge. Guide on hot to fetch a upstream repo with github user interface can be found here: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork.

## Quick start
1. Fork this repository. Enable github workflows on your newly created repository (gihub disables them due to security reasons on forks).
2. Setup deployment details according to the tables below (source:  https://github.com/helsingborg-stad/municipio-deploy/tree/master/3.0).
3. Update to upstream, whenever you want to update your production enviroment with the latest version of Municipio.

## Adding custom dependencies
You may add your own dependencies in composer.local.json file. This file is automatically read in build. We have made it a separate file, to avoid merge conflicts.
## Multiple forks of the same repository
GitHub has a limitation to one fork of the same repository. This is a inconvenience in this use case, but can be solved by a workaround. You may want to use this, when you have multiple sites to deploy in the same github organization. 

https://handong1587.github.io/linux_study/2015/12/18/create-multi-forks.html 

## Parameters
Add the folowing secrets to your github repository secrets section (https://docs.github.com/en/actions/security-guides/encrypted-secrets). We do recommend that you assign these secrets locally to your repository. You can however use organization level secret to evrything except the path, if you determine that they will persist. 

### Configuration - Production
Used for branch names: production, master

| Secret name                     | Description                                                                  | Required |
|---------------------------------|------------------------------------------------------------------------------|----------|
| DEPLOY_REMOTE_HOST_PROD         | Host domain or ip                                                            | true     |
| DEPLOY_REMOTE_PATH_PROD         | Host deployment path                                                         | true     |
| DEPLOY_REMOTE_BACKUP_DIR_PROD   | Host rsync backup path                                                       | true     |
| DEPLOY_REMOTE_USER_PROD         | Host deploy ssh user name (In sudoers with nopassword enabled)               | true     |
| DEPLOY_KEY_PROD                 | Host deploy ssh user key                                                     | true     |
| WEB_SERVER_USER_PROD            | Host web server user                                                         | true     |
| GITHUB_TOKEN                    | Github token for github npm package usage, use built in secrets.GITHUB_TOKEN | true     |
| ACF URL                         | A url where a zip-file with ACF PRO can be found (ACF provides a url).       | true     |

### Configuration - Stage
Used for branch names: stage, beta, test

| Secret name                     | Description                                                                  | Required |
|---------------------------------|------------------------------------------------------------------------------|----------|
| DEPLOY_REMOTE_HOST_STAGE        | Host domain or ip                                                            | true     |
| DEPLOY_REMOTE_PATH_STAGE        | Host deployment path                                                         | true     |
| DEPLOY_REMOTE_BACKUP_DIR_STAGE  | Host rsync backup path                                                       | true     |
| DEPLOY_REMOTE_USER_STAGE        | Host deploy ssh user name (In sudoers with nopassword enabled)               | true     |
| DEPLOY_KEY_STAGE                | Host deploy ssh user key                                                     | true     |
| WEB_SERVER_USER_STAGE           | Host web server user                                                         | true     |
| GITHUB_TOKEN                    | Github token for github npm package usage, use built in secrets.GITHUB_TOKEN | true     |
| ACF URL                         | A url where a zip-file with ACF PRO can be found (ACF provides a url).       | true     |

## Additional Setup
A fully functional website will not be automatically created when this deployment script has been executed. Some local site configuration has to be created in the a ./config/ folder on the the local machine. This is basically a wp-config.php split in multiple files, for a better overview of the configuration.

All neccesary configuration-example files can be found in the ./config-example folder in this repository. All files ending in -example.php is optional. To use them, simply remove the '-example' extenstion.

The configuration files should be reviewed in full in order to configure the site to your linkings. 

## Contribution
You may contribute to this repository if you feel that anything is missing. Simply send a pull request, and we will review it as soon as possible. 

## Suggested target environment
We do suggest that you include the following softare on the target machine.

- NGINX
- PHP 7.4 or later
- Redis
- Rsync (required for deplyment)