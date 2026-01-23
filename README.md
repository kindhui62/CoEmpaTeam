# CoEmpaTeam
CoEmpaTeam: Enhancing Cognitive Empathy using LLM-based Avatars and Dynamic Role Play in Virtual Reality

This repository accompanies our CHI 2026 submission and provides a reproducible Unity setup for the **CoEmpaTeam** prototype.  
We share a Unity `.unitypackage` export that contains the core scene/scripts/assets needed to run the demo, plus guidance to configure:
- **Local Whisper** (speech-to-text)
- **LLM FastAPI** endpoint (dialogue generation)
- **TTS voice IDs** (avatar voices)
- Optional **FinalIK** gaze/look-at (not redistributed due to license)

> Note: Some third-party plugins/assets (e.g., FinalIK) are not distributed in this repository. See **Licensing**.

---

## What’s Included

### Unity Package
- `CoEmpaTeam_Unity.unitypackage`  
  A Unity package that contains the core content required for running the CoEmpaTeam in Unity, including:
  - main scene(s)
  - scripts (Whisper STT + LLM integration + avatar orchestration)
  - Ready Player Me avatars used in our study (Alice / Benji / Caden)
  - animator controllers and included gesture clips (e.g., Talking, SittingIdle, Clapping) where applicable

### Repository Files
- `README.md` — This setup guide  
- `LICENSE` — License for code/original content included in this repository  
- `.gitignore`

---

## System Requirements

- **Unity**: Unity 2022.3 LTS (recommended)
- **XR**: Meta XR / Oculus XR Plugin depending on your project setup
- **Hardware**: Meta Quest Pro / Quest 3

---

## Quick Start (Most Users)

### 1) Create a URP Unity Project
1. Unity Hub → **New project**
3. Create project (Unity 2022.3 LTS recommended)

### 2) Import the Unity Package
1. `Assets` → `Import Package` → `Custom Package...`
2. Select `CoEmpaTeam_Unity.unitypackage`
3. Import all items

### 3) Open the Main Scene
Open the main scene shipped in the package, for example:
- `Assets/Scenes/CoLiveRoomScene.unity` (name may vary depending on your package export)

### 4) Configure Endpoints (Required)
You must configure:
- Local Whisper endpoint (speech-to-text)
- LLM FastAPI endpoint
- TTS voice IDs

See below sections.

---

## Configuration

### A) Local Whisper Service (Speech-to-Text)

The Unity client records audio and uploads a WAV file to a **user-hosted** Whisper HTTP endpoint for transcription.


#### Expected request format
- `POST` `multipart/form-data`
- field name: `file`
- audio: `audio/wav`

#### Expected response format
```json
{ "text": "<transcription>" }

#### Why Local Whisper?

We use **local transcription** to avoid sending raw audio to third-party cloud services**.

---

## B) LLM Backend (FastAPI)

`CoLive_manager.cs` calls an LLM backend through an HTTP endpoint.

### Required Configuration

Set `gptApiUrl` (in Inspector or in code):

```csharp
[Header("LLM FastAPI")]
public string gptApiUrl = "YOUR_FASTAPI_ENDPOINT";

C) Text-to-Speech (Voice IDs)

You must provide voice IDs for each avatar in CoLive_manager.cs.

private string GetVoiceIdForAvatar(string speaker)
{
    switch (speaker)
    {
        case "Benji": return "YOUR_VOICE_ID";
        case "Caden": return "YOUR_VOICE_ID";
        case "Alice": return "YOUR_VOICE_ID";
        default: return "YOUR_VOICE_ID";
    }
}


If voice IDs are not configured, TTS may fail or fall back to an unintended default.

Optional: FinalIK (Not Distributed)

FinalIK is NOT included due to license restrictions.

If you want to enable FinalIK gaze/look-at:

1) Import FinalIK

Import FinalIK into your Unity project from your licensed copy.

2) Enable Compile Flag

Add the scripting define symbol:

