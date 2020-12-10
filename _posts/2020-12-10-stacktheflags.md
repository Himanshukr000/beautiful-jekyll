---
layout: post
published: true
title: STACKTHEFLAGS
date: '2020-12-10'
image: /img/STACKTHEFLAGS/logo.png
---
# STACK THE FLAGS

![image](https://play.cat2.stf-2020.alttablabs.sg/img/main.776521d4.png)

New day, New CTF and New Writeup..... Hahahaha

![image](https://cdn.discordapp.com/attachments/773063605142552596/785159129223266315/unknown.png)

### Scoreboard FLEX ^^ 
#### [ByteForc3](https://ctftime.org/team/71631) ftw



## Walking Down a Colorful Memory Lane

![image](/img/STACKTHEFLAGS/1.png)

Just another typical Memory Forensics challenge. So starting with volatility `imageinfo`.

![image](/img/STACKTHEFLAGS/2.png)

and next was `pslist` to check the running process.

![image](/img/STACKTHEFLAGS/6.png)

Now seeing chrome running `chromehistory` was the next move.

![image](/img/STACKTHEFLAGS/4.png)

The highlighted part is the suspicious link that the user visited.
It was an image file:

`This_is_a_png_file.png: PNG image data, 64 x 1, 8-bit/color RGB, non-interlaced`
with no actual image. So the actual flag was in pixel values.

```python
from PIL import Image

f = Image.open('This_is_a_png_file.png','r')

pixels = []
width, height = f.size
for x in range(width):
	for y in range(height):
		pixel = f.getpixel((x,y))
		pixels.append(pixel)

flag = [chr(x) for sets in pixels for x in sets]
print(''.join(flag))
```

And this gave the flag right away.

 `zsteg`  also gave the flag.

 ![image](/img/STACKTHEFLAGS/5.png)

 ```govtech-csg{m3m0ry_R3dGr33nBlu3z}```

PS: We first blooded this challenge :)