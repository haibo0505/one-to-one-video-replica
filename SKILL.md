---
name: one-to-one-video-replica
description: Analyze authorized reference videos, build measurable reconstruction blueprints, compile direct Seedance 2.5 prompt packages, and compare recreations. Use for 1:1 video replication, Seedance prompts, frame-level reverse engineering, shot matching, and difference correction.
---

# 1:1 Video Reconstruction

Treat the authorized reference as the visual and temporal baseline. Reduce perceptible differences through measurement and correction.

## Boundaries

- Preserve the reference unless the user requests a change.
- Label uncertain values as measured, estimated, inferred, or unknown. Never invent metadata, media labels, or model controls.
- A prompt cannot guarantee pixel equality; references and edit mode control more than text.
- Never submit paid or external generation without authorization.

## Route by requested deliverable

1. **Seedance Direct** — use the screenshot workflow: measure each shot, write fields, then a self-contained `Seedance提示词`.
2. **Reference Analysis** — for 拆解、分析、测量、蓝图, or an engineering report.
3. **Reshoot Blueprint** — for live-action reshooting or physical-set reconstruction.
4. **Difference Detection** — when both reference and recreated versions are supplied.

For mixed requests, measure internally and return Seedance Direct output. Hide the engineering report unless requested.

## Required playbook

For raw-video analysis, reshoot planning, or version comparison, read [references/frame-reconstruction-playbook.md](references/frame-reconstruction-playbook.md) completely. In Seedance Direct mode, use it internally; never dump frame tables into the prompt.

## Seedance Direct

### Step 1 — Choose one request shape

- **Text generation:** no media; cannot achieve 1:1.
- **Reference generation:** borrow action, camera, rhythm, layout, style, or timing.
- **Shot-anchor workflow:** each shot gets source range, first-frame anchor, scene/composition/subject/microexpression/action/background/camera, then one prompt; next shots reuse anchors.
- **Video edit:** retain the source timeline; change only named elements.
- **Video extend:** continue forward or backward from the named source boundary.

Do not ask when intent selects the shape. Split edit-then-extend into two prompts. Ask once only when ambiguity materially changes the request.

### Step 2 — Map real inputs

Give each used input one narrow role; preserve exact labels and never coin them. In Seedance Direct, state the role in the relevant shot block or prompt. If a platform field/label or binding is unknown, mark `NOT READY` after the shot blocks and name the missing item.

### Step 3 — Compile, do not copy

- Convert frame IDs and coordinates into visible actions and composition changes.
- Use measured source ranges in analysis headers. Inside a shot prompt use relative hold → action → peak → settle; never invent cuts.
- Describe camera by subject, start, direction, and end.
- Bind dialogue, beats, reveals, cuts, and action peaks only when supported; with audio, include verbatim text, timing, voice style, ambience and SFX in that prompt.
- Keep continuity to identity, count, product geometry, clothing, spatial relations, event order, and final state; reuse anchors across shots.
- When the user specifies target product count or colorways, lock them across every relevant shot. The source video's object count is only a motion/composition cue; never duplicate a target colorway just to fill its layout. Count visible instances before returning each shot.

### Step 4 — Return screenshot-style shot blocks

For **Seedance Direct**, output the fixed `【Seedance全局控制】` line below exactly once, as the first line of the entire response, before any title, explanation, time range, or shot field. Then return one block per shot in this form (plus a final `NOT READY` note only when required):

```text
【Seedance全局控制】纯净画面，无字幕、花字、水印、标识及任何可读文字；全部台词只生成声音；参考图中的原有文字不继承、不重绘。

[原始时间段]

场景：
构图：
主体：
微表情：
动作：
背景动态：
镜头：

Seedance提示词：
<一段可直接复制的完整提示词>
```

Use this line verbatim exactly once at the start of each Seedance Direct reply, including initial packages, multi-shot packages, partial shot revisions, text-only fallbacks, and generate/edit/extend prompts. This shared control applies to every shot and prompt in that reply. Do not repeat its marker or full sentence inside shot fields, individual `Seedance提示词`, additional prompt variants, or closing notes.

This clean-frame default overrides reference fidelity for visible text: omit source captions, typography, watermarks, logos, UI text, and writing on props or products. Preserve spoken dialogue as audio only. Source text may be analyzed internally; never compile it into an instruction to render text. Only an explicit user request to change this policy permits adjusting the conflicting clause; keep `【Seedance全局控制】` first and avoid contradictory controls.

Each `Seedance提示词` must be self-contained for its scene, relative timing, action, verbatim dialogue, voice style, ambience, music and SFX when present, plus continuity and shot-specific exclusions. The shared clean-frame control remains only at the top of the response; do not reprint or paraphrase the entire control block in each prompt. Never say “same as above” or “append later”. Keep model, duration, ratio, resolution, FPS, format, API settings, strength, seed and UI switches outside the prompt only when they are real confirmed fields.

Before returning, count the control marker in the entire response: it must appear exactly once, on the first line. If missing, prepend the fixed line; if repeated, retain only the opening instance and remove the rest. If shot fields or prompts request visible text contrary to the active policy, remove those requests. Do not move the control to a closing exclusion list.

Seedance 2.5: duration 4–30s integer. Frame mode uses adaptive ratio/no reference arrays; edit inherits source ratio/duration; extend uses adaptive ratio + extension duration. Screenshot workflow: clean each source first frame, reuse person/product anchors, then generate the next shot. Generate ≥4s and trim short shots. Use edit/extend task mode only there. With audio, paste verbatim dialogue + voice/ambience/music timing; never invent fields.

### Step 5 — Stop before generation

**🔴 CHECKPOINT · STOP:** If the user asked for a prompt, stop after the package. Before paid generation, show the package and obtain confirmation unless submission was explicitly authorized in the current request.

## Direct-mode fallbacks

| Trigger | First action | Still unresolved |
|---|---|---|
| No reference media | Give text-only approximation and minimum anchors | Request anchors; never claim 1:1 |
| Required label or schema unknown | Mark `NOT READY`; state the exact missing item | Ask once for platform or real label |
| Source exceeds one-job limit | Propose splits at natural cuts | Stop for confirmation before multiple jobs |
| Identity or product drifts twice | Stop adding text; add or replace a visual anchor | Use edit mode or regenerate from an approved anchor |
| Exact cuts or lip-sync remain unstable | Preserve closest generative timing | Move exact cuts, sync, and explicitly requested captions to deterministic editing |

## Other modes

- **Reference Analysis:** return summary, shot/frame locks, geometry, motion, camera, lighting, color, text/audio, Master Timeline, and instructions.
- **Reshoot Blueprint:** return camera, lighting, actor, prop, marks, timing cues, and ghost overlay.
- **Difference Detection:** synchronize versions; return score, Error Map, Patch List, and next target. Prioritize P0–P4 and patch the smallest range.

## Seedance red lines

- Do not put codec data, frame IDs, coordinate or pose tables, capture settings, scores, or Error Maps into the prompt.
- Do not invent labels, capabilities, sliders, reference weights, seeds, FPS controls, or UI switches.
- Do not mix generate, edit, and extend in one prompt.
- Do not promise exact text, frame cuts, lip-sync, or 1:1 output through wording alone.
- Do not make a third text-only retry after the same consistency failure occurs twice.
