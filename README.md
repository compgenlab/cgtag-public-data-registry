# cgtag-public-data-registry

A catalog of **annotation source/release configs** for [cgtag](https://github.com/compgenlab/cgtag).
It holds *configurations, not data* — `cgtag sync` downloads the actual files.

## Layout

```
registry.toml              catalog: [[sources]] and [[releases]] entries (each has a `file`)
sources/<name>@<ver>.toml  one source's config snippet (a source + its annotations)
releases/<name>.toml       a full release bundle
```

`registry.toml` is served over HTTPS (GitHub raw, Pages, S3 — anywhere). cgtag
points at its URL; entry `file` paths resolve relative to it.

## Consuming it

```sh
cgtag registry list                          # uses this registry by default
cgtag registry add-source 2026-06 clinvar    # merge a source's config into a local release
cgtag registry pull-release 2026-06          # pull a whole release
```

## Contributing a source

Run `cgtag registry submit <release> <source>` (needs a `public_repo` `GITHUB_TOKEN`),
or open an issue with the **`source-submission`** label and the source config in a
` ```toml ` block. The [issue-to-pr workflow](.github/workflows/issue-to-pr.yml)
parses it, writes `sources/<name>@<version>.toml`, adds the `registry.toml` entry,
and opens a PR closing the issue — a maintainer reviews and merges.
