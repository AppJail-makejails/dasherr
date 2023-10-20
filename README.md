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

## How to build the Image

### Apache

```sh
appjail makejail \
    -j dasherr \
    -f "gh+AppJail-makejails/dasherr --file build-with-apache.makejail" \
    -o virtualnet=":dasherr default" \
    -o nat -- \
        --apache_tag 13.2-php81
```

### FPM

```sh
appjail makejail \
    -j dasherr \
    -f "gh+AppJail-makejails/dasherr --file build-with-php-fpm.makejail" \
    -o virtualnet=":dasherr default" \
    -o nat -- \
        --php_tag 13.2-81 --php_use_fpm 1
```

### Build

```sh
appjail stop dasherr
appjail cmd local dasherr sh -c "rm -f var/log/*"
appjail cmd local dasherr sh -c "rm -f var/cache/pkg/*"
appjail cmd local dasherr sh -c "rm -f var/run/*"
appjail cmd local dasherr vi etc/rc.conf
appjail image export dasherr
```

## Tags

| Tag                 | Arch    | Version           | Type   |
| ------------------- | ------- | ----------------- | ------ |
| `13.2-php81-apache` | `amd64` | `13.2-RELEASE-p4` | `thin` |
| `13.2-php81-fpm`    | `amd64` | `13.2-RELEASE-p4` | `thin` |
