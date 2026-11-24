# Layout with bounding boxes: FLUX 3 Klein and MOSS-Image in ComfyUI

Workflows from the JanRT Studio video "Draw boxes, get the picture". Draw boxes, describe what goes in each, and the model puts it there.

| File | Model |
|---|---|
| `layout_boxes_klein.json` | FLUX 3 Image Klein (base) |
| `layout_boxes_moss.json` | MOSS-Image (SFT) |
| `layout_boxes_klein.png`, `layout_boxes_moss.png` | The result of each; the workflow is saved inside the image |

**Download:** open a file and click **Download raw file** (no GitHub account needed), or use **Code > Download ZIP** for everything. Drag the `.json` or the `.png` onto the ComfyUI canvas.

## Before you run

- **Turn on Nodes 2.0** (ComfyUI logo menu > Nodes 2.0). The box editor only works there.
- **Get the models.** Each workflow's own note lists the files and the folder each goes in:
  - FLUX 3 Image Klein: https://huggingface.co/black-forest-labs/flux-3-image-klein-comfy (gated: accept the licence on the page first)
  - MOSS-Image: https://huggingface.co/Comfy-Org/MOSS-Image
- Made on ComfyUI 0.46.0, frontend 1.59.11, on a 16 GB GPU. Seed 42 gives the images in the video.

## How to use

1. Draw in **Create Bounding Boxes**. Turn Grid off so boxes don't snap. Draw the background first and the foreground last, and give each box a short description. A `text` box renders the words you type.
2. Describe the scene in the layout node's caption. The node adds your boxes to it as text.
3. **Keep the prompt upsampler (Klein) and the prompt enhancer (MOSS) off.** Klein's upsampler is told to remove coordinates, so with it on your boxes are rewritten away.
4. Run. The second Create Bounding Boxes takes the result as its background: open it full screen to see your boxes over the image.

Very small boxes often come out empty (Black Forest Labs' bounding-box guide).

## Licences

The workflows are free to use. The models have their own licences: FLUX 3 Image Klein, FLUX Kommunity License (read it before any commercial use); MOSS-Image, Apache 2.0.
