# Retro Video Games Dataset

A video game dataset designed for data engineering, analytics, and business intelligence tutorials, available in small and large editions.

## Available data

| Schema | Size | Model | Format | Content |
| --- | --- | --- | --- | --- |
| `v1` | `small` | `relational` | `csv` | 20 games across 3 platforms |
| `v1` | `small` | `obt` | `csv` | 20 denormalized game and platform records |
| `v1` | `large` | `relational` | `csv` | 340 games across 3 platforms |
| `v1` | `large` | `obt` | `csv` | 340 denormalized game and platform records |

The `small` edition is intentionally limited so it remains easy to understand and fast to use in examples and automated tests. The `large` edition contains every row from `small` unchanged, followed by additional records for realistic ingestion and transformation exercises. Neither edition is intended to be exhaustive.

## Files

```text
data/v1/
├── small/
│   ├── relational/
│   │   └── csv/
│   │       ├── games.csv
│   │       └── platforms.csv
│   └── obt/
│       └── csv/
│           └── games.csv
└── large/
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

The OBT edition denormalizes each game and its platform into a single row and requires no join. For each size, it contains the same game records as the corresponding relational edition. The `large` files contain all 20 records from `small` unchanged, plus additional records.

Paths: `data/v1/<size>/obt/csv/games.csv`, where `<size>` is `small` or `large`.

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

- [Small relational games](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/small/relational/csv/games.csv)
- [Small relational platforms](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/small/relational/csv/platforms.csv)
- [Small OBT games](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/small/obt/csv/games.csv)
- [Large relational games](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/large/relational/csv/games.csv)
- [Large relational platforms](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/large/relational/csv/platforms.csv)
- [Large OBT games](https://raw.githubusercontent.com/nicedatafr/datasets/main/retro-video-games/data/v1/large/obt/csv/games.csv)

For reproducible tutorials, prefer a URL pinned to a Git tag once a release is available.

## Versioning

The directory `v1` identifies the schema version. Adding or correcting rows without changing the data contract does not require a new schema version. A new version is introduced when columns, relationships, or their meaning change significantly.
