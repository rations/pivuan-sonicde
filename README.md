# Pivuan SonicDE

The apt repository of [SonicDE](https://github.com/Sonic-DE) for
[Pivuan](https://github.com/rations/pivuan), Devuan excalibur on the Raspberry Pi (arm64).

SonicDE is an X11 desktop forked from KDE Plasma 6. It needs a newer Qt and KDE Frameworks than
Devuan has, so Pivuan builds the whole stack (Qt, SonicDE's frameworks, the desktop and its
applications) into `/opt/sonicde`. Devuan's own Qt and KDE packages in `/usr` are left as they are.

This is Pivuan's build of SonicDE, not a release of the SonicDE project. Report problems with
these packages at [rations/pivuan](https://github.com/rations/pivuan/issues).

## Install

On Pivuan:

```
sudo pivuan-config --cmd SONI01
```

That adds this repository, installs SonicDE and makes it the session on the login screen
(LightDM). `sudo pivuan-config --cmd SONI02` removes it again.

The repository is at https://rations.github.io/pivuan-sonicde, signed with the same key as the
[Pivuan apt repository](https://rations.github.io/pivuan).

## Packages

| Package | What it has |
|---|---|
| `sonicde` | the session (login screen entry, D-Bus and polkit links, screen locker PAM), and all of the below |
| `sonicde-qt` | Qt |
| `sonicde-frameworks` | SonicDE's frameworks and the libraries rebuilt for its Qt |
| `sonicde-workspace` | window manager, panel and desktop, system settings, screen locker, themes |
| `sonicde-apps` | file manager, terminal, system log viewer, image editor |
| `sonicde-icons` | icon and cursor themes |
| `sonicde-l10n` | translations |
| `sonicde-wallpapers` | wallpapers |

## How it is made

The build scripts are in [rations/pivuan, `sonicde/`](https://github.com/rations/pivuan/tree/master/sonicde):
`sonicde.conf` pins the releases, `sonicde.lock` every source commit, and `patches/` holds
Pivuan's changes. The packages are built on a PC in an excalibur arm64 root, then
`sonicde/push.sh` uploads them to `ghcr.io/rations/pivuan-sonicde/debs`. This repository's
**Publish SonicDE** workflow (started by hand) puts them in the apt repository, keeping the last
2 versions of each package. Each package's `/usr/share/doc/<package>/copyright` lists the sources
it was built from, with their licenses.
