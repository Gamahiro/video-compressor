# vcompress

A tiny CLI that compresses a video with ffmpeg so it fits under chat upload limits (e.g. Discord's 20 MB).

## Requirements

- Python 3
- [ffmpeg](https://ffmpeg.org/) in your `PATH`

## Install

Works on Linux and macOS, and should work on Windows (untested). Install ffmpeg first (e.g. `apt install ffmpeg`, `brew install ffmpeg`, or `winget install ffmpeg`).

### Linux / macOS

```sh
git clone https://github.com/Gamahiro/video-compressor
cd video-compressor
ln -s "$PWD/vcompress" ~/.local/bin/vcompress
```

Or just copy the `vcompress` file anywhere on your `PATH`.

### Windows

```powershell
git clone https://github.com/Gamahiro/video-compressor
cd video-compressor
python vcompress video.mp4
```

Windows ignores the script's shebang, so run it through `python` as shown. To call it from anywhere, put the folder on your `PATH` and use `python path\to\vcompress`, or wrap it in a small `.bat` file.

## Usage

```sh
vcompress video.mp4             # med (default) -> video_med.mp4
vcompress --low video.mp4       # smallest file, max 480p
vcompress --high video.mp4      # best quality, max 1080p
vcompress -o out.mp4 video.mp4  # choose the output name
```

On Windows, prefix each command with `python ` (e.g. `python vcompress --low video.mp4`).

| Level    | Max height | Quality (CRF) | Audio |
|----------|-----------|---------------|-------|
| `--low`  | 480p      | 33            | 64k   |
| `--med`  | 720p      | 28            | 96k   |
| `--high` | 1080p     | 24            | 128k  |

Output is H.264 + AAC in an MP4, which plays almost everywhere. Videos smaller than the height cap are never upscaled, and your original file is never overwritten.

The levels set quality, not a target file size. If the result is still over 20 MB, the tool warns you; try `--low` or trim the clip.

## License

[MIT](LICENSE)
