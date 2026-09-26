# dedup-testdata

Shared test fixtures for [rpajarola/dedup](https://github.com/rpajarola/dedup), specifically the
`fingerprint` package's larger sample photos/videos (camera JPEGs, RAW files, video clips).

## Layout

- `large_testdata/*.textproto` — expected fingerprint values for each sample file, checked into
  this repo directly.
- The actual sample media files are **not** stored in git history here (they're large binary
  camera/video samples). Instead they're distributed as tarballs attached to a
  [GitHub Release](https://github.com/rpajarola/dedup-testdata/releases) on this repo, split by
  media type (`testdata-images.tar.gz`, `testdata-videos.tar.gz`, more to come as new test data
  categories are added).

## Fetching the media files

Download the latest release's tarballs and extract them alongside the `.textproto` files in
`large_testdata/`:

```sh
for asset in testdata-images testdata-videos; do
  curl -L -o "$asset.tar.gz" \
    "https://github.com/rpajarola/dedup-testdata/releases/latest/download/$asset.tar.gz"
  tar -xzf "$asset.tar.gz"
done
```

The `fingerprint` package in the main repo does this automatically before running its tests.
