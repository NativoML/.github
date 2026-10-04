<p align="center">
  <img src="https://raw.githubusercontent.com/Jibar-OS/JibarOS/main/assets/banner.png" alt="JibarOS" width="100%"/>
</p>

<p align="center">
  <a href="https://github.com/Jibar-OS/JibarOS/stargazers">
    <img src="https://img.shields.io/github/stars/Jibar-OS/JibarOS?style=social" alt="Stars" />
  </a>
  <img src="https://img.shields.io/badge/Android-16-34A853?logo=android&logoColor=white" alt="Android 16" />
  <img src="https://img.shields.io/badge/License-Apache%202.0-blue" alt="Apache 2.0" />
  <img src="https://img.shields.io/badge/Status-pre--1.0-orange" alt="pre-1.0" />
</p>

<p align="center">
  <a href="https://www.loom.com/share/a4de8aa1666e4b9a8efa128f98b7f16c">
    <img src="https://cdn.loom.com/sessions/thumbnails/a4de8aa1666e4b9a8efa128f98b7f16c-7826565414152998-full-play.gif"
         alt="v0.6.9 Fire All demo — Loom"
         width="720"/>
  </a>
</p>

# JibarOS

**An Android 16 fork where AI is a platform primitive, not an app feature.**

Twelve AI capabilities — text completion, translation, embeddings, classification, rerank, transcription, synthesis, VAD, image embeddings, description, detection, OCR — exposed to every app on the device through a single binder AIDL. One system service. One native daemon. Four pluggable backends. Pooled residency. Per-UID rate limits. Priority-aware scheduling. OEM-configurable per capability.

Models load once at the platform tier and are shared across every app that asks. Runtime infrastructure, not a chatbot. The closest mental model is **"a kernel for on-device inference."**

Named after Puerto Rico's *jíbaros* — rural folk, known for resilience and self-sufficiency. Models and runtime live on the device, work offline, no cloud account required.

> ⭐ [**Star the main repo**](https://github.com/Jibar-OS/JibarOS) — it's the cheapest signal that on-device AI belongs at the platform tier.

## Start here

👉 **[github.com/Jibar-OS/JibarOS](https://github.com/Jibar-OS/JibarOS)** — the main repo. README, architecture diagram, `default.xml` manifest, and the `docs/` directory with capability/knob/SDK/model/build guides.

## The runtime surface

OIR (Open Intelligence Runtime) is the inference layer. Twelve capabilities, permissions-gated:

| Capability | Shape | Reference backend |
|---|---|---|
| `text.complete` / `text.translate` | TokenStream | Qwen 2.5 (llama.cpp) |
| `text.embed` | Vector | MiniLM-L6-v2 (llama.cpp) |
| `text.classify` / `text.rerank` | Vector | OEM-supplied ONNX |
| `audio.transcribe` | TokenStream | whisper.cpp |
| `audio.synthesize` | AudioStream | Piper (ONNX Runtime) |
| `audio.vad` | RealtimeBoolean | Silero (ONNX Runtime) |
| `vision.embed` | Vector | SigLIP (ONNX Runtime) |
| `vision.describe` | TokenStream | libmtmd (LLaVA / SmolVLM / …) |
| `vision.detect` | BoundingBoxes | RT-DETR (ONNX Runtime) |
| `vision.ocr` | BoundingBoxes | OEM-supplied det+rec pair |

Full details in [`JibarOS/docs/CAPABILITIES.md`](https://github.com/Jibar-OS/JibarOS/blob/main/docs/CAPABILITIES.md).

## What's in this org

**Core**
- [`JibarOS`](https://github.com/Jibar-OS/JibarOS) — main: manifest + docs
- [`oird`](https://github.com/Jibar-OS/oird) — native inference daemon (C++)
- [`oir-framework-addons`](https://github.com/Jibar-OS/oir-framework-addons) — platform service + AIDL (Java)
- [`oir-patches`](https://github.com/Jibar-OS/oir-patches) — 5 small patches to upstream AOSP (69 lines)
- [`oir-sdk`](https://github.com/Jibar-OS/oir-sdk) — Kotlin SDK for apps
- [`oir-demo`](https://github.com/Jibar-OS/oir-demo) — OirDemo Mission Control reference app
- [`oir-vendor-models`](https://github.com/Jibar-OS/oir-vendor-models) — reference model bundle + fetch script
- [`device_google_cuttlefish`](https://github.com/Jibar-OS/device_google_cuttlefish) — reference device tree

**External backend forks**
- [`platform_external_llamacpp`](https://github.com/Jibar-OS/platform_external_llamacpp)
- [`platform_external_whispercpp`](https://github.com/Jibar-OS/platform_external_whispercpp)
- [`platform_external_onnxruntime`](https://github.com/Jibar-OS/platform_external_onnxruntime)

## AAOSP → JibarOS

Builds on [**AAOSP**](https://github.com/rufolangus/AAOSP), the earlier Android 15 fork that first put an LLM inside `system_server` as a platform service and introduced MCP tool-calling at the manifest layer. JibarOS extends that "AI at the platform tier" pattern from one-LLM-for-tool-calling to a general multi-backend inference layer on Android 16.

Apache 2.0. Pre-1.0. Validated on Android 16 Cuttlefish with SELinux Enforcing.
