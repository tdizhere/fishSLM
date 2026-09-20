# Guppy web chat

An intentionally small, static chat page for the exported Guppy ONNX model. All inference happens in the visitor's browser through ONNX Runtime Web; the app sends neither messages nor model input to a server.

## Run locally

Use a local static server (opening `index.html` directly prevents browsers from loading the model safely):

```powershell
npx serve .
```

Then open the printed localhost URL. The first visit downloads the ONNX Runtime Web files from jsDelivr and caches them in the browser.

## Publish on GitHub Pages

1. Push this directory to a GitHub repository.
2. In **Settings → Pages**, select **Deploy from a branch**.
3. Select the branch and **/(root)**, then save.

Keep `model.onnx` and `tokenizer.json` beside `index.html` when deploying. The site has no build step.

## Runtime choices

- Tries WebGPU first, then WebAssembly SIMD as a compatible fallback.
- Limits each response to 42 tokens and keeps 86 prompt tokens, respecting Guppy's 128-token context limit.
- Uses a small in-page ByteLevel-BPE tokenizer, avoiding a second machine-learning runtime download.
