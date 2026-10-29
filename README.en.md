# Video Replica Skill

[中文](README.md) · [Skill instructions](SKILL.md)

A Codex skill that analyzes reference videos and compiles self-contained prompts for text-and-image video generation. The default workflow targets Xiaoyunque: **the video is analysis material for Codex, not an input to the generation platform.**

## What changed

- Describe scenes, people, products, camera paths, dialogue and actions explicitly instead of asking the platform to “keep the original video.”
- Track initial state, contact, release and final state across shots.
- Distinguish image count from product count, and preserve the user's terminology for product measurements.
- Do not assume source audio, extracted frames or reference videos will be uploaded.
- Do not apply Seedance settings or claim unverified Xiaoyunque capabilities.

## Use

Clone or download the repository and have Codex read `SKILL.md`. Keep `agents/` and `references/` alongside it. Register the complete directory with your Codex skill setup if desired; this repository has no automatic installer.

Ask Codex to analyze your authorized reference video and write prompts for text plus the images you actually intend to upload. Specify product changes, count and measurements. Request either independent shot prompts or one complete multi-shot prompt.

See [the example](examples/text-image-workflow.md). The main instructions and playbook are in Chinese. Other workflows are available only when explicitly requested.

## Limits

This is an instruction package, not a video generation model or platform API integration. Media inspection tools come from the host environment. It does not guarantee pixel equality, precise cuts or lip sync. `test-prompts.json` contains manual regression scenarios, not evidence of automated or end-to-end generation tests. Do not redistribute private footage, images or conversations with the skill.

Licensed under [MIT](LICENSE), copyright 2026 haibo0505.

## Narration completeness

When speech is present, reconstruction includes the full narration, including off-screen product explanations. Inspect the entire audio, transcribe and check the words, put concrete dialogue into copyable prompts, and check for omissions, duplicate readings and sentences cut at shot boundaries. Not uploading audio to the generation platform does not remove the narration requirement; a continuous voice-over can be recorded in post-production.

If audio cannot be analyzed, disclose that narration analysis is incomplete and label any visual-only draft accordingly. Distinguish machine transcription, subtitle checks and actual listening; unverified voice qualities are suggestions, not observations. Explicit user requests for silent or visual-only output take precedence.
