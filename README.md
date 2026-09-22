# Spotify plugin for Spotube — Hetu line

Spotify metadata plugin for [Spotube](https://github.com/KRTirtho/spotube),
written in [Hetu](https://github.com/hetu-community/hetu). Maintained by
**Adamya Bhatt**; version `0.2.4`, plugin API `2.0.0`.

Provides authenticated Spotify metadata: library, liked tracks, playlists,
artist/album pages, search and scrobbling-capable endpoints. Audio streaming
itself comes from a separate audio-source plugin.

## Install

Spotube → Settings → Plugins → paste this URL → Install:

```
https://raw.githubusercontent.com/Adamyabhatt01/spotube-plugin-spotify/0.2.4/dist/plugin.smplug
```

Then open the installed entry and sign in to Spotify. Requires a Spotube build
that speaks plugin API 2.x.

The artifact is a file in this repository, so the URL above works without a
GitHub release. If you install it while a `Sonic Liberation` "Spotify" plugin is
already present you will get **two** metadata providers, because Spotube
identifies a plugin by name *and* author — disable or remove the other one.

## Relationship to upstream

This began as a fork of
[sonic-liberation/spotube-plugin-spotify](https://github.com/sonic-liberation/spotube-plugin-spotify),
whose `main` has since been rewritten in Kotlin/JS. That rewrite is not part of
this repository's mainline: `main` here is the Hetu implementation (the `0.2.x`
tags), which is what Spotube's plugin API 2.0.0 runs today. The upstream Kotlin
tree stays reachable as the second parent of the merge that established this
mainline, so nothing was rebased away.

Its dependency is [Adamyabhatt01/spotify-gql-client](https://github.com/Adamyabhatt01/spotify-gql-client),
pinned here by gitlink; that repository's `main` is the same Dart/Hetu line.

## Build from source

```bash
git clone --recurse-submodules \
  https://github.com/Adamyabhatt01/spotube-plugin-spotify.git
cd spotube-plugin-spotify
dart pub global activate hetu_script_dev_tools
hetu compile src/plugin.ht build/plugin.out
```

Then zip `plugin.json`, `build/plugin.out` and `assets/logo.png` into
`plugin.smplug` (`make archive` does this, and needs `zip`).

Both submodules resolve over https, so `--recurse-submodules` needs no SSH key.
`plugin.out` embeds its build timestamp, so two compiles of identical sources
differ in hash but not in code — compare it by behaviour, not by checksum.

## Forking

Fork this repository and its dependency, then edit `.gitmodules` in your fork to
point at your fork of the dependency. `plugin.json` holds the published name,
author, version, the abilities the host grants, and the repository URL that
Spotube uses for update checks — change `author` if you publish your own build,
otherwise you are overwriting someone else's plugin entry.
