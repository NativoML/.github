# JibarOS

**An Android-derivative OS with a built-in AI runtime at the platform layer.**

JibarOS is an AOSP fork that ships [Open Intelligence Runtime (OIR)](https://github.com/Jibar-OS/jibar-os/blob/main/docs/OVERVIEW.md) as a first-class system service — so any app on the device can call text, audio, and vision AI capabilities without bundling a model or a runtime.

Named after Puerto Rico's *jíbaros* — rural folk, known for resilience and self-sufficiency. Models and runtime live on the device, work offline, no cloud account required.

## Start here

👉 **[github.com/Jibar-OS/jibar-os](https://github.com/Jibar-OS/jibar-os)** — the main repo. README, quick-start, `default.xml` manifest, and the `docs/` directory with capability/knob/SDK/model/build guides.

## What is in this org

**Core**
- [`jibar-os`](https://github.com/Jibar-OS/jibar-os) — main: manifest + docs
- [`oird`](https://github.com/Jibar-OS/oird) — native inference daemon (C++)
- [`oir-framework-addons`](https://github.com/Jibar-OS/oir-framework-addons) — platform service + AIDL (Java)
- [`oir-patches`](https://github.com/Jibar-OS/oir-patches) — 5 small patches to upstream AOSP
- [`oir-sdk`](https://github.com/Jibar-OS/oir-sdk) — Kotlin SDK for apps
- [`oir-demo`](https://github.com/Jibar-OS/oir-demo) — OirDemo Mission Control reference app
- [`oir-vendor-models`](https://github.com/Jibar-OS/oir-vendor-models) — reference model bundle + fetch script
- [`device_google_cuttlefish`](https://github.com/Jibar-OS/device_google_cuttlefish) — reference device tree

**External backend forks**
- [`platform_external_llamacpp`](https://github.com/Jibar-OS/platform_external_llamacpp)
- [`platform_external_whispercpp`](https://github.com/Jibar-OS/platform_external_whispercpp)
- [`platform_external_onnxruntime`](https://github.com/Jibar-OS/platform_external_onnxruntime)

> Status: pre-1.0. Validated on Android 16 Cuttlefish. Licensed Apache 2.0.
