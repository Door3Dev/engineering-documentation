---
title: 2. Setting up Drush aliases to execute commands on remote AWS instances
template: third-level-navigation.html
---

Drush CLI tool is essential for Drupal development, thus it's very convenient to have ability execute its commands on remote instance.
Thankfully Drush supports so-called aliases for this very purpose.
Below is the guide how to set up aliases for AWS Bitnami environments and to use them with Docksal.

### Step 1: Create drush configuration file

In the project root (alongside with `.docksal` and `composer.json`) create `drush/sites/self.site.yml` file.

Configuration should look something like this:

```yaml
local: # Alias for local environment, necessary for DB and Files download from remote
  paths:
    drush: /usr/local/bin
    site: sites/default/
    files: sites/default/files
  root: /var/www/web
  uri: 'http://project-name.docksal'

qa: # Environment name
  host: XXX.XXX.XXX.XXX # Environment SSH IP address
  options:
    command-specific:
      sql-sync:
        sanitize: true
        no-ordered-dump: true
        structure-tables:
          common:
            - cache
            - cache_filter
            - cache_menu
            - cache_page
            - history
            - sessions
            - watchdog
      rsync:
        mode: rlptzO
        verbose: true
        no-perms: true
    source-command-specific:
      sql-sync:
        no-cache: true
        structure-tables-key: common
  paths:
    dump-dir: /tmp
    site: sites/default/
    files: /bitnami/drupal/sites/default/files
  root: /opt/bitnami/project-name/web
  uri: 'https://qa.project-name.com/' # Environment URL
  user: bitnami
```

### Step 2: Setting up remote SSH keys for Drush
Drush executes commands using SSH, so in order for it to connect we need to tell Docksal to load additional keys into CLI container.
To do that we need to create  `.docksal/docksal-local.env` file. 

In there we specify as many ssh key files as we need for any environment. 
```dotenv
SECRET_SSH_KEY_DEV='private_ssh_key_file_for_dev'
SECRET_SSH_KEY_QA='private_ssh_key_file_for_qa'
SECRET_SSH_KEY_XXXX='private_ssh_key_file_for_xxxx'
```
Format should be as follows `SECTER_SSH_KEY_XXXX` = `name_of_private_ssh_key_file` where XXXX is the server identifier.

Private ssh key files should be copied to `~/.ssh` folder on local machine. 
Docksal will automatically pull key files into CLI container so Drush can use them to connect to remote.

Don't forget to restart Docksal containers using `fin p restart` command for changes to take effect.

To use alias and execute Drush command on remote, use this format:

`fin drush @alias cache:rebuild` for cache rebuild operation.
Where `@alias` is the environment name specified in `drush/sites/self.site.yml` described above.

Examples:

`fin drush @qa cr` will run remote Drush on QA environment to rebuild Drupal cache. 
`fin drush @dev ssh` will open remote SSH session on dev server.

### Additional information and links:
- Drush site aliases <https://www.drush.org/12.x/site-aliases/>
