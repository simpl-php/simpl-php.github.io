---
layout: components
title: Csv
tab: components
---

[![Source](https://img.shields.io/badge/Source-simpl--php%2Fcsv-blue)](https://github.com/simpl-php/csv)
[![Build Status](https://img.shields.io/travis/simpl-php/csv)](https://travis-ci.org/simpl-php/csv)

# simpl/csv

Reading delimited files... the Simpl way!

Why should you use this? `fgetcsv()` is already pretty good, right?

Yes, `fgetcsv()` is pretty good, and this package uses it under the hood - with some quality of life improvements.

The main benefits of this package are:

- Easy to set number of records to skip (like headings)
- You can give it an array of column headings and it will return the parsed row as an associative array.
    - This means you get to work with array keys you define instead of having to remember the numerical position.
- This provides some basic transformations out of the box.
    - Automatically trim all values.
    - Automatically convert empty strings to `null`.
- If you provide column headings, it will compare the number of column headings to the number of columns it
parsed from each row and throw an exception if your data is missing a column.

## Installation

```bash
composer require simpl/csv
```

## Basic Usage
```php
<?php
$csv = Reader::createFromFile('/path/to/your/file.csv');
$csv->setColumns(['name', 'address', 'phone']);
$csv->setSkipRows(1);

while($row = $csv->read())
{
    print_r($row['address']);
}
```
