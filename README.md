# YouTube Liked Videos by Channel

Small CLI helper for listing your liked YouTube videos from one specific channel.

The script accepts a YouTube handle, resolves it to the channel's stable
`channel_id`, then fetches your private Liked Videos playlist and prints only
videos from that channel.

## Requirements

- `yt-dlp`
- `jq`
- A browser profile where you are signed in to YouTube

By default the script reads cookies from Firefox. Use `-b` to choose another
browser supported by `yt-dlp --cookies-from-browser`.

## Usage

```sh
./liked-by-channel KnottingKnots
./liked-by-channel @KnottingKnots
./liked-by-channel https://www.youtube.com/@KnottingKnots
```

With a different browser:

```sh
./liked-by-channel -b chrome KnottingKnots
```

## Output

Output is TSV on stdout:

```text
channel<TAB>title<TAB>url
```

Status messages are written to stderr, so stdout can be redirected or piped:

```sh
./liked-by-channel KnottingKnots > knotting_knots.tsv
./liked-by-channel KnottingKnots | fzf
```

## Handle-Only Input

The script intentionally does not accept display names like:

```sh
./liked-by-channel "Knotting Knots"
```

Display names are not unique. Handles are unique, so `KnottingKnots` resolves
directly to:

```text
https://www.youtube.com/@KnottingKnots
```

After the handle resolves, filtering uses `channel_id`, not the display name.
That is more stable for matching liked-video entries.
