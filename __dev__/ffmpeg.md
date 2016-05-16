# ffmpeg

Home page is [ffmpeg.org](https://ffmpeg.org/). Source code at [git.ffpmeg.org](https://git.ffmpeg.org/ffmpeg.git).Github mirrors indicated below

The source is divided into multiple repos

- main source: [https://git.ffmpeg.org/ffmpeg.git](https://git.ffmpeg.org/ffmpeg.git)
- web site source: [https://git.ffmpeg.org/ffmpeg-web](https://git.ffmpeg.org/ffmpeg-web)
- FATE server: [https://git.ffmpeg.org/fateserver](https://git.ffmpeg.org/fateserver)

There are Github mirrors for each of these

- mirror of main repo: [https://github.com/FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg)

FFMpeg has a number of standalone libraries.

## Libavutil

[Libavutil Documentation](https://ffmpeg.org/libavutil.html)

This is a mostly standalone library for crypto, random numbers and the like. It also has a large number of constants
for pixel formats.

## Libswscale

[Libswscale Documentation](https://ffmpeg.org/libswscale.html)

Notable for containing sws_scale for converting pixel formats (say RGB to YUV). It also has rescaling options.
