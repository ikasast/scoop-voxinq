# scoop-voxinq

A [Scoop](https://scoop.sh) bucket for [Voxinq](https://github.com/ikasast/voxinq-meeting) —
self-hosted meeting minutes: record in the browser, transcribe and summarize on your own
machine.

```powershell
scoop bucket add voxinq https://github.com/ikasast/scoop-voxinq
scoop install voxinq
voxinq setup     # dependencies, build, transcription and speaker-separation environments
voxinq start
```

`voxinq setup` is a separate step because it takes several minutes, downloads speech models,
and on a machine with an NVIDIA GPU pulls several gigabytes of PyTorch. Doing that inside
`scoop install` would mean minutes with nothing to look at and no way to resume. It is
re-runnable, and it is also how you finish an upgrade.

## What comes with it

| | |
| --- | --- |
| PostgreSQL | bundled — nothing to install or configure |
| Node, Python | Scoop dependencies (`nodejs-lts`, `python`) |
| An LLM for minutes | not included: `scoop install ollama`, or point Settings → LLM at a cloud model |

Your data lives in `%LOCALAPPDATA%\voxinq`, outside the install, so upgrading or removing the
package cannot delete it.

## Verified

`scoop install` → `voxinq setup` → `voxinq start` was run end to end on Windows 11 against the
published v2.0.0-beta.3 release, on an NVIDIA machine: bundled PostgreSQL up, transcription on
faster-whisper/CUDA with live text, speaker separation on pyannote.

## Updating the manifest

`bucket/voxinq.json` is copied from
[`packaging/scoop/voxinq.json`](https://github.com/ikasast/voxinq-meeting/tree/main/packaging)
in the main repository, which is where it is edited. The release workflow prints the `url` and
`hash` to update it with.
