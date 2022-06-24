# filters

#### drawtext

```bash
ffmpeg -i inputClip.mp4 -vf "drawtext=text='My text starting at 640x360':x=640:y=360:fontsize=24:fontcolor=white" -c:a copy output.mp4
```
