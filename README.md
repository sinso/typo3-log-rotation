# Backports `RotatingFileWriter` for TYPO3 v12

TYPO3 v13 comes with a `RotatingFileWriter` which is a great way to handle log rotation. This extension backports the `RotatingFileWriter` for your TYPO3 v12 installation.

The extension is technically compatible with TYPO3 v12 and v13, but will trigger a deprecation warning in TYPO3 v13 if the `RotatingFileWriter` of this extension is used.

## Usage

Use just as it is described in the [official documentation of the feature](https://docs.typo3.org/c/typo3/cms-core/main/en-us/Changelog/13.0/Feature-100926-IntroduceRotatingFileWriterforLogRotation.html).

Just replace the following classes:

| Original class name                             | Class provided by this extension                   |
|-------------------------------------------------|----------------------------------------------------|
| `\TYPO3\CMS\Core\Log\Writer\RotatingFileWriter` | `\Sinso\LogRotation\Log\Writer\RotatingFileWriter` |
| `\TYPO3\CMS\Core\Log\Writer\Enum\Interval`      | `\Sinso\LogRotation\Log\Writer\Enum\Interval`      |

## Example

```php
$GLOBALS['TYPO3_CONF_VARS']['LOG']['TYPO3']['CMS']['Core']['Resource']['ResourceStorage']['writerConfiguration'][\Psr\Log\LogLevel::ERROR] = [
    \Sinso\LogRotation\Log\Writer\RotatingFileWriter::class => [
        'interval' => \Sinso\LogRotation\Log\Writer\Enum\Interval::DAILY,
        'maxFiles' => 5,
    ],
];
```

## Migration to TYPO3 v13

When you migrate your installation to TYPO3 v13 change your logging configuration to use the core classes. Afterwards you can remove this extension.
