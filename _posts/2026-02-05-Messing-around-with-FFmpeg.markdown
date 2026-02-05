---
layout: post
title: "Messing around with FFmpeg"
date:   2026-02-05 16:08 +0100
categories: cli tools
---

I decided to learn some FFmpeg. I was interested in how to encode videos to
different formats since that's the most common task I would normally do in a
video editor such as Kdenlive. As it turns out this is pretty easy due to
FFmpeg automatically detecting video formats by their file extension.

```sh
ffmpeg -i input.mp4 -c copy output.mkv
```

You can also do

```sh
ffmpeg -i input.mp4 output.mkv
```
though this will re-encode the video which is slower,more expensive and results
in quality loss according to the FFmpeg
docs[\[1\]](https://ffmpeg.org/ffmpeg.html#Streamcopy).

I decided to have some fun and tried to mix together audio and video streams. I
even created a broken file that would play a different video stream in Mpv than
the one in FFplay, unfortunately I do not remember the command for that. I have
found out how to create a file with the video of one file and the audio of
another file.

```sh
ffmpeg -i "input1.mp4" -i "input2.mp4" -map 0:0 -map 1:1 -c copy Output.mp4
```

It seems that the first number indicates which file to get streams
from(starting from 0). So this gets the video stream(:0) from file 0 and gets
the audio stream(:1) from file 1 then uses the copy encoder to encode it into
the output file.

I've of course yet to understand everything, the documentation is quite long. I
has been quite fun using what abominations come out from it and actual use
cases. FFplay is also an alright multimedia player when I need one quickly, Mpv
is still my favourite.

Sources:

\[1\](<a href="https://ffmpeg.org/ffmpeg.html#Streamcopy">https://ffmpeg.org/ffmpeg.html#Streamcopy<a/>)

Software mentioned:

[FFmpeg](https://ffmpeg.org/)

[Mpv](https://mpv.io/)
