# spotube-plugin-spotify

Spotify metadata plugin for [Spotube](https://github.com/KRTirtho/spotube),
written in [Hetu](https://github.com/hetu-community/hetu). Version
`0.2.3-inline`, plugin API `2.0.0`.

Provides authenticated Spotify metadata: library, liked tracks, playlists,
artist/album pages, search and scrobbling-capable endpoints. Streams themselves
come from a separate audio-source plugin.

## Install

Spotube → Settings → Plugins → paste this URL → Install:

```
https://raw.githubusercontent.com/Adamyabhatt01/spotube-plugin-spotify/0.2.3-inline/dist/plugin.smplug
```

Then open the installed entry and sign in to Spotify. Requires a Spotube build
that speaks plugin API 2.x.

This fork publishes its bytecode as a file in the repository, so the URL above
works without a GitHub release. The upstream project is
[sonic-liberation/spotube-plugin-spotify](https://github.com/sonic-liberation/spotube-plugin-spotify),
whose releases carry the same `plugin.smplug` asset and appear in Spotube's
in-app plugin index automatically.

## Build from source

```bash
git clone --recurse-submodules https://github.com/Adamyabhatt01/spotube-plugin-spotify.git
cd spotube-plugin-spotify
dart pub global activate hetu_script_dev_tools
make compile      # -> build/plugin.out
make archive      # -> build/plugin.smplug (needs `zip`)
```

Both submodules resolve over https, so `--recurse-submodules` needs no SSH key.
`plugin.out` embeds its build timestamp, so two compiles of identical sources
differ in hash but not in code — compare it by behaviour, not by checksum.

## Forking

Fork this repository and its dependency,
[Adamyabhatt01/spotify-gql-client](https://github.com/Adamyabhatt01/spotify-gql-client)
(the Hetu Spotify GraphQL client), then edit
`.gitmodules` in your fork of the plugin to point at your fork of the
dependency. `plugin.json` holds the published name, author, version and the
abilities the host grants the plugin.
