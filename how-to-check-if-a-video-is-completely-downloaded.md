`ffmpeg` is an OS agnostic tool that is capable of determining if a video file has been completely downloaded. The command below instructs `ffmpeg` to read the input video and encode the video to nothing. During the encoding process, any errors such as missing frames are output to test.log.
 ```Shell
ffmpeg -v error -i FILENAME.mp4 -f null - 2>test.log
```
If a video file is not totally downloaded, there will be many lines in the test.log file. For example, .1 MB missing from a video file produced 71 lines of errors. If the video is fully downloaded and hasn’t been corrupted, no errors are found, and no lines are printed to test.log.

Edit

In the example I gave above, I tested the entire file because the test video I downloaded was a torrent, which can have missing chunks throughout the file.

Adding `-sseof -60` to the list of arguments will check the last 60 seconds of the file, which is considerably faster.
```Shell
ffmpeg -v error -sseof -60 -i FILENAME.mp4 -f null - 2>test.log
```
You'll need a newer version of ffmpeg, 2.8 was missing the sseof flag, so I used 3.0.

[Original Source](https://unix.stackexchange.com/questions/269342/how-to-check-if-a-video-is-completely-downloaded/280567#280567)
