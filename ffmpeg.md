## Check resolution
from https://superuser.com/questions/841235/how-do-i-use-ffmpeg-to-get-the-video-resolution
```
$ ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=s=x:p=0 input.mp4
```

## Count frames
from https://stackoverflow.com/questions/2017843/fetch-frame-count-with-ffmpeg
```
$ ffprobe -v error -select_streams v:0 -count_packets -show_entries stream=nb_read_packets -of csv=p=0 input.mp4
```

## Crop video (in xy)
from https://video.stackexchange.com/questions/4563/how-can-i-crop-a-video-with-ffmpeg
```
$ ffmpeg -i in.mp4 -filter:v "crop=out_w:out_h:x:y" out.mp4
```

## Clip video (in time)
from https://superuser.com/questions/138331/using-ffmpeg-to-cut-up-video
```
ffmpeg -ss 00:00:30.0 -i input.wmv -c copy -t 00:00:10.0 output.wmv
```
or, alternatively, 
```
ffmpeg -ss 30 -i input.wmv -c copy -t 10 output.wmv
```

