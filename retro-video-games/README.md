# Retro Video Games Dataset

A compact video game dataset designed for data engineering, analytics, and business intelligence tutorials.

## Available data

| Schema | Size | Model | Format | Content |
| --- | --- | --- | --- | --- |
| `v1` | `small` | `relational` | `csv` | 20 games across 3 platforms |
| `v1` | `small` | `obt` | `csv` | 20 denormalized game and platform records |

The `small` edition is intentionally limited so it remains easy to understand and fast to use in examples and automated tests. It is not intended to be exhaustive.

## Files

```text
data/v1/small/
├── relational/
│   └── csv/
│       ├── games.csv
│       └── platforms.csv
└── obt/
    └── csv/
        └── games.csv
```

## Relational model

### `games.csv`

One row represents one game released on one platform.

| Column | Description | Example |
| --- | --- | --- |
| `official_name` | Official game name | `Alex Kidd in Miracle World` |
| `short_name` | Short or commonly used game name | `Alex Kidd` |
| `platform_official_name` | Official platform name; references `platforms.official_name` | `Sega Master System` |
| `release_date` | Game release date in ISO 8601 format (`YYYY-MM-DD`) | `1987-09-01` |
| `series_universe` | Series or fictional universe associated with the game | `Alex Kidd` |

### `platforms.csv`

One row represents one video game platform.

| Column | Description | Example |
| --- | --- | --- |
| `official_name` | Official platform name and relational key | `Sega Master System` |
| `short_name` | Short or commonly used platform name | `Master System` |
| `brand` | Platform brand or manufacturer | `SEGA` |
| `release_date` | Platform release date in ISO 8601 format (`YYYY-MM-DD`) | `1987-09-01` |

## Relationship

The files can be joined using the platform's official name:

```text
games.platform_official_name = platforms.official_name
```

## One Big Table model

The OBT edition denormalizes each game and its platform into a single row. It contains the same 20 games as the relational edition and requires no join.

Path: `data/v1/small/obt/csv/games.csv`

| Column | Description | Example |
| --- | --- | --- |
| `game_official_name` | Official game name | `Alex Kidd in Miracle World` |
| `game_short_name` | Short or commonly used game name | `Alex Kidd` |
| `game_release_date` | Game release date in ISO 8601 format (`YYYY-MM-DD`) | `1987-09-01` |
| `series_universe` | Series or fictional universe associated with the game | `Alex Kidd` |
| `platform_official_name` | Official platform name | `Sega Master System` |
| `platform_short_name` | Short or commonly used platform name | `Master System` |
| `platform_brand` | Platform brand or manufacturer | `SEGA` |
| `platform_release_date` | Platform release date in ISO 8601 format (`YYYY-MM-DD`) | `1987-09-01` |

The `game_` and `platform_` prefixes make similarly named attributes unambiguous in the denormalized file.

## Direct access

The CSV files can be downloaded directly from the `main` branch:

- [games.csv](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/small/relational/csv/games.csv)
- [platforms.csv](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/small/relational/csv/platforms.csv)
- [games.csv (OBT)](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/small/obt/csv/games.csv)

For reproducible tutorials, prefer a URL pinned to a Git tag once a release is available.

## Versioning

The directory `v1` identifies the schema version. Adding or correcting rows without changing the data contract does not require a new schema version. A new version is introduced when columns, relationships, or their meaning change significantly.
