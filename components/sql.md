---
layout: components
title: SQL
tab: components
---

[![Source](https://img.shields.io/badge/Source-simpl--php%2Fsql-blue)](https://github.com/simpl-php/sql)
[![Build Status](https://img.shields.io/travis/simpl-php/sql)](https://travis-ci.org/simpl-php/sql)

# simpl/sql
A dead-simple layer on top of PDO to make PDO setup and querying simpler

## Installation

```bash
composer require simpl/sql
```

This component makes it easy to make and execute SQL statements with PDO.

You can run parameterized queries in a single step instead of doing separate prepare and execute statements.

This will automatically convert your query to a prepared statement with parameterized queries to prevent nasty SQL injection attacks.

## Examples

### Connecting to the database.
```php
$db = new \Simpl\SQL('localhost', 'your-db-name', 'your-username', 'your-password');
```


### Running a SELECT query with parameters.
```php

$res = $db->query('select * from test where foo = ? or bar = ?', [$foo, $bar]);
```

> Since this is just a wrapper around PDO, you'll get back a `\PDOStatement` object you can then operate on as you normally would.

### Running a DELETE statement.
```php
$count = $db->exec('delete from test where id = ?', $id);
```

### Running an UPDATE statement.
```php
$count = $db->exec('update test set foo = ? where id = ?', [$foo, $id]);
```

> For both UPDATES and DELETES, `exec()` will return the number of affected rows.

### Running an INSERT statement.
```php
$id = $db->insert('insert into test (foo, bar) values (?,?)', [$foo, $bar]);
```

> For INSERT statements, `insert()` will return the last inserted id.


