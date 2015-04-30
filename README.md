# Drupal 8 starter project with Docker and composer

It uses the [Composer template](https://github.com/drupal-composer/drupal-project).

## Usage

First you need to [install composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

> Note: The instructions below refer to the [global composer installation](https://getcomposer.org/doc/00-intro.md#globally).
You might need to replace `composer` with `php composer.phar` (or similar) for your setup.

After that you can create the project:

```
composer create-project drupal-composer/drupal-project:8.x-dev some-dir --stability dev --no-interaction
```

With `composer require ...` you can download new dependencies to your installation.

```
cd some-dir
composer require drupal/devel:8.*
```

Copy the [.gitignore](https://github.com/louisbl/drupal8-starter/blob/master/.gitignore).

Copy and adapt the [docker-compose.yml](https://github.com/louisbl/drupal8-starter/blob/master/docker-compose.yml) in your project.

Copy the [nginx configuration](https://github.com/louisbl/drupal8-starter/blob/master/docker/nginx/default.conf) in `docker/nginx`.

Make an `html` link to the web folder :
```
ln -s web html
```

Start the servers:
```
docker-compose up
```

* Varnish is on [localhost:8017](http://localhost:8017)
* Nginx is on [localhost:8016](http://localhost:8016)
* Adminer is on [localhost:8015](http:"//localhost:8015)

To run `drush` commands use:
```
docker-compose run --rm drush <CMD>
```
The `drush` container is linked with nginx and mysql already.

## What does the template do?

When installing the given `composer.json` some tasks are taken care of:

* Drupal will be installed in the `web`-directory.
* Autoloader is implemented to use the generated composer autoloader in `vendor/autoload.php`,
  instead of the one provided by Drupal (`web/vendor/autoload.php`).
* Modules (packages of type `drupal-module`) will be placed in `web/modules/contrib/`
* Theme (packages of type `drupal-module`) will be placed in `web/themes/contrib/`
* Profiles (packages of type `drupal-profile`) will be placed in `web/profiles/contrib/`
* Creates default writable versions of `settings.php` and `services.yml`.
* Creates `sites/default/files`-directory.
* Latest version of drush is installed locally for use at `vendor/bin/drush`.


## Generate composer.json from existing project

With using [the "Composer Generate" drush extension](https://www.drupal.org/project/composer_generate)
you can now generate a basic `composer.json` file from an existing project. Note
that the generated `composer.json` might differ from this project's file.


## FAQ

### Should I commit the contrib modules I download

Composer recommends **no**. They provide [argumentation against but also workrounds if a project decides to do it anyway](https://getcomposer.org/doc/faqs/should-i-commit-the-dependencies-in-my-vendor-directory.md).
