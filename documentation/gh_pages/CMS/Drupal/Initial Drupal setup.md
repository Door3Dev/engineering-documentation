---
title: 1. Initial Drupal setup using Docksal
template: third-level-navigation.html
---

### Step 1: Install Docksal

Before you begin, make sure you have Docker installed on your machine.
Once Docker is installed, you can proceed to install Docksal using the following commands:

```shell
curl -fsSL https://get.docksal.io | sh
```
This command downloads and installs the Docksal CLI on your system.
After installation, you should have access to the ```fin``` command, which is used to interact with Docksal.

### Step 2: Install and run a Drupal Project

Now that Docksal is installed, let's create a new Drupal project.
Navigate to the directory where you want to set up your project and run the following command:

```shell
fin project create
```
Or use it's shorthand alias: ```fin p create```

This command will launch a wizard in which you can select which type of CMS you need to install and run.

It should look something like this:
```shell
1. Name your project (lowercase alphanumeric, underscore, and hyphen): test-project

2. What would you like to install?
  PHP based
    1.  Drupal 10 (Composer Version)
    2.  Drupal 10 (BLT Version)
    3.  Drupal 9 (Composer Version)
    4.  Drupal 9 (BLT Version)
    5.  Drupal 7
    6.  Wordpress
    7.  Magento
    8. Laravel
    9. Symfony Skeleton
    10. Symfony WebApp
    11. Grav CMS
    12. Backdrop CMS

  Go based
    13. Hugo

  JS based
    14. Gatsby JS
    15. Angular

  HTML
    16. Static HTML site

  Custom
    0. Custom git repository

```

This wizard will automatically download and build selected CMS into Docksal container. 

Installing Drupal 10 (Composer Version) should result in next output:
```shell
[success] Installation complete.  User name: admin  User password: XXXXXXXXX
Open http://test-drupal-10.docksal in your browser to verify the setup.
Look for admin login credentials in the output above.
```

### Step 3: Install and run a Drupal Project
Congratulations! Your new Drupal project is installed and ready for further work.

To run / stop / restart project using Docksal `Fin` CLI tool navigate to project folder and use following commands:

```shell
fin p start 
fin p stop
fin p restart
```

### Additional information and lilnks:
- Docksal installation and documentation https://docksal.io
