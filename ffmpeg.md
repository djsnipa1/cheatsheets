FFMPEG
======

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
- 