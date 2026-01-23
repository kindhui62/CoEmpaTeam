# CoEmpaTeam

**CoEmpaTeam: Enhancing Cognitive Empathy using LLM-based Avatars and Dynamic Role Play in Virtual Reality**

This repository accompanies our **CHI 2026** submission and provides a reproducible Unity setup for the **CoEmpaTeam** prototype.

We share a Unity `.unitypackage` export that contains the core scene/scripts/assets needed to run the demo, plus guidance to configure:

- **Local Whisper** (speech-to-text)
- **LLM FastAPI** endpoint (dialogue generation)
- **TTS voice IDs** (avatar voices)
- Optional **FinalIK** gaze/look-at (**not redistributed due to license**)

> Note: Some third-party plugins/assets (e.g., FinalIK) are not distributed in this repository. See **License & Third-Party Terms**.

---

## What’s Included

### Unity Package
- `CoEmpaTeam_Unity.unitypackage`  
  A Unity package that contains the core content required for running CoEmpaTeam in Unity, including:
  - Main scene(s)
  - Scripts (Whisper STT + LLM integration + avatar orchestration)
  - Ready Player Me avatars used in our study (**Alice / Benji / Caden**)
  - Animator controllers and included gesture clips (e.g., `Talking`, `SittingIdle`, `Clapping`) where applicable

### Repository Files
- `README.md` — this setup guide  
- `LICENSE` — license for code/original content included in this repository  
- `.gitignore`

---

## System Requirements

- **Unity**: Unity 2022.3 LTS (recommended)
- **XR**: Meta XR / Oculus XR Plugin (depending on your project setup)
- **Hardware**: Meta Quest Pro / Quest 3 (recommended)

---

## Quick Start

### 1) Create a URP Unity Project
1. Open **Unity Hub** → **New project**
2. Choose **Universal Render Pipeline (URP)** template
3. Create the project (Unity 2022.3 LTS recommended)

### 2) Import the Unity Package
1. `Assets` → `Import Package` → `Custom Package...`
2. Select `CoEmpaTeam_Unity.unitypackage`
3. Import all items

### 3) Open the Main Scene
Open the main scene shipped in the package, for example:
- `Assets/Scenes/CoLiveRoomScene.unity` *(name may vary depending on your package export)*

### 4) Configure Endpoints (Required)
You must configure:
- Local Whisper endpoint (speech-to-text)
- LLM FastAPI endpoint
- TTS voice IDs

See **Configuration** below.

---

## Configuration

### A) Local Whisper Service (Speech-to-Text)

The Unity client records audio and uploads a WAV file to a **user-hosted** Whisper HTTP endpoint for transcription.

c Expected request format
- `POST` `multipart/form-data`
- field name: `file`
- audio: `audio/wav`

#### Expected response format
```json
{ "text": "<transcription>" }
```

#### Why local Whisper?

We use local transcription to avoid sending raw audio to third-party cloud services and to support offline/LAN deployments.


### B) LLM Backend (FastAPI)

CoLive_manager.cs calls an LLM backend through an HTTP endpoint.

### Required configuration

Set gptApiUrl (in Inspector or in code)

> Tip: In the scene hierarchy, you likely have a CoLive_manager_object. Select it and set gptApiUrl in the Inspector.

### C) Text-to-Speech (Voice IDs)

You must provide voice IDs for each avatar in CoLive_manager.cs.

If voice IDs are not configured, TTS may fail or fall back to an unintended default.

### Optional: FinalIK (Not Distributed)

#### FinalIK is NOT included due to license restrictions.

If you want to enable FinalIK gaze/look-at:

1) Import FinalIK

Import FinalIK into your Unity project from your licensed copy.

2) Enable compile flag

Add the scripting define symbol:

Edit → Project Settings → Player → Other Settings → Scripting Define Symbols

Add:

FINAL_IK

3) Bind scene references

Locate LookAtManager in the scene and bind (in Inspector):

aliceLook, benjiLook, cadenLook (LookAtIK components)

head targets and proxy transforms (e.g., AliceLookProxy, BenjiLookProxy, CadenLookProxy)

playerCamera (CenterEyeAnchor or your main camera transform)

Scripts wrapped in #if FINAL_IK will be excluded unless the define symbol is present.

#### Animations (Mixamo)

This repository includes the animator controllers/state machines used to drive avatar gestures (e.g., Talking, SittingIdle, Clapping).

Animation clips are sourced from Mixamo (Adobe) and retargeted to our Ready Player Me avatars.

If you prefer not to use the included clips, you can download equivalent animations from Mixamo and replace the clips while keeping:

the same animator controller structure

the same parameter names and state names (recommended for compatibility)

#### Ready Player Me Avatars

This repository includes three Ready Player Me avatars (Alice, Benji, Caden) used in our study to support reproducibility.

Avatars were created using the Ready Player Me avatar creator and exported for Unity usage.

Please ensure your usage complies with Ready Player Me’s terms.


## Third-Party Libraries / Dependencies

This project relies on third-party libraries/plugins, governed by their own licenses/terms:

FinalIK (optional; not redistributed)

Ready Player Me (avatars + loader tooling)

Mixamo (animation source)

Meta XR / Oculus XR Plugin (depending on your Unity setup)

## Citation

If you use this repository/package in academic work, please cite our CHI 2026 paper (citation details will be updated upon publication).



