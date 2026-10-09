# reroot-models

Model artifacts for [Reroot](https://github.com/januwewalwala2005/reroot).
No source code lives here — only weights that are too large to ship inside
the application installer.

## Why this repo exists

Reroot's installer is ~256 MB. The Laya ONNX export is ~1.7 GB, so
bundling it would make the download roughly seven times larger for a
feature not every user reaches. Instead the app downloads the model once,
on first use, into a machine-level cache and verifies it against the
SHA-256 digests pinned in `packages/rust/inference/src/laya_download.rs`.

Hugging Face is the natural home for weights, but upstream
(`convaiinnovations/laya`) publishes only `model.safetensors`; there is no
ONNX to fetch. This repo hosts the export produced by Reroot's own
`scripts/laya/export_onnx.py`.

## Releases

| Tag | Contents |
|---|---|
| `laya-en-onnx-v1` | Laya `en` variant, opset 17. Max absolute logit difference vs the PyTorch reference: 1.25e-06. |

Tags are pinned, never `latest`: the digests in the application describe
exactly these artifacts, and a model changing underneath a released build
is not a feature.
