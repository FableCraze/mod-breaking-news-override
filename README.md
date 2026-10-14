# Breaking News Override for SkyFire 5.4.8

Porting scaffold for [SkyFire_548](https://github.com/FableCraze/SkyFire_548).
This repository is maintained independently under the FableCraze account and
is not a GitHub fork of AzerothCore.

**Status: the port has not been implemented yet.** The source files in `src/`
are inherited from AzerothCore and are incompatible with SkyFire 5.4.8.
`module.cmake` disables their discovery by SkyFire's module system so this
scaffold can live in `modules/` without compiling incompatible code.

## Get the scaffold

From the root of a SkyFire checkout with module-system support, run:

```sh
git clone https://github.com/FableCraze/mod-breaking-news-override.git modules/mod-breaking-news-override
```

The repository is public. It has its own Git history, separate from the core.
Run commits and pushes from the module directory.

## Goal

Show news in the character-selection screen frame, using a local HTML file.
The original options in `conf/breakingnews.conf.dist` are preserved as a
reference; SkyFire does not load them while the module is disabled.

See [PORTING.md](PORTING.md) for the missing dependencies, integration points,
and activation criteria. Compilation and in-game behavior have not yet been
validated on client version 5.4.8.

## Origin and credits

Derived from [AzerothCore's mod-breaking-news-override](https://github.com/azerothcore/mod-breaking-news-override).
Credits go to the AzerothCore community and Foe for the original implementation.
This SkyFire port is maintained independently.

The original `LICENSE` file has been preserved. License notices for AGPL v3
also appear in the inherited source and configuration files; those notices
remain unchanged.
