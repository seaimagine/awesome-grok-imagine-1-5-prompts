# Grok Imagine Video 1.5 API Quickstart

This page is a concise companion to the official xAI documentation. API behavior, access, regions, pricing, and limits can change; verify the current details before production use.

- [Official video generation documentation](https://docs.x.ai/developers/model-capabilities/video/generation)
- [Official model page](https://docs.x.ai/developers/models/grok-imagine-video-1.5)
- [Official pricing](https://docs.x.ai/developers/pricing)

## Model and configuration

| Setting | Current documented behavior |
|---|---|
| Model | `grok-imagine-video-1.5` |
| Duration | 1–15 seconds for generation |
| Aspect ratios | `1:1`, `16:9`, `9:16`, `4:3`, `3:4`, `3:2`, `2:3` |
| Resolution | `480p`, `720p`, `1080p` |
| Reference-to-video | Up to 720p |
| Video editing | Keeps input duration and aspect ratio; source capped at 8.7s; output capped at 720p |
| Audio | Generated videos include an audio track by default |

## Text-to-video with Python SDK

Set `XAI_API_KEY` in your environment; do not hardcode it in source control.

```python
import os
import xai_sdk

client = xai_sdk.Client(api_key=os.getenv("XAI_API_KEY"))

video = client.video.generate(
    model="grok-imagine-video-1.5",
    prompt=(
        "A small orange maintenance robot plants four broad feet on a wet "
        "harbor deck and slowly lifts a fallen steel beam. Heavy rain, "
        "believable hydraulic weight, synchronized machinery and water sounds."
    ),
    duration=10,
    aspect_ratio="16:9",
    resolution="720p",
)

print(video.url)
```

The SDK handles polling for this high-level call.

## Text-to-video with REST

Generation is asynchronous. First create a request:

```bash
curl -X POST https://api.x.ai/v1/videos/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $XAI_API_KEY" \
  -d '{
    "model": "grok-imagine-video-1.5",
    "prompt": "A tiny felt baker stops a giant croissant from rolling off a wooden table using a red thread pulley. Original stop-motion scene, playful kitchen foley, no text or logos.",
    "duration": 8,
    "aspect_ratio": "16:9",
    "resolution": "720p"
  }'
```

The response contains a `request_id`. Poll it:

```bash
curl -X GET "https://api.x.ai/v1/videos/REQUEST_ID" \
  -H "Authorization: Bearer $XAI_API_KEY"
```

Expected lifecycle states are `pending`, `done`, `expired`, and `failed`. Completed video URLs are temporary; download or process the result promptly if you need to retain it.

## Request modes

| Mode | REST input shape |
|---|---|
| Text-to-video | `prompt` |
| Image-to-video | `prompt` + `image` |
| Reference-to-video | `prompt` + `reference_images` and/or supported preset `reference_audios` |
| Edit video | `/v1/videos/edits` + `video` |
| Extend video | `/v1/videos/extensions` + `video` |

Only one mode can be active per request. In particular, do not mix `image` and `reference_images`.

For supported file inputs, URL formats, preset voices, regional availability, and current request schemas, use the official workflow pages linked from the [video generation documentation](https://docs.x.ai/developers/model-capabilities/video/generation).

## Production checklist

- Store the API key in a secret manager or environment variable.
- Poll with bounded timeouts and backoff rather than an unbounded tight loop.
- Handle `failed`, `expired`, authentication, permission, and rate-limit responses.
- Record model name, prompt version, settings, request ID, and usage metadata.
- Download temporary output URLs promptly and validate media before publishing.
- Moderate prompts, input media, and generated output according to your use case.
- Obtain consent for real faces, voices, personal media, trademarks, and private locations.

[Browse prompt examples](../prompts/README.md) · [Use Grok Imagine 1.5 online](https://seaimagine.com/model/grok-imagine-1-5/) · [Main README](../README.md)
