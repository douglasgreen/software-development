# PHP Checklist

## Composer

- Define an "autoload" section for [PSR-4
  autoload](https://www.phptutorial.net/php-oop/php-composer-autoload/).
- Define a "require" section and Set the [required PHP
  version](https://koenwoortman.com/composer-require-php-version/)
- Add a "require-dev" section to install development tools.
- Add a "scripts" section to run your development tools.

### Development Tools

Install these tools:
- [PHP Code Sniffer](https://github.com/squizlabs/PHP_CodeSniffer) for linting
  and formatting
- [PHP Mess Detector](https://phpmd.org/) for linting
- [PHPStan](https://phpstan.org/) for linting
- [PHPUnit](https://phpunit.de/index.html) for unit tests
- [Rector](https://getrector.com/) for upgrades

### Config files

Set up config files for each tool:
- phpcs.xml for PHPCS
- phpmd.xml for PHPMD
- phpstan.neon for PHPStan
- phpunit.xml for PHPUnit
- rector.php for Rector

### PHPStan

- Define [PHPStan global or local
  aliases](https://phpstan.org/writing-php-code/phpdoc-types#global-type-aliases)
  for any multi-dimenstional arrays or shapes.

### Maintenance

- Run `composer outdated` to check for upgrades.
- Run `composer update` to update within current version range.
- Run `composer update --with-all-dependencies` to update all dependencies.
- Update the Rector config file and run it.
