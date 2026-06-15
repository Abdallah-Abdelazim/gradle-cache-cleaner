# gradle-cache-cleaner

A shell script that reclaims disk space by removing old versions of cached Maven and Gradle dependencies, keeping only the latest version of each artifact.

## What it does

Scans two caches and deletes all but the most recent version of each artifact:

- **`~/.m2/repository`** — Maven local repository
- **`~/.gradle/caches/modules-2/files-2.1`** — Gradle module cache

SNAPSHOT versions are left untouched.

## Usage

```sh
# Preview what would be deleted (safe, no changes made)
./clean-old-deps --dry-run

# Delete old versions
./clean-old-deps
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
chmod +x clean-old-deps
```

Then run it directly:

```sh
./clean-old-deps --dry-run
```

Or place it on your `PATH` for convenience:

```sh
cp clean-old-deps /usr/local/bin/
```
