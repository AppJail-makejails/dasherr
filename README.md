# Dasherr

Dasherr is a minimal and lightweight dashboard for your self-hosted services (and bookmarks).

Features:

* Loads instantly + Remains light on resources
* Responsive design (uses Bootstrap framework)
* Shows Temperature, CPU load and Memory used by tapping into Glances API (default 5s updates)
* Built-in online check of services (checked only at time of page load/refresh, to minimize background activity & load)
* Several built-in **Themes** (easy to edit & add your own)
* Wallpaper backgrounds supported
* FontAwesome icons (also supports Self-hosted/Web image icons)
* All settings in a single easy to edit json file, with **built-in editor**
* Support for alternate configurations without needing multiple Dasherr installations

github.com/erohtar/Dasherr

<img src="https://raw.githubusercontent.com/erohtar/Dasherr/main/www/res/favicon.svg" width="30%" height="auto" alt="Dasherr logo">

## How to use this Makejail

```console
$ appjail oci run -Pd \
    -o overwrite=force \
    -o virtualnet=":<random> default" \
    -o nat \
    -o fstab="/path/to/your/config.json /usr/local/www/html/settings.json" \
    ghcr.io/appjail-makejails/dasherr dasherr
```

### Arguments (stage: build)

* `dasherr_from` (default: `ghcr.io/appjail-makejails/dasherr`): Location of OCI image. See also [OCI Configuration](#oci-configuration).
* `dasherr_tag` (default: `latest`): OCI image tag. See also [OCI Configuration](#oci-configuration).

### Environment (OCI image)

* `PGID` (default: `1000`): Equivalent to `PUID` but for the Process Group ID.
* `PUID` (default: `1000`): Process User ID for the container's main process, allowing you to match the owner of files written to mounted host volumes to your host system's user. Writable volumes are changed based on this environment variable.
* `UMASK` (default: `0022`): Override default umask setting.

## OCI Configuration

```yaml
build:
  variants:
    - tag: 15.1-apache
      containerfile: Containerfile.apache
      aliases: ["latest"]
      default: true
      args:
        FREEBSD_RELEASE: "15.1"
        APACHEVER: "24"
        PHPVER: "84"
        NO_PKGCLEAN: "1"
      cache_dirs: ["pkgcache0:/var/cache/pkg"]
    - tag: 15.1-fpm
      containerfile: Containerfile.fpm
      args:
        FREEBSD_RELEASE: "15.1"
        PHPVER: "84"
        NO_PKGCLEAN: "1"
      cache_dirs: ["pkgcache0:/var/cache/pkg"]
```
