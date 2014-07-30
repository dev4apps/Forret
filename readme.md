## Forret: L4 Foundation
Demo of [Admin Panel](http://forret.io/admin/login)
  * username = admin@forret.io | password = password

Demo of [User Frontend](http://forret.io/)

### Overview
The purpose of this application is to provide a starting point for development where the code provided can be copy/pasted and used as an example for future expansion (ie Implementation of a Post object). This demo uses [Laravel 4](https://github.com/laravel/laravel/tree/develop) at its core and [Sentry 2](https://github.com/cartalyst/sentry) for user authentication and roles. The code is seperated into three different "modules", consisting of a User frontend, and an Admin backend. Both of which make internal API calls. The API is built on [Dingo/Api](https://github.com/dingo/api). The admin panel has been built with [AdminLTE](https://github.com/almasaeed2010/AdminLTE). The HTML and views for [Metronic](http://themeforest.net/item/metronic-responsive-admin-dashboard-template/4021469?WT.ac=category_item&WT.z_author=keenthemes) can be provided upon request however the assets will not be as those need to be acquired through ThemeForrest.

### Features
 1. HMVC-esque: This application is split into different modules
  * Api
     * all urls are prefixed with `/api` for example `www.forret.dev/api/users`
     * The api layer is the only module that communicates with the database. 
     * Also where validation occurs.
     * All responses (success or errors) are generated by Dingo/Api
  * Admin
     * Makes internal Api calls to do everything from log a user in, to gathering the requested data to display
     * Users must have the necessary roles to access any admin url
  * Frontend
     * Can be accessed by non authenticated users as well as users with only the `Users` role.
 2. Folder/File Structure **None of the following should be taken as "Best Practice". This is simply how I feel I get the most clean and organized code**
   * *Controllers* - Code dealing with getting data from the user or db, and return data to the user. Filters are also executed in the `__construct` of each controller. Note that the filters for each "module" are contained in the `app\filters\` folder.
    * *Models* - Code dealing with how models relate to each other as well as various db settings
    * *Routes* - No filters here. Only for translating uri->Controller@method. Not that the routes for each "module" are contained in the `app\routes\` folder.
    * *Views* - The views only reference urls. They have no knowledge of routes or route names. They have been heavily broken up to allow for easy editing.
    * *Repositories* - The code that is processing data, or getting data from models, for example `User::find(1)` is placed in the repositories.
    * *Exceptions* - All custom exceptions are placed in the `app\Starter\Exceptions` folder
 3. Validation
  * Validation is done through the Respect/Validation library. 
  * The UserValidator class contains the rules to be executed for various situations that would need validation (Login, Creation, Updating). This class extends the Validator class which contains the code to execute validation.
 4. Logging
    * Every page load and api call is logged to the `actions` table via the `Action` model. If `config\queue.php` is set as `sync` the user will have to wait for these rows to be written. If configured for Iron-io however this logging will be done asynchronously.

### Instructions
This is a Laravel application that is best installed via [Forge](https://forge.laravel.com).  Forge makes dealing with environment variables incredibly easy, see [here](http://mattstauffer.co/blog/laravel-forge-using-environment-variables-for-environment-detection). The below environment variables need to be set
* DB_DATABASE
* DB_HOSTNAME
* DB_USERNAME
* DB_PASSWORD
* API_BUGSNAG (set as blank string if not using bug snag)
* CONF_DEBUG ('true' or 'false' to set debug mode)

### Links
* [Laravel4](https://github.com/laravel/laravel/tree/develop)
* [Sentry2](https://github.com/cartalyst/sentry)
* [Dingo/Api](https://github.com/dingo/api)
* [AdminLTE](https://github.com/almasaeed2010/AdminLTE)
* [Laravel-4-Generators](https://github.com/JeffreyWay/Laravel-4-Generators)
* [Iron-mq](https://github.com/iron-io/iron_mq_php)
* [Faker](https://github.com/fzaninotto/Faker)
* [Laravel-vendor-cleanup](https://github.com/barryvdh/laravel-vendor-cleanup)
* [Laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper)
* [Laravel-debugbar](https://github.com/barryvdh/laravel-debugbar)
* [Bugsnag](https://github.com/bugsnag/bugsnag-php)
* [Respect/Validation](https://github.com/Respect/Validation)

### Tests
1. Many tests have currently been added.

### History
* Forret was originally designed to be a tool for internal use only. Because this became so useful internally, Appit Ventures decided that it would be a good product to make open source and allow the community to utiltize it as well.

### To Do
* Swap out Laravel's auth for Oauth2
* Add try catch statements to frontend
* Catch all exceptions and throw the proper Dingo/API exceptions
* All views for admin panel
* All views for user frontend
* Continue to write acceptance tests for backend API
* Selenium tests for frontend
* Swap out Respect/Validation for either stock Laravel validation or other library

=======
This Starter kit is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)