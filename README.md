# Watch changes in the file system using PHP

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/file-system-watcher.svg?style=flat-square)](https://packagist.org/packages/spatie/file-system-watcher)
[![Tests](https://github.com/spatie/file-system-watcher/actions/workflows/run-tests.yml/badge.svg)](https://github.com/spatie/file-system-watcher/actions/workflows/run-tests.yml)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/spatie/file-system-watcher/Check%20&%20fix%20styling?label=code%20style)](https://github.com/spatie/file-system-watcher/actions?query=workflow%3A"Check+%26+fix+styling"+branch%3Amaster)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/file-system-watcher.svg?style=flat-square)](https://packagist.org/packages/spatie/file-system-watcher)

This package allows you to react to all kinds of changes in the file system. 

Here's how you can run code when a new file gets added.

```php
 (new Watcher())
    ->paths($directory, $anotherDirectory)
    ->onFileCreated(function (string $newFilePath) {
        // do something...
    })
    ->watch();
```

## Support us

[<img src="https://github-ads.s3.eu-central-1.amazonaws.com/file-system-watcher.jpg?t=1" width="419px" />](https://spatie.be/github-ad-click/file-system-watcher)

We invest a lot of resources into creating [best in class open source packages](https://spatie.be/open-source). You can support us by [buying one of our paid products](https://spatie.be/open-source/support-us).

We highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using. You'll find our address on [our contact page](https://spatie.be/about-us). We publish all received postcards on [our virtual postcard wall](https://spatie.be/open-source/postcards).

## Installation

You can install the package via composer:

```bash
composer require spatie/file-system-watcher
```

In your project, you should have the JavaScript package [`chokidar`](https://github.com/paulmillr/chokidar) installed. You can install it via npm

```bash
npm install chokidar
```

or Yarn

```bash
yarn add chokidar
```

## Usage

Here's how you can start watching a directory and get notified of any changes.

```php
 use Spatie\Watcher\Watcher
 
 ;(new Watcher())
    ->paths($directory)
    ->onAnyChange(function (string $type, string $path) {
        if ($type === Watcher::EVENT_TYPE_FILE_CREATED) {
            echo "file {$path} was created";
        }
    })
```

You can pass as many directories as you like to `paths`.

### Detected the type of change

The `$type` parameter of the closure you pass to `onAnyChange` can contain one of these values:

- `Watcher::EVENT_TYPE_FILE_CREATED`: a file was created
- `Watcher::EVENT_TYPE_FILE_UPDATED`: a file was updated
- `Watcher::EVENT_TYPE_FILE_DELETED`: a file was deleted
- `Watcher::EVENT_TYPE_DIRECTORY_CREATED`: a directory was created
- `Watcher::EVENT_TYPE_DIRECTORY_DELETED`: a directory was deleted

### Listening for specific events

To handle file systems events of a certain type, you can make use of dedicated functions. Here's how you would listen for file creations only.

```php
 (new Watcher())
    ->paths($directory)
    ->onFileCreated(function (string $newFilePath) {
        // do something...
    })
```

These are the related available methods:

- `onFileCreated()`: accepts a closure that will get passed the new file path
- `onFileUpdated()`: accepts a closure that will get passed the updated file path
- `onFileDeleted()`: accepts a closure that will get passed the deleted file path
- `onDirectoryCreated()`: accepts a closure that will get passed the created directory path
- `onDirectoryDeleted()`: accepts a closure that will get passed the deleted directory path

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
