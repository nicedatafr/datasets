# Nice Data Datasets

Public datasets maintained by [Nice Data](https://github.com/nicedatafr) for data engineering, analytics, and business intelligence tutorials.

## Available datasets

| Dataset | Description | Available models | Current schema |
| --- | --- | --- | --- |
| [Retro Video Games](retro-video-games/) | Video games and their platforms, provided in compact editions for tutorials and quick tests. | Relational, OBT | `v1` |

## Repository structure

Datasets follow this directory convention:

```text
<dataset>/data/<schema-version>/<size>/<model>/<format>/
```

- `schema-version` identifies the data contract, such as `v1`.
- `size` identifies the relative volume, such as `small` or `large`.
- `model` identifies the data representation, such as `relational` or `obt`.
- `format` identifies the storage format, such as `csv` or `parquet`.

Only editions and formats that are currently available are included in the repository.
