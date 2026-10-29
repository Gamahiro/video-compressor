# vcompress

A tiny CLI that compresses a video with ffmpeg so it fits under chat upload limits (e.g. Discord's 20 MB).

## Requirements

- Python 3
- [ffmpeg](https://ffmpeg.org/) in your `PATH`

## Install

```sh
git clone <repo-url>
cd video-compressor
ln -s "$PWD/vcompress" ~/.local/bin/vcompress
```

Or just copy the `vcompress` file anywhere on your `PATH`.

## Usage

```sh
vcompress video.mp4             # med (default) -> video_med.mp4
vcompress --low video.mp4       # smallest file, max 480p
vcompress --high video.mp4      # best quality, max 1080p
vcompress -o out.mp4 video.mp4  # choose the output name
```

| Level    | Max height | Quality (CRF) | Audio |
|----------|-----------|---------------|-------|
| `--low`  | 480p      | 33            | 64k   |
| `--med`  | 720p      | 28            | 96k   |
| `--high` | 1080p     | 24            | 128k  |

Output is H.264 + AAC in an MP4, which plays almost everywhere. Videos smaller than the height cap are never upscaled, and your original file is never overwritten.

The levels set quality, not a target file size. If the result is still over 20 MB, the tool warns you; try `--low` or trim the clip.

## License

[MIT](LICENSE)
