# Ansible Role: `locales`

[![Code Linter](https://github.com/Frzk/ansible-role-locales/actions/workflows/linter.yml/badge.svg?branch=main)](https://github.com/Frzk/ansible-role-locales/actions/workflows/linter.yml)

This Ansible role allows you to install and configure the *locales* of the targeted host.

More precisely, it will:
- Generate `/etc.locale.conf` or `/etc/default/locale` (depending on the host OS)
- Generate `/etc/locale.gen`
- Generate the locales depending on the previous file.

Some distributions (such as Arch Linux) don't need any additional package. In this case, just leave `locales_package_name` empty (or remove it).

Also, please note that we are completely replacing the content of the `/etc/locale.gen` file, so **you have to triple-check the values you provide**.

## Role variables

Variables and properties in bold are mandatory. Others are optional.

| Variable name                | Description                                          | Default value                                                                  |
| ---------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------ |
| `locales_package_name`       | Name of the package to install.                      |                                                                                |
| `locales_configuration_file` | Path to the locale configuration file of the system. | `/etc/locale.conf`                                                             |
| `locales_locales`            | A list of [locales](#locale-properties).             | See [locales properties](#locale-properties) default values.                   |
| `locales_lang`               | Value to use as the `LANG` environment variable.     | `locale` value of the first [locale](#locale-properties) in `locales_locales`. |
| `locales_language`           | Value to use as the `LANGUAGE` environment variable. | `locales_lang`                                                                 |
| `locales_lc`                 | A [locales_lc](#locales_lc-properties) dict.         | `{}`                                                                           |

:green_book: Documentation:

- [More about locales and environment variables](https://www.gnu.org/software/gettext/manual/html_node/Setting-the-POSIX-Locale.html#Setting-the-POSIX-Locale)

### locale properties

| Property name   | Description     | Default value |
| --------------- | --------------- |-------------- |
| **`locale`**    | Locale name.    | `en_US.UTF-8` |
| `charset`       | Locale charset. | `UTF-8`       |

### locales_lc properties

:point_right: These are only set if a value different from `locales_lang` is provided.

| Property  name   | Description                                                   | Default value  |
| ---------------- | ------------------------------------------------------------- | -------------- |
| `address`        | Value to use as the `LC_ADDRESS` environment variable.        | `locales_lang` |
| `all`            | Value to use as the `LC_ALL` environment variable.            | `locales_lang` |
| `collate`        | Value to use as the `LC_COLLATE` environment variable.        | `locales_lang` |
| `ctype`          | Value to use as the `LC_CTYPE` environment variable.          | `locales_lang` |
| `identification` | Value to use as the `LC_IDENTIFICATION` environment variable. | `locales_lang` |
| `measurement`    | Value to use as the `LC_MEASUREMENT` environment variable.    | `locales_lang` |
| `messages`       | Value to use as the `LC_MESSAGES` environment variable.       | `locales_lang` |
| `monetary`       | Value to use as the `LC_MONETARY` environment variable.       | `locales_lang` |
| `name`           | Value to use as the `LC_NAME` environment variable.           | `locales_lang` |
| `numeric`        | Value to use as the `LC_NUMERIC` environment variable.        | `locales_lang` |
| `paper`          | Value to use as the `LC_PAPER` environment variable.          | `locales_lang` |
| `response`       | Value to use as the `LC_RESPONSE` environment variable.       | `locales_lang` |
| `telephone`      | Value to use as the `LC_TELEPHONE` environment variable.      | `locales_lang` |
| `time`           | Value to use as the `LC_TIME` environment variable.           | `locales_lang` |


## Example

Here is a small example of what your file should look like.

**IMPORTANT**: DO NOT use this example as it is.

```yaml
---
locales_locales:
  - locale: en_US.UTF-8
    charset: UTF-8
  - locale: fr_BE.UTF-8
    charset: UTF-8

locales_lc:
  collate: "fr_FR.UTF-8"
...
```


## Contributing

Code reviews, patches, comments, bug reports and feature requests are welcome. Please read the [Contributing Guide](CONTRIBUTING.md) for further details.
