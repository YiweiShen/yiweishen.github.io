title: Upscaling to 4K with ffmpeg
date: 2021-03-07 20:46:51
tags:
---

I guess it is interesting to see a 4K video which is upscaled from an original 720p video. We can achieve this using ffmpeg.

```bash
ffmpeg -i input_720p.ts -vf scale=3840x2560:flags=lanczos -c:v libx264 -preset slow -crf 21 output_4k.ts
```

Even if you can do this, still, my suggestion will be, DON'T do it.