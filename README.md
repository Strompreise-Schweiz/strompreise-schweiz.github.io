# Strompreise Schweiz: hub repository

Tariff data of all utilities with constant and multilevel tariffs only, maintained by the
[Strompreise Schweiz](https://github.com/Strompreise-Schweiz) initiative. Each utility has one folder.
All logic lives in [`tariff-core`](https://github.com/Strompreise-Schweiz/tariff-core).

This repo is also the GitHub Pages site of the organization. It serves every utility under one domain,
including those with their own repo:

| What | URL |
|---|---|
| Every utility | [`https://data.strompreise-schweiz.ch/index.json`](https://data.strompreise-schweiz.ch/index.json) |
| One utility | `https://data.strompreise-schweiz.ch/<slug>/index.json` |
| Its current tariffs | `https://data.strompreise-schweiz.ch/<slug>/tariffs/current.json` |
| Status of all utilities | [`https://data.strompreise-schweiz.ch/status.html`](https://data.strompreise-schweiz.ch/status.html) |

The format is the VSE format with additional fields, see
[`SCHEMA.md`](https://github.com/Strompreise-Schweiz/tariff-core/blob/main/SCHEMA.md). Prices exclude VAT.


## VSE conformance

Whether the tariff file each utility publishes follows the [OpenAPI definitions of the VSE](https://github.com/Strompreise-Schweiz/tariff-core/tree/main/schemas/vse).
Details in `utilities/<slug>/data/vse-conformance.json`. Add a row when adding a utility.

| Utility | VSE 1.0.0 | VSE 1.0.1 |
|---|---|---|
| [`elektrizitaetswerk-wangen`](utilities/elektrizitaetswerk-wangen/) | [![VSE 1.0.0](https://img.shields.io/endpoint?url=https%3A%2F%2Fdata.strompreise-schweiz.ch%2Felektrizitaetswerk-wangen%2Fbadges%2Fvse-1.0.0.json)](utilities/elektrizitaetswerk-wangen/data/vse-conformance.json) | [![VSE 1.0.1](https://img.shields.io/endpoint?url=https%3A%2F%2Fdata.strompreise-schweiz.ch%2Felektrizitaetswerk-wangen%2Fbadges%2Fvse-1.0.1.json)](utilities/elektrizitaetswerk-wangen/data/vse-conformance.json) |

## Hub or own repo

A utility lives in exactly one place:

- **Here**, if it has constant and multilevel tariffs only. One workflow run publishes all of them.
- **In its own repo**, if it has dynamic tariffs or maintains its data itself. Those repos are listed
  in [`repositories.json`](repositories.json), so the overall index includes them.

A utility can move between the two without any URL on `data.strompreise-schweiz.ch` changing.
See [`docs/decisions.md`](https://github.com/Strompreise-Schweiz/tariff-core/blob/main/docs/decisions.md).

## Structure

| Path | Content | Who changes it |
|---|---|---|
| `utilities/<slug>/config/source.json` | Data sources | Person |
| `utilities/<slug>/curation/<year>.json` | Corrections and product mapping, each with a reason | Person |
| `utilities/<slug>/data/supplier.json` and logo | Details of the utility | Person |
| `utilities/<slug>/data/**` otherwise | Generated data | GitHub Actions only |
| `repositories.json` | Utilities with their own repo | Person |

The folder name must equal `slug` in `config/source.json`, because it is part of the URL.

## Adding a utility

Create `utilities/<slug>/` with `config/source.json` and `curation/`, then follow
[`adding-organization.md`](https://github.com/Strompreise-Schweiz/tariff-core/blob/main/docs/adding-organization.md).
Corrections are welcome as pull requests.

## License

Tariff data is published under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), as stated per
utility in `data_license`. Logos and brand names remain the property of their owners and are not covered.
