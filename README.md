# UnivAQ_Stream

## Saves Microsoft Stream videos uploaded by UnivAQ.

This project was originally based on https://github.com/jacopo-j/PoliDown

Improvements in this fork:
 - UnivAQ autologin
 - Multithreading download through aria2c
 - Possibility to choose the video resolution


## PREREQS

* [**Node.js**](https://nodejs.org/it/download/): anything above v8.0 seems to work.
* [**aria2**](https://github.com/aria2/aria2/releases): this needs to be in your `$PATH` (for example, copy aria2c.exe to c:\windows). PoliDown calls `aria2c` with a bunch of arguments in order to improve the download speed.
* [**ffmpeg**](https://www.ffmpeg.org/download.html): a recent version (year 2019 or above), in [`$PATH`](https://www.thewindowsclub.com/how-to-install-ffmpeg-on-windows-10). On Windows, the [nightly build](https://ffmpeg.zeranoe.com/builds/win64/static/ffmpeg-20200309-608b8a8-win64-static.zip) is required.


## USAGE

* Clone this repo
* `cd` into the cloned folder
* `npm install` to install dependencies

Default usage:
```
$ node univaqstream.js --username NOMEUTENTE --videoUrls "https://web.microsoftstream.com/video/VIDEO-1"

$ node univaqstream.js -u NOMEUTENTE -v "https://web.microsoftstream.com/video/VIDEO-1"
```

Show options:
```
$ node univaqstream.js -h

Options:
  --version              Show version number                           [boolean]
  -v, --videoUrls                                             [array] [required]
  -u, --username         Nome utnete UnivAQ                  [string] [required]
  -p, --password                                                        [string]
  -o, --outputDirectory                             [string] [default: "videos"]
  -q, --quality          Video Quality [0-5]                            [number]
  -k, --noKeyring        Do not use system keyring    [boolean] [default: false]
  -h, --help             Show help                                     [boolean]
```

Multiple videos download:
```
Project was originally based on https://github.com/jacopo-j/PoliDown
$ node univaqstream.js -u NOMEUTENTE
    -v "https://web.microsoftstream.com/video/VIDEO-1"
                "https://web.microsoftstream.com/video/VIDEO-2"
                "https://web.microsoftstream.com/video/VIDEO-3"
```

Define default video quality [0-5] (avoid manual prompt for each video):
```
$ node univaqstream.js -u NOMEUTENTE -v "https://web.microsoftstream.com/video/VIDEO-1" -q 4
```

Output directory (relative or absoulte path):
```
$ node univaqstream.js -u NOMEUTENTE -v "https://web.microsoftstream.com/video/VIDEO-1" -o "/my/path/here"
```

Do not use system keyring to save the password:
```
$ node univaqstream.js -u NOMEUTENTE -v "https://web.microsoftstream.com/video/VIDEO-1" -k
```


You can omit the password argument. PoliDown will ask for it interactively and then save it securely in system's keychain for the next use.

## EXPECTED OUTPUT

```

Using aria2 version 1.35.0
Using ffmpeg version git-2020-03-06-cfd9a65 Copyright (c) 2000-2020 the FFmpeg developers

Launching headless Chrome to perform the OpenID Connect dance...
Navigating to STS login page...
Filling in Servizi Online login form...
We are logged in.

Start downloading video: https://web.microsoftstream.com/video/d1e6c909-3189-488f-8172-e88947249f02
Got required authentication cookies.
Looking up AMS stream locator...

Video title is: SALIONI ALBERTO  088805-FISICA TECNICA (712804)

[0] 320x180
[1] 480x270
[2] 640x360
[3] 960x540
[4] 1280x720
[5] 1920x1080
Choose the desired resolution: 5

03/10 20:47:14 [NOTICE] Downloading 898 item(s)

[...]

At this point Chrome's job is done, shutting it down...
Done!
```

The video is now saved under `videos/`, or whatever the `outputDirectory` argument points to.
