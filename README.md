# dedup-testdata

Shared sample media (camera JPEGs, RAW files, video clips) used as test fixtures by
[rpajarola/dedup](https://github.com/rpajarola/dedup), specifically its `fingerprint` package.

The expected-fingerprint test cases themselves (`.textproto` files) live only in the main
`dedup` repo, not here — this repo just holds the media and generic metadata about it, so it
stays useful independent of any one project's test format.

## Layout

- `sources.yaml` — per-file metadata (currently just source URL and media type) for every file
  distributed here. `source_url: null` means the file predates this record and its origin
  wasn't documented.
- The media files themselves are **not** stored in git history here. Instead they're distributed
  as tarballs attached to a [GitHub Release](https://github.com/rpajarola/dedup-testdata/releases),
  split by media type (`testdata-images.tar.gz`, `testdata-videos.tar.gz`, more to come as new
  test data categories are added).

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
