# xml-authoring-project

A structured directory where we build and store xmls.

This acts as a project template which forms the base for creating an xml-authoring-directory for a particular client.

## Prerequisites

* Git
* PHP
* [Composer installed](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx) globally

## Work with commands

### Install dependencies

For users:

```bash
$ composer install
```
    
Developers may wish to use [`--prefer-source`](https://getcomposer.org/doc/03-cli.md#install) to work on git repositories of dependent components):    

```bash
$ composer install --prefer-source
```
        

* Try example `hello-world` command from `xml-authoring-tools`:

    ```bash
    # Stream some example content into the config file (creating it if it does not exist) 
    $ pwd
    /Users/x/Documents/Projects/XmlAuthoringSuite/xml-authoring-project
    $ cat vendor/xmlsquad/xmlauthor-example-command/XmlAuthoringProjectSettings.yaml.dist >> XmlAuthoringProjectSettings.yaml
    
    # Try
    bin/console hello-world
    ```

* (optional) Require additional command packages:

    ```bash
    composer require xmlsquad/some-package
    ```
    
    To study/try commands from required packages - see package's `README.md`.
    
## Who needs this anyway?

So, you are a staff member who is responsible for creating and editing a client's Xml files.

We have a client who wants some Xmls authored. We need to set up a folder on your computer that acts as a 'working directory' for the client's Xml project. 

We use Git SCM to track changes to the files within this directory.

Each instance of this [xml-authoring-project](https://github.com/xmlsquad/xml-authoring-project) has a `composer.json` file in the root directory which specifies an ever-increasing set of custom software tools that can speed up your most repetitive tasks.

### Custom software tools

[These tools](https://github.com/xmlsquad/xml-authoring-tools) have been built to work in the context of this xml-authoring-project. 

We will use software tools to:

* to manipulate and query the Xmls files that are stored within this directory; 
* when run inside [Bitbucket Pipelines](https://bitbucket.org/product/features/pipelines), to test and report on the state of the Xml files whenever changes are committed.

We also use custom tools (along with the project's configuration settings) to convert the client's Google Sheets into snippets of Xml that are stored here. 

# Getting started

We assume that you have installed :

* [Git SCM](https://git-scm.com/) 
  * (with [Git LFS](https://www.atlassian.com/git/tutorials/git-lfs) enabled)
* [Composer](https://getcomposer.org/doc/00-intro.md) (installed globally)

## Navigate to your `Projects` directory

* On your workstation, open MacOs Terminal or Windows Git Bash
* Navigate to the folder on your computer where you keep Xml authoring projects. 
```
$ cd /Users/Bob/Documents/Projects/XmlAuthoring
```

Given a client, we may or may not already have their working directory set up as a git repository in the cloud.

### Using an existing working directory.


* Determine the location of the "origin" Git repository for that client's working directory (ask the account manager).
* Run `git clone` to get a local copy of the client's working directory
* Use `cd` to change into the working directory.


Now, you should be able to work on the Xml files.

Once your edits are finished, use `git` to [commit your changes](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) to the `origin`.

### Set up a new xml authoring project working directory for a client

We create a new git repository (based on this [xml-authoring-project](https://github.com/xmlsquad/xml-authoring-project)), alter the remotes then push it to our git hosting solution. Effectively, we [fork it](https://help.github.com/articles/fork-a-repo/).

* Ensure the client has an empty "origin" Git repository created for them (ask the client's account manager).
* Run `git clone` to get a local copy of https://github.com/xmlsquad/xml-authoring-project 
* Use `cd` to change into the working directory.
* Use `git remote set-url` command set the `origin` to the client's repository. ie. 
```
$ git remote set-url origin git@github.com:path/to/git/repo.git
```
Query the setting to ensure it worked:
```
$ git remote -v
origin	git@github.com:path/to/git/repo.git (fetch)
origin	git@github.com:path/to/git/repo.git (push)
```
* `git push` to push the base project up to the client's `origin` repository.

## Ensure the tools are installed

* Run `composer install` to ensure that all the tools are installed.

Now, you should be able to work on the Xml files.

Once your edits are finished, use `git` to commit your changes to the `origin`.

## Configure the tools

As the end user, you will need to add some configuration files to the root of the project:

### Connecting to GSuite

NOTE: At the time of writing we have [2 sub-projects that are connecting to GSuite](https://github.com/xmlsquad?tab=repositories). Each project's developer has been given freedom to solve the issue of Google API authentication as they need. In the next few hours, I will look at all solutions and pick one to be the definitive method.

In the mean time, you could copy the pattern used by another devloper to determine where your credential files will be stored.

Check the project's dev branches and pull requests. The one's that connect to GSuite are: 

* [gsheet-to-xml](https://github.com/xmlsquad/gsheet-to-xml) - Given the url of a Google Sheet, this Symfony Console command fetches the Google Sheet and outputs it in the form of Xml.
* [ping-drive](https://github.com/xmlsquad/ping-drive) - Symfony Console command that reports its attempts at locating and reading the contents of a Google Drive folder or file.

A third sub project is being built called:
* [capture-lookups](https://github.com/xmlsquad/capture-lookups) - A Symfony 3.4 Console command. When given configuration file listing URLs of Google Sheets, grabs them and stores them locally as CSV files.

We have a library for shared code at:
* [xml-authoring-library](https://github.com/xmlsquad/xml-authoring-library)

### XmlAuthoringProjectSettings.yaml

One instance of an xml-authoring-project is created for each of our company's clients. This configuration file is used to store client-wide configurations like the location of the client's key files and folders on GSuite. 

# Using the tools

See: https://github.com/xmlsquad/xml-authoring-tools

# Keeping the tools updated

The custom tools are always improving. 

To update to the latest versions of the tools.

* First ensure all changes to client files are committed and pushed to the repository
* In the command terminal, navigate to the root of the client working directory and run `composer update`

## Development Notes

### Composer validation notice is OK

The team [uses a trick](https://github.com/xmlsquad/xml-authoring-project/issues/2#issuecomment-394185484) to check dependencies. This trick leaves a validation warning when the project's `composer.json` file is checked by `composer validate`.

```bash
$ pwd
/Users/x/Documents/Projects/XmlAuthoring/xml-authoring-project
$ composer validate
./composer.json is valid for simple usage with composer but has
strict errors that make it unable to be published as a package:
See https://getcomposer.org/doc/04-schema.md for details on the schema
The property repositories-local is not defined and the definition does not allow additional properties
```

So, although it might look painful. It is harmless. So, we ignore it. We will remove it once the project is more settled.
