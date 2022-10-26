FFMPEG
======

## Convert AVI to MP4

**no Re-encode**: Only changing the container

```bash
ffmpeg -i input_filename.avi -c:v copy -c:a copy -y output_filename.mp4
```
In this commandline, you are providing

- the AVI video as input
- specifying the name of the output MP4 file,
- instructing FFmpeg to directly copy the audio and video (seen here: ``-c:v copy -c:a copy``) from the AVI container format to the MP4 container format.

Convert Image Sequence to Video
-------------------------------

#### Sequential

In this example the input images are sequentially named img001.png, img002.png, img003.png, etc.

```bash
ffmpeg -framerate 24 -i img%03d.png output.mp4
```
- When outputting H.264, adding `-vf format=yuv420p or -pix\_fmt yuv420p` will ensure compatibility so crappy players can decode the video. See the [colorspace and chroma-subsampling](https://trac.ffmpeg.org/wiki/Slideshow#Colorspaceconversionandchromasub-sampling) for more info.

- If \-framerate option is omitted the default will input and output 25 frames per second. See [Frame rates](https://trac.ffmpeg.org/wiki/Slideshow#Framerates) for more info.

#### Starting with a specific image

For example if you want to start with img126.png then use the `-start_number` option:

```bash
ffmpeg -start_number 126 -i img%03d.png -pix_fmt yuv420p out.mp4
```

#### Pipe

You can use `cat` or other tools to pipe to ffmpeg:

```bash
cat *.png | ffmpeg -f image2pipe -i - output.mkv
```
Convert .mov to .mp4
--------------------

``` shell
ffmpeg -i IMG_1530.mov -vcodec h264 -acodec mp2 my-video.mp4
```

Converting .oog to .mp3
-----------------------

*I used this command:*

``` bash
ffmpeg -i audio.ogg -b:a 320k audio.mp3
```

Here is a more complicated version:

``` bash
ffmpeg -i input.wav -vn -ar 44100 -ac 2 -b:a 192k output.mp3
```

**Explanation of the used arguments in this example:**

-   -i - input file
-   -vn - Disable video, to make sure no video (including album cover
    image) is included if the source would be a video file
-   -ar - Set the audio sampling frequency. For output streams it is set
    by default to the frequency of the corresponding input stream. For
    input streams this option only makes sense for audio grabbing
    devices and raw demuxers and is mapped to the corresponding demuxer
    options.
-   -ac - Set the number of audio channels. For output streams it is set
    by default to the number of input audio channels. For input streams
    this option only makes sense for audio grabbing devices and raw
    demuxers and is mapped to the corresponding demuxer options. So used
    here to make sure it is stereo (2 channels)
-   -b:a - Converts the audio bitrate to be exact 192kbit per second
