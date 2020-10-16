---
layout: components
title: Console
tab: components
---

[![Source](https://img.shields.io/badge/Source-simpl--php%2Fconsole-blue)](https://github.com/simpl-php/console)

# Simpl/Console

> Boilerplate for creating a new console project using `symfony/console`.

## Installation

```
composer create-project simpl/console [your-project-name] --stability=dev
```

## Basic Usage

### Command Help
```bash
php console help app:hello
```

### Run the hello command.
```bash
php console app:hello
```

### Run the hello command with optional `name` parameter
```bash
php console app:hello --name="Josh"
```

## Adding your own commands.
You can add new commands by adding a class that extends `Symfony\Component\Console\Command\Command` to the `app\Commands` directory.

Once you've added your command, register it in the `console` script.

```php
// ... register commands
$application->add(new Commands\Hello());
```

> See `app\Commands\Hello` for an example.