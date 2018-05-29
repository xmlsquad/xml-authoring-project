# xml-authoring-directory

A structured directory where we build and store xmls.

## Prerequisites

* Git
* PHP
* [Composer installed](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx) globally

## Work with commands

* Install dependencies

    ```bash
    composer install
    ```

* Try example `hello-world` command from `xml-authoring-tools`:

    ```bash
    # Copy example config
    cp vendor/forikal-uk/xml-authoring-tools/scapesettings.yml.dist ./scapesettings.yml
    
    # Try
    bin/console hello-world
    ```

* (optional) Require additional command packages:

    ```bash
    composer require forikal-uk/some-package
    ```
    
    To study/try commands from required packages - see package's `README.md`.