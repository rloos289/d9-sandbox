# Docksal powered Drupal 9 With Composer Installation

This is a sample Drupal 9 with Composer installation pre-configured for use with Docksal.

Features:

- Drupal 9 Composer Project
- `fin init` [example](.docksal/commands/init)
- Using the [default](.docksal/docksal.env#L9) Docksal LAMP stack with [image version pinning](.docksal/docksal.env#L13-L15)
- PHP and MySQL settings overrides [examples](.docksal/etc)

## Setup instructions

### Step #1: Docksal environment setup

**This is a one time setup - skip this if you already have a working Docksal environment.**

Follow [Docksal environment setup instructions (MacOS with Docker Desktop)](https://docs.docksal.io/getting-started/setup/#install-macos-docker-for-mac)
### Step #2: Project setup

1. Clone this repo into your Projects directory

    ```
    git clone git@github.com:rloos289/d9-sandbox.git
    cd d9-sandbox
    ```

2. Initialize the site

    This will initialize local settings and install the site via drush

    ```
    fin init
    ```

3. Point your browser to

    ```
    http://d9-sandbox.docksal
    ```

When the automated install is complete the command line output will display the admin username and password.

After running `fin init` you will have a full D9 instance ready to go with the following things.
- Basic configuration files from the standard profile installed and configured.
- Settings.php and development.services.yml configured for local dev work.
- Composer set up to allow for Drupal patches.
- Composer set with different sections for dev and regular dependencies.
- The admin toolbar module installed and configured as an example of a contrib module.
- An empty custom module installed and configured as an example of custom modules.

## Custom Commands

- fin sequelpro - Open this site's database in sequel pro (requires a local version of sequelpro `brew install --cask sequel-pro`)
- fin uli - Generate a one-time user login link for Drupal
- fin init - Starts site initialization and runs `fin site-init` (you should only have to run this once)
- fin site-init - Installs and configures the site (don't run this directly)
- fin phpcs - Validates all of the PHP in web/modules/custom to the Drupal standard
- fin phpcs-clean-up - Fixes everything marked by `fin phpcs` that can be fixed automatically
- fin remindme - Prints helpful docker terms and links to the terminal.
- fin test - Test the site installation.

## More automation with 'fin init'

Site provisioning can be automated using `fin init`, which calls the shell script in [.docksal/commands/init](.docksal/commands/init).
This script is meant to be modified per project. The one in this repo will give you a good starting example.

Some common tasks that can be handled by the init script (an other [custom commands](https://docs.docksal.io/fin/custom-commands/)):

- initialize local settings files for Docker Compose, Drupal, Behat, etc.
- import DB or perform a site install
- compile Sass
- run DB updates, revert features, clear caches, etc.
- enable/disable modules, update variables values
## Security notice

This repo is intended for quick start demos and includes a hardcoded value for `hash_salt` in `settings.php`.
If you are basing your project code base on this repo, make sure you regenerate and update the `hash_salt` value.
A new value can be generated with `drush ev '$hash = Drupal\Component\Utility\Crypt::randomBytesBase64(55); print $hash . "\n";'`
