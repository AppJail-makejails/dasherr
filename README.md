# Dasherr

A Minimal and lightweight dashboard for your self-hosted services (and bookmarks).

## Features:

* Loads instantly + Remains light on resources
* Responsive design (uses Bootstrap framework)
* Shows Temperature, CPU load and Memory used by tapping into Glances API (default 5s updates)
* Built-in online check of services (checked only at time of page load/refresh, to minimize background activity & load)
* Several built-in **Themes** (easy to edit & add your own)
* Wallpaper backgrounds supported
* FontAwesome icons (also supports Self-hosted/Web image icons)
* All settings in a single easy to edit json file, with **built-in editor**
* Support for alternate configurations without needing multiple Dasherr installations

<img src="https://raw.githubusercontent.com/erohtar/Dasherr/main/www/res/favicon.svg" width="30%" height="auto">

github.com/erohtar/Dasherr

## How to use this Makejail

```sh
appjail makejail \
    -j dasherr \
    -f gh+AppJail-makejails/dasherr \
    -o virtualnet=":dasherr default" \
    -o nat \
    -o expose=80
appjail cmd local dasherr cp $PWD/settings.json usr/local/www/apache24/data/settings.json
appjail cmd jexec dasherr chown www:www /usr/local/www/apache24/data/settings.json
```

### Arguments

* `dasherr_tag` (default: `13.2-php81-apache`): see [#tags](#tags).
* `dasherr_php_type` (default: `production`) The PHP configuration file to link to `/usr/local/etc/php.ini`. Valid values: `development`, `production`. Only valid for apache, use the `php_type` argument when using php-fpm.

### Volumes

#### Apache

| Name                    | owner | group | perm | type | mountpoint                                   |
| ----------------------- | ----- | ----- | ---- | ---- | -------------------------------------------- |
| adminerevo-plugins-file |   -   |   -   |  -   |  -   | usr/local/www/apache24/data/plugins.php      |
| adminerevo-plugins      |   -   |   -   |  -   |  -   | /usr/local/www/apache24/data/plugins         |
| adminerevo-drivers      |   -   |   -   |  -   |  -   | /usr/local/www/apache24/data/plugins/drivers |

#### FPM

| Name                    | owner | group | perm | type | mountpoint                                |
| ----------------------- | ----- | ----- | ---- | ---- | ----------------------------------------- |
| adminerevo-plugins-file |   -   |   -   |  -   |  -   | usr/local/www/adminerevo/plugins.php      |
| adminerevo-plugins      |   -   |   -   |  -   |  -   | /usr/local/www/adminerevo/plugins         |
| adminerevo-drivers      |   -   |   -   |  -   |  -   | /usr/local/www/adminerevo/plugins/drivers |

## Tags

| Tag                 | Arch    | Version        | Type   |
| ------------------- | ------- | -------------- | ------ |
| `13.2-php81-apache` | `amd64` | `13.2-RELEASE` | `thin` |
| `13.2-php81-fpm`    | `amd64` | `13.2-RELEASE` | `thin` |
| `14.0-php81-apache` | `amd64` | `14.0-RELEASE` | `thin` |
| `14.0-php81-fpm`    | `amd64` | `14.0-RELEASE` | `thin` |
