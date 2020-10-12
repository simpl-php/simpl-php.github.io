---
layout: components
title: Config
tab: components
---

# simpl/config

[![Build Status](https://img.shields.io/travis/simpl-php/config.svg?style=flat-square)](https://travis-ci.org/simpl-php/config)


Simple configuration provider based on [PHP dotenv](https://github.com/vlucas/phpdotenv)

Combines the simplicity of `.env` files with the flexibility of defining arrays of config values.


## Installation

```bash
composer require simpl/config
```

## Setup

For the default installation, the following directory structure is assumed. The `*.php` filenames in this example are contrived. They can be anything you'd like.

```
.env
config/
    app.php
    database.php
    logging.php 
```

## Basic Usage
Define your per-environment configuration in .env files in the root of your project.

```
.env
.env.dev
.env.uat
.env.prod
```

Environment File Example

```
APP_ENV=local
DEBUG=true
```

Load your configuration file.

```php
<?php
use Simpl\Config;
$config = new Config;

$debug = $config->get('DEBUG');
var_dump($debug); // bool(true)
```

If you want more flexibility, you can use `.php` files that return arrays of configuration values. Any `.php` files in the `config` directory will be automatically parsed and loaded into the config object.

```php
<?php
# config/app.php

return [
	'name' => env('APP_NAME', 'Simpl PHP Example'),
	'debug' => env('DEBUG', false),
	'environment' => env('APP_ENV', 'local'),
];
```
>Note: The above example makes use of the `env()` helper function to get a value loaded from your `.env` file.


Then you can access your config values using dot notation. The first segment of the notation will be the name of the file where it was defined. Example, if you defined the key `environment` in `config/app.php`, you would access it's value in the config as `app.environment`.
```php
$environment = $config->get('app.environment');
var_dump($environment); // string(5) "local"
```