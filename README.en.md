# 1:1 Video Replica Skill

A Codex skill for reconstructing **authorized** reference videos. It measures shots and timing, prepares direct Seedance prompts, supports physical reshoots, and compares a recreation with its reference.

The goal is to reduce visible differences. Text prompts alone cannot guarantee pixel-level equality.

## Install

Copy this repository to your Codex skills directory so that `SKILL.md` is at `one-to-one-video-replica/SKILL.md`. On Windows:

```powershell
git clone https://github.com/haibo0505/one-to-one-video-replica.git
New-Item -ItemType Directory -Force -Path (Join-Path $env:USERPROFILE '.codex\skills') | Out-Null
Copy-Item -Recurse -Force -LiteralPath '.\one-to-one-video-replica' -Destination (Join-Path $env:USERPROFILE '.codex\skills\one-to-one-video-replica')
```

## Use

Invoke `$one-to-one-video-replica` with your licensed reference video and any replacement product, person, or audio assets. State the target product count and colorways explicitly when they differ from the source video.

The four routes are Seedance Direct, Reference Analysis, Reshoot Blueprint, and Difference Detection. See [README.md](README.md) and [SKILL.md](SKILL.md) for details.

Licensed under [MIT](LICENSE).
