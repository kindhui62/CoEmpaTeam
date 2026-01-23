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

