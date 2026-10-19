# ToAPIs · Lower-cost baibot image guide

Original baibot media examples with three image models.

[中文](README_zh-CN.md) · [Model & pricing](https://go2v.toapis.com/1019_bai_g) · [Upstream](https://github.com/etkecc/baibot)

**Community guide operated by ToAPIs.** The validated boundary is: Existing OpenAI-compatible image provider via loopback bridge; Matrix delivery/encryption pending. Individual project UI acceptance is listed below.

## Demo

![Three image models and their dated prices](social/image-comparison-en.png)

## Model pricing and case amounts

Tested on 2026-10-19. Sorted from low to high by the displayed case amount. Image amounts marked **Quoted** are current configured per-request rates, not task-confirmed net settlements. Video amounts use settled API receipts.

| Model / tested preset | Type | Case amount / quote | Applicable model rate | Fee evidence |
|---|---|---:|---|---|
| gpt-image-2(VIP)<br>low / 1K | image | Quoted $0.0019 | $0.0019/image | Matched current rate; individual task billing unavailable; same-model batch logs recorded separately |
| gpt-image-2<br>1K | image | Quoted $0.015 | $0.015/image | Matched current rate; individual task billing unavailable; same-model batch logs recorded separately |
| gpt-image-2.5-flare<br>high / 1K | image | Quoted $0.0225 | $0.0225/image | Matched current rate; individual task billing unavailable; same-model batch logs recorded separately |

`gpt-image-2(VIP)` starts at **$0.0019/image**; this guide uses **low / 1K at $0.0019/image**. The API ID is `gpt-image-2-vip`. Prices apply to the shown configuration; requested 1K does not guarantee a fixed pixel size. Original output dimensions are in each evidence file.

Seedance token rates and case USD/s have different units. The clip fee excludes its separately listed first-frame image. Token-rate estimates do not lock a final charge.

## Reuse

Python 3.10+; Node.js 22+ only for the optional MCP Image client. Copy `.env.example` to a private `.env`, configure your Key and a separate random local bridge token of at least 24 characters. Keep both private.

```bash
python run_case.py --job jobs/gpt-image-2-vip.json
# Review the current quote, then deliberately submit once:
python run_case.py --job jobs/gpt-image-2-vip.json --live
# Optional OpenAI-compatible bridge, loopback only:
python bridge.py
```

[Project-specific configuration and limits](integration/README.md). Saved state resumes the same task. A lost submit response stops for reconciliation; it is not an instruction to submit again. Use a new `run_id` only for a deliberate new paid example.

The server queries `/v1/pricing` with the same generation Key, submits to `/v1/images/generations` or `/v1/videos/generations`, polls the corresponding task path, and reads `billing` when available. It returns PNG/base64 to synchronous image consumers and adapts the supported multipart image-to-video route. Unsupported edit, chat and speech routes fail explicitly.

## Tested scope

[Detailed acceptance notes](ACCEPTANCE.md) · [Public evidence](evidence/) · [Input jobs](jobs/) · [Provider/recipe](integration/)

Inspected upstream revision: [`5a9037cbac5d`](https://github.com/etkecc/baibot/commit/5a9037cbac5d03ae4f5b1b55601cd40a44f6c09c). Generated assets and API-boundary checks do not establish full upstream app integration or maintainer endorsement.

## Original prompt

```text
Square friendly flat illustration for a private community chat: a small orange robot tending three green plants on a balcony above a bright seaside town, clear simple shapes, warm coral and cream palette, approachable original editorial artwork, no brand, no letters, no text, no watermark.
```

## References

- [Upstream project](https://github.com/etkecc/baibot)
- [Pricing and actual charges](https://docs.toapis.com/docs/en/api-reference/account/pricing)
- [Try the matching image model](https://go2v.toapis.com/1019_bai_g)
