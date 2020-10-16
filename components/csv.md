---
layout: components
title: Csv
tab: components
---

[![Source](https://img.shields.io/badge/Source-simpl--php%2Fcsv-blue)](https://github.com/simpl-php/csv)
[![Build Status](https://img.shields.io/travis/simpl-php/csv)](https://travis-ci.org/simpl-php/csv)

# simpl/csv

> Reading delimited files... the Simpl way!

## Why should you use this? We already have `fgetcsv()`.

Yes, `fgetcsv()` is great, and this package uses it under the hood - with some quality of life improvements.

The main benefits of this package are:

- Easy to set number of records to skip (like headings)
- You can give it an array of column headings and it will return the parsed row as an associative array.
    - This means you get to work with array keys you define instead of having to remember the numerical position.
- This provides some basic transformations out of the box.
    - Automatically trim all values.
    - Automatically convert empty strings to `null`.
- If you provide column headings, it will compare the number of column headings to the number of columns it
parsed from each row and throw an exception if your data is missing a column.
- Return the full CSV as an array or json object.

## Installation

```bash
composer require simpl/csv
```

## Basic Usage
```php
<?php
use Simpl\Csv\Reader;
$csv = Reader::createFromFile('/path/to/your/file.csv');
$csv->setColumns(['name', 'address', 'phone']);
$csv->setSkipRows(1);

while($row = $csv->read())
{
    print_r($row['address']);
}
```

## It's not just for CSVs

You can use it for any delimited file by calling `setDelimiter()`.

```php
<?php
use Simpl\Csv\Reader;
$csv = Reader::createFromFile('/path/to/your/file.csv');
$csv->setColumns(['name', 'address', 'phone']);
$csv->setDelimiter("\t");
$csv->setSkipRows(1);

while($row = $csv->read())
{
    print_r($row['address']);
}
```

## Other result formats
Don't want to get one row at a time? That's fine. You can get the file as an array or json object. 

```php
use Simpl\Csv\Reader;
$csv = Reader::createFromFile('/path/to/your/file.csv');
$csv->setColumns(['name', 'address', 'phone']);
$csv->setSkipRows(1);
$array = $csv->toArray();
$json = $csv->toJson();
```