# gradle-cache-cleaner

A shell script that reclaims disk space by removing cached Maven and Gradle dependencies.

## What it does

Scans two caches and deletes old versions of each artifact, keeping only the latest:

- **`~/.m2/repository`** — Maven local repository
- **`~/.gradle/caches/modules-2/files-2.1`** — Gradle module cache

SNAPSHOT versions are left untouched by default.

## Usage

```sh
# Delete old versions, keep latest (SNAPSHOTs untouched)
./clean-gradle-cache

# Delete everything — all versions, latest, and SNAPSHOTs
./clean-gradle-cache --all

# Preview without deleting (works with or without --all)
./clean-gradle-cache --dry-run
./clean-gradle-cache --all --dry-run
```

### Example output

```
Scanning /Users/you/.m2/repository ...
  deleting  /Users/you/.m2/repository/com/squareup/okhttp3/okhttp/4.9.3  (1.2M)
  deleting  /Users/you/.m2/repository/com/squareup/okhttp3/okhttp/4.10.0  (1.3M)

Scanning /Users/you/.gradle/caches/modules-2/files-2.1 ...
  deleting  /Users/you/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-stdlib/1.8.22  (3.1M)

Done — removed 3 old version directories.
```

## Requirements

- **bash** 4+
- **`sort -V`** — available natively on Linux and macOS 12+

## Installation

Clone the repo and make the script executable:

```sh
git clone git@github.com:Abdallah-Abdelazim/gradle-cache-cleaner.git
cd gradle-cache-cleaner
chmod +x clean-gradle-cache
```

Then run it directly:

```sh
./clean-gradle-cache --dry-run
```

Or place it on your `PATH` for convenience:

```sh
cp clean-gradle-cache /usr/local/bin/
```
