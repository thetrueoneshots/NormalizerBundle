Bowl Of Soup Normalizer
=====

[![Build Status](https://travis-ci.org/BowlOfSoup/NormalizerBundle.svg?branch=master)](https://travis-ci.org/BowlOfSoup/NormalizerBundle)
[![codecov](https://codecov.io/gh/BowlOfSoup/NormalizerBundle/branch/master/graph/badge.svg?token=2OW4EWvMUD)](https://codecov.io/gh/BowlOfSoup/NormalizerBundle)
[![PHP Version](https://img.shields.io/badge/php-7.2.x%20--%208.2.x-blue.svg)](https://www.php.net/)
[![Symfony Version](https://img.shields.io/badge/symfony-5.4.x-blue.svg)](https://symfony.com/)

Installation
-----
    composer require bowlofsoup/normalizer-bundle

Add the bundle to your `config/bundles.php` file

    BowlOfSoup\NormalizerBundle\BowlOfSoupNormalizerBundle::class => ['all' => true],

Quick feature overview
-----
- It's a Symfony bundle!
- Normalizes class properties and methods (public, protected, private)
- Can Serialize normalized content
- Works with Symfony and Doctrine as its ORM. Can handle Doctrine proxies
- Circular reference check: Handles circular reference by detecting it and returning content of the objects getId() method
- Object caching: If a getId() method is implemented for an object it will cache the normalized object per normalize command
- Annotation caching, this means speed!
    - The annotations for an object are cached. This means not parsing annotations multiple times for the same object. per flow (per normalize command)
    - In Symfony prod mode, annotations are cached completely (after first run)
- Symfony translations
    - Indicate domain (translation filename) and locale in annotations
    - Does not support formatting with ICU MessageFormat (yet), so no parameters

The main features are described in the [documentation](https://github.com/BowlOfSoup/NormalizerBundle/wiki).

Documentation
-----
Documentation on the usage and all supported options can be found [in the wiki](https://github.com/BowlOfSoup/NormalizerBundle/wiki).

1. [What is serialization and normalization?](https://github.com/BowlOfSoup/NormalizerBundle/wiki/What-is-serialization-and-normalization%3F)
2. [Installation](https://github.com/BowlOfSoup/NormalizerBundle/wiki/Installation)
3. [Serializing](https://github.com/BowlOfSoup/NormalizerBundle/wiki/Serializing)
    1. [Serialize annotations](https://github.com/BowlOfSoup/NormalizerBundle/wiki/Serialize-annotations)
4. [Normalizing](https://github.com/BowlOfSoup/NormalizerBundle/wiki/Normalizing)
    1. [Normalize annotations](https://github.com/BowlOfSoup/NormalizerBundle/wiki/Normalize-annotations)
5. [Translate a value](https://github.com/BowlOfSoup/NormalizerBundle/wiki/Translate-a-value)
    1. [Translate annotations](https://github.com/BowlOfSoup/NormalizerBundle/wiki/Translate-annotations)

Why use this normalizer and not ...
-----
- The Bowl Of Soup Normalizer uses an opt-in mechanism by default. You have to indicate which properties must be normalized
- You can indicate a context group, how is the value to be normalized, in which context?
- It's designed with speed in mind. Not packed with features for which you don't use half of it
- It has proven itself in a complex application with 15.000+ daily end users

Development
-----
The following CI tools can be used to check for code quality before pushing code:

### Rector
Rector can be used to automated code upgrades and refactoring. Try a dry-run first!
```bash
vendor/bin/rector process --dry-run --no-progress-bar --ansi
```

### PHPStan
PHPStan is a static code analysis tool that focuses on finding errors in the code.
Fixing the outcome of PHPStan prevents possible bugs and errors.
```bash
vendor/bin/phpstan
```

### PHPUnit
Speaks for itself, code should be tested. Run with coverage (output = tests/coverage):
```bash
XDEBUG_MODE=coverage php -dzend_extension=xdebug.so vendor/bin/phpunit 
```
Or without coverage:
```bash
vendor/bin/phpunit
```

**Code coverage** `master`:

<img src="https://codecov.io/gh/BowlOfSoup/NormalizerBundle/branch/master/graphs/sunburst.svg?token=2OW4EWvMUD" width="200">

### Code style fixer
Have php-cs-fixer automatically fix styling.
```bash
vendor/bin/php-cs-fixer fix
```