# Psychoinformatics comparison inputs

This repository supplies the Psychoinformatics content for the [comparison downstream](https://github.com/ORINOCO-Lite/psychoinformatics-downstream).
It supports development with the ORINOCO team, using one capture to compare native ORINOCO with Orinoco Lite.
The [official website](https://www.psychoinformatics.de/) is a separate deployment.

## Inputs

- `sources/pool/public-thing.jsonl`: captured Pool records.
- `metadata/`: converted records and annotation companions.
- `site.yaml`: identity, navigation, and presentation settings.
- `content/`: authored pages, section introductions, portraits, images, and dataset bundle resources.
- `assets/img/`: institutional logos processed by Hugo.
- `static/`: identity images published at their original paths.
- `overrides/`: upstream home layout and identity settings that replace the neutral template defaults.

The home layout comes from the selected `www-from-model` revision.
Its asset and Explore links use Hugo's `relURL` so the site also works under a hosting path prefix.
Dataset bundle resources stay in `content/` so upstream Hugo publishes the downloads and embeds their Dataset JSON-LD.
Generated record pages and graphs do not belong here.
The reusable template contains none of this site's branding or dataset downloads.

The retained capture contains 5,030 records.
Its original capture time is unknown.
Metadata preserves the capture's compact or expanded annotation values and its original PAV spelling.
The annotation companions retain the source form where reconstruction requires it; joining them to YAML must reproduce all 5,030 captured JSON records exactly.
Git records later input changes.
The downstream's submodule selects the input commit for each build.

## Build and compare

Clone the downstream with its submodule, then run:

```console
pixi run --locked build
pixi run --locked orinoco-lite serve --port 8769
```

Use `build-pages` instead of `build` to test the configured public URL.
These builds need no Pool API.

For a new capture or software repin, follow the package's [comparison procedure](https://github.com/ORINOCO-Lite/orinoco-lite-dev/blob/codex/stage-c-records/docs/agents/staged-upstream-validation.md).
It generates both sites from the same inputs and reports their differences.
Keep generated reports outside this input repository.
