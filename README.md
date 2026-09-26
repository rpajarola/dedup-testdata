# dedup-testdata

Shared test fixtures for [rpajarola/dedup](https://github.com/rpajarola/dedup), specifically the
`fingerprint` package's larger sample photos/videos (camera JPEGs, RAW files, video clips).

## Layout

- `large_testdata/*.textproto` — expected fingerprint values for each sample file, checked into
  this repo directly.
- The actual sample media files are **not** stored in git history here (they're large binary
  camera/video samples). Instead they're distributed as a tarball attached to a
  [GitHub Release](https://github.com/rpajarola/dedup-testdata/releases) on this repo.

## Fetching the media files

Download the latest release's `large_testdata.tar.gz` and extract it alongside the `.textproto`
files in `large_testdata/`:

```sh
curl -L -o large_testdata.tar.gz \
  https://github.com/rpajarola/dedup-testdata/releases/latest/download/large_testdata.tar.gz
tar -xzf large_testdata.tar.gz
```

The `fingerprint` package in the main repo does this automatically before running its tests.
