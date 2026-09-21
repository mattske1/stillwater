# Stillwater

Seamless photorealistic ambient nature loops — water, stone, mist — made to sit
under chilled-out music on YouTube and social media.

Stillwater is a product of **Koryuai**, written by **Mattske** with agentic
support for **Edged Out Records**, and given away for free here for independent
artists looking to create quick visuals for their music to make it eye-catching
on YouTube and social media platforms.

## How it works

Three stages, each one replaceable:

1. **Still** — `still.py` generates a photorealistic long-exposure-style scene
   with FLUX.1-schnell (free HuggingFace Inference API). Start from one of the
   prompts in `scenes/`, or write your own: rock sculpture shape + screen
   placement, water source and speed, time of day, light and mood.
2. **Animate** — `animate.py` brings the still to life with the free Wan 2.2
   image-to-video HuggingFace Space. Static camera, continuous water and mist
   motion, no cuts. Output is a ~5 second clip.
3. **Weave** — `weave.py` chains copies of the clip with crossfades into a
   seamless loop of any exact length, then crossfades the tail back into the
   head so the loop point is invisible. Water is forgiving — the weave hides
   the repetition.

## Quickstart

```bash
pip install -r requirements.txt
# ffmpeg must be installed: https://ffmpeg.org/download.html
# No accounts or API keys needed — both AI services are free hosted
# HuggingFace Spaces. (Set HF_TOKEN if you have one and want a
# shorter queue on the animation step.)

# 1. still
python3 still.py --prompt "$(head -1 scenes/dawn-cairn.txt)" --out still.png

# 2. animate (a few minutes on the free queue)
python3 animate.py --still still.png --out clip.mp4

# 3. weave a 60-second seamless loop
python3 weave.py --clip clip.mp4 --target 60 --out stillwater-60s.mp4
```

The 15-second demo in `demo/` was made exactly this way — same scripts, same
free services, nothing you can't run yourself right now.

## Tips

- **Static camera is the whole trick.** Tell the animator the camera doesn't
  move, and the weave becomes invisible.
- **Water sources that work:** waterfalls, springs, cascades — anything flowing
  and continuous. Avoid pipes and spouts; they read wrong.
- **No day/night transitions** inside a single loop — pick one light and stay
  in it.
- Longer crossfades hide better for water; `weave.py` solves the fade length
  automatically to hit your exact target.

## License

MIT — free for whatever you want to make with it.
