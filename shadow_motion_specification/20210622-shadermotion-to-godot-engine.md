# Convert ShaderMotion to be played in Godot Engine

## Context and Problem Statement

We want a better way of importing animations to Godot Engine. There no common way to exchange motion from other places to Godot and have them work interchangably on different characters.

## Describe the proposed option and how it helps to overcome the problem or limitation

ShaderMotion files in video format provide a good way to record motion. We want the ability to play it back in Godot Engine onto a VRM character.

## Describe how your proposal will work, with code, pseudo-code, mock-ups, or diagrams

Install youtube-dl and ffmpeg with scoop

`scoop install youtube-dl ffmpeg`

Convert ShaderMotion videos into webm VP9.

`youtube-dl https://www.youtube.com/playlist?list=NNNN --audio-format wav --format webm --recode-video webm`

Crop the preview frame of the video for the left and the right side.

```
rm -rf shader_motion_character_00
mkdir -p shader_motion_character_00
ffmpeg -i "NNNN.webm" "-filter:v" "crop=in_w*(1-0.925):ih:0:0,fps=60,scale=24x180:flags=lanczos+full_chroma_inp" shader_motion_character_00.webm

rm -rf shader_motion_character_01
mkdir -p shader_motion_character_01
ffmpeg -i "NNNN.webm" "-filter:v" "crop=in_w*(1-0.925):in_h:in_w:in_h,fps=60,scale=24x180:flags=lanczos+full_chroma_inp" shader_motion_character_01.webm
```

See frame layout in `frame_layout.md`.

## Positive Consequences <!-- optional -->

- Can interchange motions

## Negative Consequences <!-- optional -->

- Complexity

## If this enhancement will not be used often, can it be worked around with a few lines of script?

Not trivial.

## Is there a reason why this should be core and done by us?

The ability to give motion to 3d characters or NPCS is important.

The ability to interchange pose is important.

## References <!-- optional -->

- https://motion.chibifire.com
- https://github.com/ytdl-org/youtube-dl
- https://github.com/FFmpeg/FFmpeg

## Derivative License

Copyright (c) 2020-2021 V-Sekai contributors.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
