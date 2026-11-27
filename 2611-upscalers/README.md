# Three one-step upscalers in ComfyUI: Kandinsky ImageSR 2.0, Steppe, SeedVR2

Workflows from the JanRT Studio video ([watch on YouTube](YOUTUBE_LINK)), set up the way the video's live demo ends, each with a how-to note on the canvas.

| File | What |
|---|---|
| `upscalers_kandinsky.json` | Kandinsky ImageSR 2.0, x4, creativity 4: the portrait from the video. Needs our node pack (below) |
| `upscalers_steppe_krea2.json` | The official Krea 2 Turbo template with Steppe between KSampler and VAE Decode (inside the subgraph, seed 3). Needs our node pack |
| `upscalers_seedvr2.json` | The official SeedVR2 7B int8 template, x4, on the old photo from the video. Built in, no custom nodes |
| `upscalers_kandinsky.png`, `upscalers_steppe_krea2.png`, `upscalers_seedvr2.png` | The result of each; the workflow is saved inside the image. Steppe and SeedVR2 are full size. Kandinsky is shown at 3/4 size to fit GitHub's 25 MB limit; the workflow makes it at the full 3840 x 5120 |
| `upscalers_portrait.png`, `upscalers_oldscan.png` | The input pictures: put them in ComfyUI's `input` folder |

**Download:** open a file and click **Download raw file** (no GitHub account needed), or use **Code > Download ZIP** for everything. Drag the `.json` or the `.png` onto the ComfyUI canvas.

## Before you run

- **Update ComfyUI** (made on ComfyUI 0.46.0, frontend 1.59.11).
- **Install our node pack** for Kandinsky and Steppe: [ComfyUI-JanRT-Upscalers](https://github.com/JanRTstudio/ComfyUI-JanRT-Upscalers). In `ComfyUI/custom_nodes`, run:

  ```
  git clone --branch v0.1.0 https://github.com/JanRTstudio/ComfyUI-JanRT-Upscalers
  ```

  No git? On the pack's page, **Releases > v0.1.0 > Source code (zip)**, and unzip it into `ComfyUI/custom_nodes`. No `pip install` needed. Restart ComfyUI: the nodes are under **JanRT/upscale**. The pack's README has the hashes it checks.
- **Get the models:**

| File | Folder | Size | For |
|---|---|---|---|
| [Kandinsky ImageSR 2.0](https://huggingface.co/kandinskylab/Kandinsky-ImageSR-2.0): the `transformer` folder (3 shards + `config.json`) | `models/kandinsky_sr/Kandinsky-ImageSR-2.0/transformer/` | 10.2 GB | Kandinsky |
| [`ae.safetensors`](https://huggingface.co/Comfy-Org/z_image_turbo/tree/main/split_files/vae) (FLUX.1 VAE) | `models/vae/` | 335 MB | Kandinsky |
| [`steppe_wan_2_1_200M_1step.safetensors`](https://huggingface.co/TensorForger/Steppe-Wan2.1) | `models/latent_upscale_models/` | 445 MB | Steppe for Krea 2, Qwen-Image, Wan |
| [`steppe_flux_2_200M_1step.safetensors`](https://huggingface.co/TensorForger/Steppe-Flux.2) | `models/latent_upscale_models/` | 385 MB | Steppe for FLUX.2, FLUX 3 Klein, MOSS-Image (not used here) |
| [Krea 2 Turbo](https://huggingface.co/Comfy-Org/Krea-2): `krea2_turbo_fp8_scaled`, `qwen3vl_4b_fp8_scaled`, `qwen_image_vae`, and the template's style LoRA `krea2_darkbrush` | `models/diffusion_models/`, `text_encoders/`, `vae/`, `loras/` | 13.1 + 5.2 GB + 254 MB | the Steppe workflow |
| [SeedVR2](https://huggingface.co/Comfy-Org/SeedVR2): `seedvr2_7b_int8_convrot`, `seedvr2_ema_vae_fp16` | `models/diffusion_models/`, `models/vae/` | 8.3 GB + 501 MB | SeedVR2 |

- Tested on a 16 GB GPU with 32 GB RAM, on a 960 x 1280 picture: Kandinsky x2 13 s, x4 43 s; SeedVR2 7B x2 under 5 s, x4 16 s; Steppe 2x a couple of seconds on top of the render.

## Which one to use

1. **Making a picture with Krea, Qwen or FLUX.2? Add Steppe.** It's almost free.
2. **Fast and faithful, on any picture? SeedVR2.**
3. **Most real detail? Kandinsky.** Keep creativity low (0 to 4) on faces: 8 redraws more and can change a face.

## More tips

- **Steppe 4x:** chain two Steppe Upscale Latent nodes. On illustrations set hff to 0.6 on the second, or flat paint gets grainy. Use VAE Decode (Tiled), or the 4K decode fills 16 GB.
- **Steppe only takes latents** from its model families, so it can't fix an old photo. Use Kandinsky or SeedVR2 on pictures you already have.
- **SeedVR2:** skip the 3B model. It over-sharpens.
- **Kandinsky:** keep the loader on bf16. fp8 saves little on 16 GB and changes the output slightly.

## Licences

The workflows are free to use (MIT, like this repo). Kandinsky ImageSR 2.0 and Steppe are MIT, SeedVR2 is Apache 2.0, the FLUX.1 VAE is Apache 2.0. Krea 2 is under the [Krea 2 Community License](https://huggingface.co/krea/Krea-2-Turbo/blob/main/LICENSE.pdf): read it before you use the model or its outputs. The input pictures are AI images made for the video.
