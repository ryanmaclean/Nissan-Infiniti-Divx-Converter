# Nissan Infiniti Divx Converter
Quick and dirty python script to convert files downloaded from the internet to a Divx format that conforms to the Nissan/Infiniti Nav specifications

## The Specifications

The [Infiniti manual](https://owners.infinitiusa.com/content/manualsandguides/QX50/2016/2016-qx50-owner-manual.pdf) specifies the following regarding Divx playback: 

| File Types | | | 
| ---------------- | --------- | -------------------------------- |
| .divx, .avi | Video Codecs | DivX3, DivX4, DivX5, DivX6 |
| | Audio Codecs MP3 | MPEG2.5 Audio Layer3, AC3, LPCM |

## The ffmpeg Options

As found on [this instuctables page for Divx conversion](http://www.instructables.com/id/Play-Video-via-USB-on-Nissan-or-Infiniti-Vehicles-/) using a separate tool, we get the parameters needed for `ffmpeg` in order to create a compatible file. 

```
ffmpeg -i INPUTFILE OUTPUTFILE -f avi -r 29.97 -vcodec libxvid -vtag dx50 -vf scale=704:384 -aspect 16:9 -maxrate 1800k -b:v 1500k -qmin 3 -qmax 5 -bufsize 4096 -mbd 2 -bf 2 -trellis 1 -flags +aic -cmp 2 -subcmp 2 -g 300 -acodec libmp3lame -ar 48000 -b:a 128k -ac 2
```

## Parameters

The only thing we really need is the input filename - we assume a `.avi` file doesn't exist in the directory in which we run the script. Therefore, we take an input file from the command line, and stop if one doesn't exist. 

_ Note: if the destination `.avi` file exists, you'll be prompted with a `[y/N]` input, the default being `no`. _

### Example

```
nissan_infiniti_divx.py filename.mp4

Command to run: ffmpeg -i filename.mp4 filename.avi -f avi -r 29.97 -vcodec libxvid -vtag dx50 -vf scale=704:384 -aspect 16:9 -maxrate 1800k -b:v 1500k -qmin 3 -qmax 5 -bufsize 4096 -mbd 2 -bf 2 -trellis 1 -flags +aic -cmp 2 -subcmp 2 -g 300 -acodec libmp3lame -ar 48000 -b:a 128k -ac 2

[...]
```

## Installing ffmpeg

This script require ffmpeg, which can be installed as follows: 

### RPM-Based Distro

`sudo yum install ffmpeg`

### Debian-Based Distro

`sudo apt-get install ffmpeg`

### Windows

`choco install ffmpeg`

### macOS

`brew install ffmpeg`
