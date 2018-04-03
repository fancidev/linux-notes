# Debian Notes

## Installing Debian on Hyper-V (Windows 10)

### Configure package source

If network is not available during installation, the setup program will not
provide mirror urls for packages. As a result, attempts to `apt install` will
result in various seemingly weird errors.

The solution is to edit `/etc/apt/sources.list` and add package sources. For
convenience and reliability, I just add the primary source (rather than
mirrors). The following lines are suitable:

```
# This is the main source for packages.
deb http://deb.debian.org/debian stretch main
deb-src http://deb.debian.org/debian stretch main

# This is the source for security packages.
deb http://security.debian.org/debian-security stretch/updates main
deb-src http://security.debian.org/debian-security stretch/updates main

# Below sources are urgent updates to the main packages, but not as urgent
# as those in the security source.
deb http://deb.debian.org/debian/ stretch-updates main
deb-src http://deb.debian.org/debian/ stretch-updates main
```

Notes:
- `deb` is for binary package. `deb-src` is for source-code package.
- `stretch` is the code name for Debian 9.

After adding the package sources, run `apt update` from root to refresh the
local package cache. This command visits each configured source and downloads
the list of available packages and their versions.

When the command finishes, it informs you how many packages can be "upgraded".
To upgrade them, run `apt upgrade`.
