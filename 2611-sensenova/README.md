# SenseNova U1.6 in ComfyUI: the image model that proofreads itself

Workflows from the JanRT Studio video. SenseNova U1.6 draws an image, reads it back, writes itself notes on what's wrong with the text, and draws it again.

| File | What |
|---|---|
| `sensenova_t2i_poster.json` | Text to image with self-correction: the movie poster from the video |
| `sensenova_edit.json` | Edit with a prompt: the coat-and-mug edit from the video |
| `sensenova_t2i_poster.png`, `sensenova_edit.png` | The result of each; the workflow is saved inside the image |
| `sensenova_rooftop.png` | The edit's input picture: put it in ComfyUI's `input` folder |

**Download:** open a file and click **Download raw file** (no GitHub account needed), or use **Code > Download ZIP** for everything. Drag the `.json` or the `.png` onto the ComfyUI canvas.

## Before you run

- **Update ComfyUI.** SenseNova needs a recent version (made on ComfyUI 0.46.0, frontend 1.59.11).
- **Get the model** (each workflow's own note lists the files and the folder each goes in): https://huggingface.co/Comfy-Org/SenseNova-U1 (the checkpoint and the 8-step Turbo LoRA).
- Runs on a 16 GB GPU. With Turbo on, a poster takes about 40 s and an edit about 16 s.

## How to use

**Text to image**
1. **Self-Correction on.** After the first image the model reads it back and writes notes: boxes on a 0–1000 grid plus what the text should say. **Preview as Text** shows them. If it finds nothing, it looks once and stops.
2. **Turbo on, prompt rewriter off.** The rewriter needs its own text encoder, a separate download.
3. **Quote every line of text** you want. Mistakes show up in small print: credits, ingredients, fine print.
4. **It only checks text**, not counts or clock hands, and a fix can drop words. Seed 5 does exactly that: the second pass fixes two credit lines and loses the music credit, as in the video. Look at the second image too.

**Edit**
1. Load your picture and keep **Resize Image/Mask at 2 megapixels**. A big, sharp 4 MP photo comes out crunchy.
2. Say what to change and what to keep (face, hair, pose, background).
3. To fix the text in another model's image, quote every line as it should read and turn **Self-Correction on**.

## Licences

The workflows are free to use. SenseNova U1.6 is Apache 2.0.
