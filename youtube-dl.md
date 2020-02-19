# youtube-dl

## Options

### My Settinngs

```shell
-format "(bestvideo[vcodec^=av01][height>=720][fps>30]/bestvideo[vcodec=vp9.2][height>=720][fps>30]/bestvideo[vcodec=vp9][height>=720][fps>30]/bestvideo[vcodec^=av01][height>=720]/bestvideo[vcodec=vp9.2][height>=720]/bestvideo[vcodec=vp9][height>=720]/bestvideo[height>=720]/bestvideo)+(bestaudio[acodec=opus]/bestaudio)/best" -force-ipv4 --no-continue --download-archive archive.log --add-metadata --write-description --write-info-json --write-annotations --write-thumbnail --embed-thumbnail --sub-format "srt" --embed-subs --write-auto-sub
```

### Download Best Quality

```shell
--format "(bestvideo[vcodec^=av01][height>=1080][fps>30]/bestvideo[vcodec=vp9.2][height>=1080][fps>30]/bestvideo[vcodec=vp9][height>=1080][fps>30]/bestvideo[vcodec^=av01][height>=1080]/bestvideo[vcodec=vp9.2][height>=1080]/bestvideo[vcodec=vp9][height>=1080]/bestvideo[height>=1080]/bestvideo[vcodec^=av01][height>=720][fps>30]/bestvideo[vcodec=vp9.2][height>=720][fps>30]/bestvideo[vcodec=vp9][height>=720][fps>30]/bestvideo[vcodec^=av01][height>=720]/bestvideo[vcodec=vp9.2][height>=720]/bestvideo[vcodec=vp9][height>=720]/bestvideo[height>=720]/bestvideo)+(bestaudio[acodec=opus]/bestaudio)/best"
```
_Courtesy of Veloldo, tell youtube-dl to download the best quality available prioritizing the most compressed/recent codecs_

I'm going to modify it to take out 1080p

### Other Options

`--verbose` : Tell youtube\-dl to print various debugging information

`--force-ipv4` : Tell youtube\-dl to use IPv4, needed because lots of hosting and VPNs providers don't support IPv6.

`--ignore-errors` : Tell youtube\-dl to continue on download errors (for example to skip unavailable videos in a playlist)

`--no-continue` : Tell youtube\-dl not to resume partially downloaded files and to restart from the beginning (Mainly to avoid corruption)

`--no-overwrites` : Tell youtube\-dl not to overwrite existing files (Useful when metadata has already been downloaded)

`--download-archive archive.log` : Tell youtube\-dl to write every video that has been downloaded in `archive.log` to automatically skip them next time the script is started

`--add-metadata` : Tell youtube\-dl to write metadata to the video files

`--write-description` : Tell youtube\-dl to write video description to a `.description` file

`--write-info-json` : Tell youtube\-dl to write video metadata to a `.info.json` file

`--write-annotations` : Tell youtube\-dl to write video annotations to a `.annotations.xml` file

`--write-thumbnail` : Tell youtube\-dl to write thumbnail image to disk

`--embed-thumbnail` : Tell youtube\-dl to embed thumbnail in the audio as cover art (only useful when downloading audio\-only content like podcast)

`--all-subs` : Tell youtube\-dl to download all the available subtitles of the video

`--sub-format "srt"` : Tell youtube\-dl to prioritize `.srt` subtitles

`--embed-subs` : Tell youtube\-dl to embed subtitles in the video

(Channels Scripts) `--output "%(uploader)s/%(uploader)s - %(upload_date)s - %(title)s/%(uploader)s - %(upload_date)s - %(title)s.%(ext)s"` : Tell youtube\-dl to download the videos in folders and subfolders, using the naming scheme `Uploader/Uploader - 20191231 - Title/Uploader - 20191231 - Title.ext`

(Playlists Scripts) `--output "%(playlist)s (%(uploader)s)/%(upload_date)s - %(title)s/%(upload_date)s - %(title)s.%(ext)s"` : Tell youtube\-dl to download the videos in folders and subfolders, using the naming scheme `PlaylistName - Uploader/20191231 - Title/20191231 - Title.ext`

(Unique Scripts) `--output "%(title)s - %(uploader)s - %(upload_date)s/%(title)s - %(uploader)s - %(upload_date)s.%(ext)s"` : Tell youtube\-dl to download the videos in folders and subfolders, using the naming scheme `Title - Uploader - 20191231/Title - Uploader - 20191231.ext`

`--merge-output-format "mkv"` : Tell youtube\-dl to merge the video and audio that were downloaded separately in a `.mkv` file

(Archive Scripts) `--datebefore 20181231` : Tell youtube\-dl to download everything that was created before December 31, 2018 (included).

(Active Scripts) `--dateafter 20190101` : Tell youtube\-dl to download everything that was created after January 1, 2019 (included).

`--batch-file "Source - XXXXXX.txt"` : Tell youtube\-dl to look for links in `Source - XXXXXX.txt`
