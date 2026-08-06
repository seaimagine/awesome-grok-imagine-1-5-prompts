# Grok Imagine 1.5 Prompting Guide

This guide explains how to turn a creative idea into a controllable short-video prompt for Grok Imagine Video 1.5.

## 1. Choose the right workflow

| Workflow | Use it when | Prompt emphasis |
|---|---|---|
| Text-to-video | You need a new scene and can accept exploratory visual design | Subject, environment, composition, action, style |
| Image-to-video | The first frame and identity already look right | Motion, camera, physics, audio, invariants |
| Reference-to-video | One or more images should guide identity or visual language without acting strictly as frame one | Which reference controls which subject or detail |
| Video editing | The source timing and composition should remain, but selected visual properties must change | “Change only X; preserve Y” |
| Video extension | You need a continuation from the source video's final state | Starting state, direction, unresolved action, continuity |

Do not combine `image` and `reference_images` in one API generation request. Select the workflow that best matches the job.

## 2. Budget the timeline before writing details

A short clip needs visual breathing room. A reliable starting point is:

| Duration | Recommended structure |
|---:|---|
| 1–4s | One action or seamless loop |
| 5–8s | Setup → action → reaction |
| 9–12s | Three clear beats with one motivated cut |
| 13–15s | Mini story with setup, development, payoff and final hold |

If a spoken line takes four seconds, do not place three other key actions in the same four seconds. Read dialogue aloud at the intended pace before finalizing the timeline.

## 3. Describe identity once, then protect it

Start with a compact subject lock:

```text
SUBJECT LOCK: A fictional adult bicycle messenger with a round face, short black curls, rust-orange rain shell, charcoal trousers, silver helmet, and one navy delivery bag. Keep face, hair, clothing, bag, bicycle geometry, colors, and left-to-right travel direction unchanged.
```

For a product reference:

```text
Preserve the exact silhouette, dimensions, material, color, button layout, seams, label placement, and count of the supplied product. Do not redesign, simplify, decorate, duplicate, or add controls.
```

Avoid repeating a slightly different full description in every shot. Contradictory redescriptions cause drift.

## 4. Write physical motion, not abstract intensity

Weak:

```text
The runner moves dynamically and the cape looks epic.
```

Stronger:

```text
The runner plants the right foot, shifts weight forward, and accelerates. The heavy cape lags half a beat behind the torso, stretches under air resistance, then settles toward the center line after each stride.
```

Useful physical variables:

- **Mass:** light paper, heavy steel, dense wool, full glass bottle.
- **Contact:** shoe grips wet track, hand closes around handle, cup touches table.
- **Inertia:** object continues after the character stops; vehicle decelerates over distance.
- **Material response:** brittle caramel fractures; viscous serum stretches; damp fabric clings.
- **Environment:** particles and clothing share the same wind; shadows follow the same light.

## 5. Give the camera one job per beat

Use camera motion to reveal information or follow action:

- slow push-in for recognition or tension;
- lateral track for running, driving, or product assembly;
- restrained arc for an object reveal or musical ensemble;
- locked camera for loops, comedy timing, architecture, or transformations;
- focus pull to shift attention without cutting.

Avoid impossible stacks such as “drone shot, handheld close-up, 360-degree orbit, crash zoom, and FPV dive” inside three seconds.

## 6. Direct native audio as separate layers

```text
AUDIO:
- Ambience: quiet apartment at dawn, distant traffic through a closed window.
- Foley: bottle lock, button click, short carbonation hiss, pour into glass.
- Dialogue: Creator says, "That is actually crisp," with an amused, conversational delivery and natural lip sync.
- Music: none.
```

For spoken dialogue:

- quote the exact words;
- name the speaker;
- specify delivery and volume;
- keep the line short enough for the assigned time;
- state whether the voice is on-screen, off-screen, narration, radio, or phone-filtered;
- do not ask the mouth to move during voiceover.

## 7. Use negative constraints diagnostically

A compact avoid block is more helpful than a giant generic negative prompt.

```text
AVOID: face drift, clothing changes, duplicated cups, floating feet, changing light direction, random cuts, readable signs, logos, subtitles, watermark.
```

Tie constraints to likely failure modes in the scene:

- group scene → duplicated people, character swaps;
- product demo → geometry drift, extra controls, changing labels;
- hand close-up → extra fingers, lost contact, object clipping;
- action → weightless movement, sliding feet, broken screen direction;
- liquid → changing volume, impossible splash direction;
- architecture → bending walls, extra openings, floating furniture;
- dialogue → long line, speaker confusion, robotic mouth motion.

## 8. Iterate one variable at a time

Use a focused revision:

```text
Keep the subject, composition, camera path, timing, lighting, and audio unchanged. Revise only the landing: both feet contact the roof in sequence, knees compress under weight, two nearby tiles crack, and the scarf settles after the body stops.
```

Changing story, camera, wardrobe, lighting, audio, and duration at once makes it difficult to learn which instruction improved or damaged the result.

## 9. Resolution and ratio strategy

- Use `480p` for fast composition and timing drafts.
- Use `720p` for review and reference-to-video delivery.
- Use `1080p` for final text-to-video or image-to-video when detail matters.
- Image-to-video defaults to the input image's ratio. If you override the ratio, the source may be stretched; prepare the reference at the intended delivery ratio instead.
- Video editing keeps the source ratio and duration and is capped at 720p.

## 10. Final checklist

- Is the intended workflow explicit?
- Is the clip 1–15 seconds?
- Does each timeline beat have one dominant action?
- Can all dialogue fit at a natural speaking pace?
- Are subject and product invariants stated once and clearly?
- Are camera motion and focus physically possible?
- Do wind, gravity, contact, material and light directions agree?
- Is the final frame useful for an edit, loop, thumbnail, or end card?
- Are privacy, likeness, trademark and disclosure requirements addressed?

[Browse 40 prompts](../prompts/README.md) · [Use Grok Imagine 1.5 online](https://seaimagine.com/model/grok-imagine-1-5/) · [Main README](../README.md)
