# dedup-testdata

Shared sample media (camera JPEGs, RAW files, video clips) used as test fixtures by
[rpajarola/dedup](https://github.com/rpajarola/dedup) (`fingerprint` package) and
[rpajarola/exiftools](https://github.com/rpajarola/exiftools).

The expected-value test cases themselves (`.textproto` files, `regression_data.go`, etc.) live
only in each consuming repo, not here — this repo just holds the media and generic metadata
about it, so it stays useful independent of any one project's test format.

## Layout

- `sources.yaml` — per-file metadata for every file distributed here: `source_url` (where it was
  downloaded from; `null` means the file predates this record and its origin wasn't documented),
  `type` (image/video/sidecar/raw-exif), `archive_url` (which release tarball contains it), and
  an optional `note` for anything non-obvious (e.g. deliberately corrupted fixtures).
- The media files themselves are **not** stored in git history here. Instead they're distributed
  as tarballs attached to a [GitHub Release](https://github.com/rpajarola/dedup-testdata/releases),
  split by media type (`testdata-images.tar.gz`, `testdata-videos.tar.gz`, more to come as new
  test data categories are added). `testdata-images.tar.gz` has one subdirectory, `corrupt/`,
  containing intentionally malformed files used to test parser error handling — everything else
  is flat.

## Fetching the media files

Download the latest release's tarballs and extract them:

```sh
for asset in testdata-images testdata-videos; do
  curl -L -o "$asset.tar.gz" \
    "https://github.com/rpajarola/dedup-testdata/releases/latest/download/$asset.tar.gz"
  tar -xzf "$asset.tar.gz"
done
```

The `fingerprint` package in the main `dedup` repo does this automatically before running its
tests.
