# Data

The files the notebook reads are not committed. When the terms let you republish them, they are assets on the GitHub release tagged `data`. The release is public. When the terms let you download the files but not republish them, do not create that release. Write the command that downloads them from the source, and say what it needs (an account, a key in `.env`, a path).

`OWNER/REPO` is your fork, the form `username/aii600-final-project`. In the clone, once:

```bash
gh repo set-default OWNER/REPO
```

Create the release from the project root, after the files are in this folder:

```bash
gh release create data data/your-file.csv --repo OWNER/REPO --title "Data" --notes "See data/README.md"
```

Add every file the notebook reads. When a file changes:

```bash
gh release upload data data/your-file.csv --repo OWNER/REPO --clobber
```

On another machine:

```bash
gh release download data --dir data --repo OWNER/REPO
```

Record a SHA-256 for each file. Replacing a file with `--clobber` does not show up in git, so update the hash in the same commit:

```bash
shasum -a 256 data/your-file.csv
```

## This project

**Source.** SAMHSA, National Survey on Drug Use and Health (NSDUH), public-use files, 2021 to 2024: https://www.samhsa.gov/data/data-we-collect/nsduh-national-survey-drug-use-and-health/datafiles/2024. SAMHSA states that 2021 on cannot be pooled with earlier years.

**Republishing.** The SAMHSA pages state no license or redistribution terms. Until that is confirmed, the files are not on a release. Download them from the source. No account or key is needed.

**Download.** From the project root:

```bash
mkdir -p data/raw data/codebooks
B=https://www.samhsa.gov/data/system/files/media-puf-file
for f in NSDUH-2021-DS0001-bndl-data-tsv_v4.zip NSDUH-2022-DS0001-bndl-data-tsv_v2.zip \
         nsduh-2023-ds0001-bndl-data-tsv_v2.zip NSDUH-2024-DS0001-bndl-data-tsv_v1.zip; do
  curl -fL -o data/raw/$f "$B/$f"
done
for f in NSDUH-2021-DS0001-info-codebook.pdf NSDUH-2022-DS0001-info-codebook_v2.pdf \
         nsduh-2023-ds0001-info-codebook_v2.pdf nsduh-2024-ds0001-info-codebook_v1.pdf; do
  curl -fL -o data/codebooks/$f "$B/$f"
done
shasum -a 256 data/raw/*.zip
```

Each zip holds one tab-separated file, `NSDUH_<year>_Tab.txt`. The notebook reads it from the zip without unzipping it. The 2024 file is version 1, so SAMHSA may revise it. A new version has a new file name and hash.

**Files and SHA-256** (downloaded 2026-10-26):

| File | Size | Rows | Columns | SHA-256 |
|---|---:|---:|---:|---|
| `raw/NSDUH-2021-DS0001-bndl-data-tsv_v4.zip` | 38.1 MB | 58,034 | 2,995 | `3e1ad9449f5f8d7acdc5df085b561b30d59a77dca96a3525610efe91cee75497` |
| `raw/NSDUH-2022-DS0001-bndl-data-tsv_v2.zip` | 30.3 MB | 59,069 | 2,653 | `cde54c4af548de3cacebff00127fda4ffa645fb9cd4803dbd0ae9ed3df1c799f` |
| `raw/nsduh-2023-ds0001-bndl-data-tsv_v2.zip` | 29.0 MB | 56,705 | 2,636 | `f2ed2fb234ebe04b6548e827fd90138830bb6bc8411e215a526d0ef3ddcd9324` |
| `raw/NSDUH-2024-DS0001-bndl-data-tsv_v1.zip` | 29.8 MB | 58,633 | 2,632 | `a26f3009991e848c9a6b594e5d57906621a75459c7ba51d10b409ed2f8432a8f` |

**Unit, sample size, time span.** One respondent aged 12 or older, per survey year, 2021 to 2024. The row counts above include all ages. The analysis keeps adults who received mental-health treatment in the past year, a count that comes from the notebook. Each row has an analysis weight, `ANALWT2_C`. Population estimates use it.
