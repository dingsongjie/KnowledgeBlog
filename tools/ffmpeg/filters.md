# filters

#### drawtext

```bash
ffmpeg -i inputClip.mp4 -vf "drawtext=text='My text starting at 640x360':x=640:y=360:fontsize=24:fontcolor=white" -c:a copy output.mp4
```

#### noise

```bash
ffmpeg -i inputClip.mp4  noise=alls=20:allf=t+u -vf output.mp4
```

#### bit-noise

```bash
ffmpeg -i inputClip.mp4 -bsf noise=1000000  output.mp4
```

#### draw-box

```bash
 ffmpeg -i 1.mp4 -vf "drawbox=y=10:color=black@0.03:width=iw:height=128:t=fill,drawbox=y=ih/PHI:color=black@0.03:width=iw:height=128:t=fill,drawbox=y=ih-50:color=white@0.05:width=iw:height=50:t=fill"  internal.mp4
```
