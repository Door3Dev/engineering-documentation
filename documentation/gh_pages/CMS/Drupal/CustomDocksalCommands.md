---
title: 3. Creating custom Docksal commands
template: third-level-navigation.html
---

Drupal development workflow often requires to move DB or `files` folder between environments, usually to our local.

Now that we created our [Drush aliases](RemoteDrushExecutionOnAWS.md)
Let's set up custom Docksal commands to simplify this process.

There are already some commands available in `.docksal/commands` folder after we completed [Initial Drupal setup.md](Initial%20Drupal%20setup.md).
These are simply shell scripts that can be executed using `fin command-name`, where `command-name` is the name of the file.
For example: `fin pull-db`.

Below are the most common commands:

Pull DB from Dev to local (filename: `pull-db`):
```shell
#!/usr/bin/env bash
set -e
set -x

fin drush sql-sync @dev @local --structure-tables-list="cache*" -y
fin drush cim -y
fin drush cr
```

Pull Files from Dev to local (filename: `pull-files`):
```shell
#!/usr/bin/env bash
set -e
set -x

fin drush rsync @dev:%files @local:%files -y
```

Push DB from local to Dev (filename: `push-db`):
```shell
#!/usr/bin/env bash
set -e
set -x

fin drush sql-sync @local @dev --structure-tables-list="cache*" -y
fin drush @dev cim -y
fin drush @dev cr


```

Push Files from local to Dev (filename: `push-files`):
```shell
#!/usr/bin/env bash
set -e
set -x

fin drush rsync @local:%files @dev:%files -y
```

And so on and so forth.

### Additional information and links:
- Docksal custom commands https://docs.docksal.io/fin/custom-commands/
