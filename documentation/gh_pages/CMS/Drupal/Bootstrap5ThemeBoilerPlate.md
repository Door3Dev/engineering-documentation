---
title: 2.1 Bootstrap 5 Theme Boilerplate
template: third-level-navigation.html
---

This article describes how to install base Boostrap5 theme and create subtheme for development.

### Step 1: Install Bootstrap 5 theme using composer

In project root (where `composer.json` and `composer.lock` files are located) run:

```shell
fin composer require 'drupal/bootstrap5:^3.0'
```
### Install theme and create subtheme

1. In `Appearance` section in admin area of the website find newly downloaded Bootstrap5 theme and click `Install`
2. After installation go to Boostrap5 theme settings and scroll down to the Subtheme section
3. Leave location as is `themes/custom`
4. Populate in `Subtheme name` and `Subtheme machine name`
5. Hit `Create`

### Preparing subtheme for development

Our newly created subtheme should now be enabled in `Appearance` and set as Default.

Subtheme files are now located in `themes/custom/[machinename]`

Since we will be using scss, we need to create `NPM` script and install necessary node_modules.
But first let's make sure that we won't get those into our git repository.

Locate `.gitignore` file in project root (alongside with `composer.json`) and add lines to it:
```gitignore
# Ignore custom theme build artifacts
web/themes/custom/*/node_modules
web/themes/custom/*/css
```
Now we can create and populate our `package.json` file in our subtheme as such:

```json
{
  "name": "custom_theme",
  "description": "Bootstrap 5 subtheme.",
  "author": "DOOR3",
  "private": true,
  "version": "1.0.0",
  "scripts": {
    "css:compile": "node-sass --source-map-root file://${PWD}/ --source-map-embed true --importer node_modules/node-sass-magic-importer/dist/cli.js scss/style.scss -o css ",
    "css:prefix": "postcss --use autoprefixer -b '> 10%' css/*.css -r",
    "scss:lint": "npx stylelint scss/*.scss --mw 5 && npx stylelint scss/**/*.scss --mw 5 && npx stylelint scss/**/**/*.scss --mw 5",
    "scss:lint:fix": "npx stylelint scss/*.scss --fix && npx stylelint scss/**/*.scss --fix && npx stylelint scss/**/**/*.scss --fix",
    "watch": "nodemon -e scss -x \"npm run css:compile\" --ignore dist -L",
    "build": "npm run scss:lint && npm run css:compile && npm run css:prefix"
  },
  "dependencies": {
    "autoprefixer": "^10.4.13",
    "node-sass": "^7.0.3",
    "node-sass-magic-importer": "^5.2.0",
    "nodemon": "^2.0.20",
    "postcss": "^8.2.4",
    "postcss-cli": "^8.3.1"
  },
  "devDependencies": {
    "stylelint": "^13.9.0",
    "stylelint-config-recess-order": "^2.3.0",
    "stylelint-config-sass-guidelines": "^7.1.0",
    "stylelint-config-standard": "^20.0.0",
    "stylelint-scss": "^3.18.0"
  }
}

```

Now we can run our NPM scripts. There are 2 options, run locally (local `Node.JS` and `NPM` installs are required) or run inside Docksal container.

Run locally (see `scripts` section in `package.json`):

```shell
npm install 
npm run [script_name] 
```

Run inside Docksal container:

```shell
fin exec npm install 
fin exec npm run [script_name] 
```


### Additional information and links:
- Bootstrap5 theme <https://www.drupal.org/project/bootstrap5>