Edit → Project Settings → Player → Other Settings → Scripting Define Symbols

Add:

FINAL_IK

3) Bind Scene References

Locate LookAtManager in the scene and bind (in Inspector):

aliceLook, benjiLook, cadenLook (LookAtIK components)

head targets and proxy transforms (e.g., AliceLookProxy, BenjiLookProxy, CadenLookProxy)

playerCamera (CenterEyeAnchor or your main camera transform)

Scripts wrapped in #if FINAL_IK will be excluded unless the define symbol is present.

Animations (Mixamo)

This repository includes the animator controllers/state machines used to drive avatar gestures (e.g., Talking, SittingIdle, Clapping).

Animation clips are sourced from Mixamo (Adobe) and retargeted to our Ready Player Me avatars.

If you prefer not to use the included clips, you can download equivalent animations from Mixamo and replace the clips while keeping:

the same animator controller structure

the same parameter names and state names (recommended for compatibility)

Ready Player Me Avatars

This repository includes three Ready Player Me avatars (Alice, Benji, Caden) used in our study to support reproducibility.

Avatars were created using the Ready Player Me avatar creator and exported for Unity usage.

Please ensure your usage complies with Ready Player Me’s terms.

Minimal Import Option (If You Only Need Specific Parts)

If you do not want to import everything, you can import the .unitypackage and only select:

Scripts (Whisper / LLM / manager scripts)

Animator Controllers + relevant animation clips

Avatars (Alice / Benji / Caden prefabs)

This is useful if you already have your own environment/scene and only need the interaction stack.

Common Setup Checklist (Recommended)

After importing:

Open the correct scene

Ensure XR rig exists (e.g., OVRCameraRig) and is active

In Inspector:

set Whisper endpoint (WhisperSpeechToText)

set LLM endpoint (CoLive_manager.cs → gptApiUrl)

set voice IDs (GetVoiceIdForAvatar)

Press Play in Editor to validate the pipeline end-to-end

Troubleshooting
1) “Rescan shows nothing” / Git GUI shows no changes

If Git GUI shows no unstaged changes:

confirm the .unitypackage is inside the repository folder

confirm it is not ignored by .gitignore

press Rescan

if still empty, check file size and filesystem sync (OneDrive sometimes delays file change notifications)

2) GitHub web upload says “Try again with a file smaller than 25MB”

GitHub’s browser upload UI has a practical limit (commonly 25MB).
For large binaries (like an 88MB .unitypackage), use git push (command line or Git GUI), or use Git LFS.

3) Pink / missing materials after import

You likely imported into a non-URP project or URP is not configured:

Use URP template from Unity Hub

Ensure URP pipeline asset is assigned in Project Settings → Graphics

4) FinalIK compile errors

If FinalIK is not installed but scripts reference it:

keep scripts under #if FINAL_IK guards (recommended)

ensure FINAL_IK define is not set unless FinalIK is imported

5) Whisper endpoint returns empty text

Validate:

endpoint URL is reachable from your machine/device

request is multipart/form-data with field name file

response JSON contains:

{ "text": "..." }

Recommended Distribution (GitHub Releases)

For large .unitypackage files, we recommend:

publish the .unitypackage under GitHub Releases (Assets)

keep the repository lightweight, and link the release in README

If you prefer to store binaries directly in git, consider Git LFS.

Third-Party Libraries / Dependencies

This project relies on third-party libraries/plugins, governed by their own licenses/terms:

FinalIK (optional; not redistributed)

Ready Player Me (avatars + loader tooling)

Mixamo (animation source)

Meta XR / Oculus XR Plugin (depending on your Unity setup)

Citation

If you use this repository/package in academic work, please cite our CHI 2026 paper (citation details will be updated upon publication).

License

Code and original content in this repository: see LICENSE.

Third-party assets/plugins (FinalIK, Ready Player Me, Mixamo, Meta XR/Oculus XR) remain under their own licenses/terms and are not re-licensed by this repository.
