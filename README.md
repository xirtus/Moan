# Moan

Moan is the digital audio workstation of [SexOS](https://github.com/xirtus/sexos):
GarageBand-simple on the surface, with Logic-style depth underneath. It has audio and
MIDI tracks, a mixer, offline region rendering, WAV/FLAC/MP3 export, and CLAP and VST3
plugins. Each plugin runs in its own disposable protection domain, so a plugin that
crashes or hangs ends only itself.

This repository holds Moan's own source and history, extracted from the SexOS tree:

| Path | What it is |
| --- | --- |
| `apps/moan` | The Moan program (Weft UI, project model, transport, export) |
| `apps/moanrack` | Plugin rack helper and the restricted-helper crash/hang probes |
| `apps/moanplug` | The disposable helper that loads and runs one plugin |
| `apps/moan-probe` | Diagnostic probe used by the SexOS boot gates |
| `crates/moan-core` | Project, tracks, regions and the audio engine (no_std) |
| `crates/moan-export` | Audio export through the SexOS FFmpeg build |
| `crates/moan-plugin` | CLAP and VST3 hosting, jobs and the helper supervisor |
| `scripts/` | FFmpeg and plugin-fixture build helpers |

## Building

Moan builds inside the SexOS workspace for now: its manifests point at SexOS crates
(`sex-app`, `sex-pdx`, `weft`, `serenade-core`) and vendored plugin SDKs
(`vendor/clap-sys-0.5.0`, `vendor/vst3-0.3.0`) by relative path. Place this tree at the
root of a SexOS checkout and build with SexOS's `scripts/entrypoint_build.sh`. The SexOS
repository keeps the same tree in step with this one.

## Plans

- LV2 and LADSPA hosting beside CLAP and VST3, on a shared sandboxed plugin host.
- MIDI and parameter events into plugins, so instruments play and parameters automate.
- MIDI tracks with a piano roll, a built-in synth and sampler.

## License

GPL-3.0-only, like the rest of SexOS's own code. Vendored SDKs keep their own licenses.
