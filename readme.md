# Mayank API generator
> Yeoman generator for creating API's using MongoDB/Sequelize (Mysql, Postgres, sqlite), Express, and Node - lets you quickly set up a project following best practices.

#### Generated project:

## Usage

Install `yo`, `grunt-cli`, and `expressjs-api`:
```
<<<<<<< HEAD
npm install -g yo grunt-cli expressjs-api
=======
npm install -g yo grunt-cli generator-expressjs-api
>>>>>>> bda044f54c4946528f251fdca0a1bea89d0248d2

```

Make a new directory, and `cd` into it:
```
mkdir my-new-project && cd $_
```

Run `yo expressjs-api`, optionally passing an app name:
```
yo expressjs-api [app-name]
```

Run `grunt` for building, `grunt serve` for preview, and `grunt serve:dist` for a preview of the built app.

## Prerequisites

* MongoDB - Download and Install [MongoDB](http://www.mongodb.org/downloads) - If you plan on scaffolding your project with mongoose, you'll need mongoDB to be installed and have the `mongod` process running.

## Supported Configurations

**General**

* Build Systems: `Grunt`, `Gulp` (Coming Soon)
* Testing:
  * `Jasmine`
  * `Mocha + Chai + Sinon`
    * Chai assertions:
      * `Expect`
      * `Should`

**Server**

* Scripts: `Babel`
* Database:
  * `None`,
  * `MongoDB`, `SQL`
    * Sequelize (SQL) Table Options: `Timestamps`, `Paranoid`, `Pluralized Names`  
    * Authentication boilerplate: `Yes`, `No`
    * oAuth integrations: `Facebook` `Twitter` `Google`
    * Socket.io integration: `Yes`, `No`

## Generators

Available generators:

* App
    - [expressjs-api](#app) (aka [expressjs-api:app](#app))
* Server Side
    - [expressjs-api:endpoint](#endpoint)
* Deployment
    - [expressjs-api:openshift](#openshift)
    - [expressjs-api:heroku](#heroku)

### App
Sets up a new ExpressJS API Boilerplate with best practices

Usage:
```bash
Usage:
  yo expressjs-api:app [options] [<name>]

Options:
  -h,   --help          # Print the generator's options and usage
        --skip-cache    # Do not remember prompt answers                        Default: false
        --skip-install  # Do not install dependencies                           Default: false
        --app-suffix    # Allow a custom suffix to be added to the module name  Default: App

Arguments:
  name    Type: String  Required: false
```

Example:
```bash
yo expressjs-api
```

### Endpoint
Generates a new API endpoint.

Usage:
```bash
Usage:
  yo expressjs-api:endpoint [options] <name>

Options:
  -h,   --help               # Print the generator's options and usage
        --skip-cache         # Do not remember prompt answers           Default: false
        --route              # URL for the endpoint
        --models             # Specify which model(s) to use
        --endpointDirectory  # Parent directory for enpoints

Arguments:
  name    Type: String  Required: true
```

Example:
```bash
yo expressjs-api:endpoint message
[?] What will the url of your endpoint be? /api/messages
```

Produces:

    server/api/message/index.js
    server/api/message/index.spec.js
    server/api/message/message.controller.js
    server/api/message/message.integration.js
    server/api/message/message.model.js  (optional)
    server/api/message/message.events.js (optional)
    server/api/message/message.socket.js (optional)

###Openshift

Deploying to OpenShift can be done in just a few steps:

    yo expressjs-api:openshift

A live application URL will be available in the output.

> **oAuth**
>
> If you're using any oAuth strategies, you must set environment variables for your selected oAuth. For example, if we're using Facebook oAuth we would do this :
>
>     rhc set-env FACEBOOK_ID=id -a my-openshift-app
>     rhc set-env FACEBOOK_SECRET=secret -a my-openshift-app
>
> You will also need to set `DOMAIN` environment variable:
>
>     rhc set-env DOMAIN=<your-openshift-app-name>.rhcloud.com
>
>     # or (if you're using it):
>
>     rhc set-env DOMAIN=<your-custom-domain>
>
> After you've set the required environment variables, restart the server:
>
>     rhc app-restart -a my-openshift-app

To make your deployment process easier consider using [grunt-build-control](https://github.com/robwierzbowski/grunt-build-control).

**Pushing Updates**

    grunt

Commit and push the resulting build, located in your dist folder:

    grunt buildcontrol:openshift

### Heroku

Deploying to heroku only takes a few steps.

    yo expressjs-api:heroku

To work with your new heroku app using the command line, you will need to run any `heroku` commands from the `dist` folder.


If you're using mongoDB you will need to add a database to your app:

    heroku addons:create mongolab

Your app should now be live. To view it run `heroku open`.

>
> If you're using any oAuth strategies, you must set environment variables for your selected oAuth. For example, if we're using **Facebook** oAuth we would do this :
>
>     heroku config:set FACEBOOK_ID=id
>     heroku config:set FACEBOOK_SECRET=secret
>
> You will also need to set `DOMAIN` environment variable:
>
>     heroku config:set DOMAIN=<your-heroku-app-name>.herokuapp.com
>
>     # or (if you're using it):
>
>     heroku config:set DOMAIN=<your-custom-domain>
>

To make your deployment process easier consider using [grunt-build-control](https://github.com/robwierzbowski/grunt-build-control).

#### Pushing Updates

    grunt

Commit and push the resulting build, located in your dist folder:

    grunt buildcontrol:heroku

## Configuration
Yeoman generated projects can be further tweaked according to your needs by modifying project files appropriately.

A `.yo-rc` file is generated for helping you copy configuration across projects, and to allow you to keep track of your settings. You can change this as you see fit.

## Testing

Running `grunt test` will run the client and server unit tests with karma and mocha.

Use `grunt test:server` to only run server tests.

**Protractor tests**

To setup protractor e2e tests, you must first run

`npm run update-webdriver`

Use `grunt test:e2e` to have protractor go through tests located in the `e2e` folder.

**Code Coverage**

Use `grunt test:coverage` to run mocha-istanbul and generate code coverage reports.

`coverage/server` will be populated with `e2e` and `unit` folders containing the `lcov` reports.

The coverage taget has 3 available options:
- `test:coverage:unit` generate server unit test coverage
- `test:coverage:e2e` generate server e2e test coverage
- `test:coverage:check` combine the coverage reports and check against predefined thresholds

* *when no option is given `test:coverage` runs all options in the above order*

**Debugging**

Use `grunt serve:debug` for a more debugging-friendly environment.

## Environment Variables

Keeping your app secrets and other sensitive information in source control isn't a good idea. To have grunt launch your app with specific environment variables, add them to the git ignored environment config file: `server/config/local.env.js`.

## Project Structure

Overview

    └── server
        ├── api                 - Our apps server api
        ├── auth                - For handling authentication with different auth strategies
        ├── components          - Our reusable or app-wide components
        ├── config              - Where we do the bulk of our apps configuration
        │   └── local.env.js    - Keep our environment variables out of source control
        │   └── environment     - Configuration specific to the node environment

An example server component in `server/api`

    thing
    ├── index.js                - Routes
    ├── thing.controller.js     - Controller for our `thing` endpoint
    ├── thing.model.js          - Database model
    ├── thing.socket.js         - Register socket events
    └── thing.spec.js           - Test

