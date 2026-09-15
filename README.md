# Psychoinformatics comparison inputs

These are reusable site-specific inputs for an Orinoco Lite comparison deployment, not the official Psychoinformatics website.
Git records changes to this input set over time; package code, template files, generated pages, and builds belong outside this repository.

## Inputs and scope

- `sources/pool/public-thing.jsonl` is the retained public Pool capture used by the native reference generator.
- `metadata/records/` and `metadata/overlays/annotations/` are its converted Lite records and machine-provenance companions.
- `site.yaml` contains the captured identity, navigation, and presentation settings.
- `content/` contains authored pages, section introductions, and ordinary page-bundle images, not generated record Markdown.

Record filenames use the PID after its prefix, retaining slash-separated paths beneath the class directory and percent-encoding unsafe filename characters; annotation companions mirror those paths.
The PID values inside the files are unchanged.

This baseline comes from the completed [same-capture comparison](https://github.com/ORINOCO-Lite/orinoco-lite-dev/blob/836fed5/docs/agents/upstream-deployment-validation.md).
The raw capture retains source values, including the invalid date omitted by the existing Lite conversion; that difference remains unresolved in the report.
The original capture time and API origin are not established by this repository's creation date.
Images are retained comparison inputs, not fresh downloads; metadata alone cannot reproduce their bytes.
Existing rights remain with their holders: this repository does not grant a new blanket license or resolve production publication and image-rights decisions.

## Build and deploy

From the sibling `orinoco-lite-dev` checkout, with the comparison package/template candidates available:

```console
pixi run orinoco-lite dev setup ../orinoco-lite-psychoinformatics-downstream \
  --site-specific ../psychoinformatics-site-specific \
  --template ../orinoco-lite-template
cd ../orinoco-lite-psychoinformatics-downstream
pixi run orinoco-lite build --base-url /
pixi run orinoco-lite verify-site build/site
pixi run orinoco-lite serve --port 8769
```

Setup installs this committed input repository at `site-specific/` and enables local package development.
For a portable deployment, import this tree into an ordinary downstream at `site-specific/` (for example with Git subtree), or publish it and use a reachable submodule URL.
Do not publish a local-path submodule or an editable package link.
Select the tested package commit and template candidate, or subsequent releases containing their fixes, in the downstream's normal dependency declarations.
The linked report identifies the candidates; no additional pin manifest is needed here.

Supply the actual deployment origin with `build --base-url https://YOUR-HOST/`, then publish the resulting `build/site/` using the downstream's normal hosting workflow.
The baseline is checked at an origin root; captured editorial URLs such as Explore's `/graph.js` need review before using project-subpath hosting.
The captured upstream `identity.base_url` is not permission to deploy to that domain.
No production cutover or GitHub editing destination is configured here.
Only a static host is required after building; neither the Lite build nor output comparison requires a running Pool API.

## Update and compare

For a new comparison, retain the new capture here and convert it in a fresh disposable downstream with `dev setup --snapshot`.
Review the resulting record and companion changes before updating this tree; do not overwrite site-authored changes or infer curation decisions.
Review media and authored-content updates separately, then commit the input change.
Regenerate the native reference from that same capture through a temporary local Pool API, stop the API, and compare the two static outputs using the linked guide.
Keep deliberate deviations in that comparison report rather than creating another difference ledger here.
The Explore page's snapshot notice is an intentional deployment clarification; there is no automatic refresh schedule.
