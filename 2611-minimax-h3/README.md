# MiniMax H3 Image in ComfyUI: 5 tips, tested and explained

Workflows from the JanRT Studio video ([watch on YouTube](YOUTUBE_LINK)). Both are the official ComfyUI templates, set up the way the video ends: smaller model files that run on a 16 GB GPU, the prompt enhancer off, and a how-to note on the canvas.

| File | What |
|---|---|
| `minimax_h3_t2i.json` | Text to image at 16 MP: the Paris portrait from the video (seed 42) |
| `minimax_h3_edit.json` | Edit with one line: the black satin gown edit from the video (seed 7) |
| `minimax_h3_t2i.png`, `minimax_h3_edit.png` | The result of each; the workflow is saved inside the image. The edit is full size, pixel for pixel. The t2i picture is shown at 3/4 size to fit GitHub's 25 MB limit; the workflow makes it at the full 16 MP (3552 x 4736) |
| `minimax_h3_paris.png` | The edit's input picture: put it in ComfyUI's `input` folder |

**Download:** open a file and click **Download raw file** (no GitHub account needed), or use **Code > Download ZIP** for everything. Drag the `.json` or the `.png` onto the ComfyUI canvas.

## Before you run

- **Update ComfyUI** (made on ComfyUI 0.46.0, frontend 1.59.11).
- **Get the models** from https://huggingface.co/Comfy-Org/MiniMax-H3-Image:

| File | Folder | Size |
|---|---|---|
| `minimax_h3_image_pruned_w4a8.safetensors` | `models/diffusion_models/` | 12.6 GB |
| `qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors` | `models/text_encoders/` | 15.7 GB |
| `qwen3.5_9b_w4a8_gptq.safetensors` (prompt enhancer) | `models/text_encoders/` | 7.3 GB |
| `minimax_h3_image_vae_fp16.safetensors` | `models/vae/` | 1.2 GB |

  The templates ask for the int8 files (21 GB + 27 GB). These smaller ones are what we ran in the video.
- Tested on a 16 GB GPU with 32 GB RAM: 16 MP text to image in about 36 s, an 8 MP edit in about 35 s.

## The 5 tips

1. **Run it big.** 16 MP is native; 4 MP comes out crunchy.
2. **Stuck at 4 MP?** Plug an empty (black or white) image into `image_1`: smoother skin. At 16 MP it barely matters.
3. **LCM sampler** gives smooth, retouched skin. Stay on **euler** for real skin texture.
4. **Prompt enhancer off for clear edits:** about 35 s instead of 100, and nearly the same picture. On when your line is vague and you want ideas.
5. **Edit from the original.** Feeding a result back in drifts red and adds grain every round. Put all your changes in one line instead.

## More tips

- **Describe the result,** not a command: "The woman in &lt;Picture 1&gt; now wears ...".
- **Words in the picture go in "quotes"**, accents and all.
- **Two pictures?** Give each a role: "The woman in &lt;Picture 1&gt; is &lt;Subject 1&gt;. The taxi in &lt;Picture 2&gt; is &lt;Subject 2&gt;."
- Small text on a reference picture (a sign, a label) comes out garbled.

## Licences

The workflows are free to use. MiniMax H3 Image is under the [MiniMax Community License](https://github.com/MiniMax-AI/MiniMax-H3-Image/blob/main/LICENSE), which excludes some territories (EU, UK, Republic of Korea, USA). Read it before you use the model or its outputs: MiniMax offers a waiver to users with revenue up to US$1M ([apply here](https://platform.minimax.io/console/license/h3-image)).
