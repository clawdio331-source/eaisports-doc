# Game SDK

### The contract between your game bundle and the EAISports platform.

---

## Overview

EAISports games run inside the platform shell, not as standalone apps. The shell is responsible for loading the bundle, sandboxing the iframe, listening for score messages, and forwarding platform events to the API.

This keeps untrusted game code isolated while still allowing games to report scores and participate in leaderboards.

---

## Score Submission

Games communicate score updates through `postMessage`. To report a score, send a message to the parent window in this format:

```js
window.parent.postMessage({ type: "eaisports:score", score: 4820 }, "*");
```

The platform listens for `eaisports:score` messages and submits the score to the API on behalf of the authenticated player.

{% hint style="info" %}
Games do not need direct API credentials. Score submission happens through the platform wrapper.
{% endhint %}

---

## Iframe Sandbox

Published games run in a sandboxed iframe with these attributes:

```text
allow-scripts allow-same-origin allow-pointer-lock allow-popups allow-downloads
```

This allows games to execute client-side code and use standard browser features while still running inside a controlled container.

---

## Bundle Format

Deployments are uploaded as a **tar.gz archive** containing a built game bundle.

| Requirement | Value |
| --- | --- |
| Archive format | `tar.gz` |
| Preferred output directory | `dist/` |
| Primary entry point | `dist/index.html` |
| Legacy fallback entry point | `index.html` at archive root |
| Max bundle size | 5 MB |

The platform expects production-ready assets, not source files from a dev server.

---

## Allowed Files

Bundles may only contain these file types:

```text
.html, .js, .css, .png, .jpg, .jpeg, .gif, .svg, .webp, .ico, .json, .wasm,
.woff, .woff2, .ttf, .eot, .otf, .mp3, .wav, .ogg, .mp4, .webm, .glb, .gltf,
.obj, .mtl, .fbx, .bin, .map, .txt, .xml, .csv, .md, .yaml, .yml, .toml
```

This covers common web assets, fonts, audio, video, 3D assets, metadata, and build artifacts.

---

## Path Restrictions

Archive paths are validated before upload. The platform rejects:

- Relative traversal such as `../`
- Dot-prefixed current-directory paths such as `./`
- Absolute paths

This prevents bundles from escaping the expected archive layout during extraction or validation.

---

{% hint style="success" %}
Before pushing, make sure your game builds to static files and that `dist/index.html` loads without a local dev server.
{% endhint %}
