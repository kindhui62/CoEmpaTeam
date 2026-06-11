# CoEmpaTeam
CoEmpaTeam: Enhancing Cognitive Empathy using LLM-based Avatars and Dynamic Role Play in Virtual Reality.

This repository accompanies our CHI 2026 submission and provides a reproducible prototype setup.
Some third-party assets/plugins are not redistributed due to licensing.

## Contents
- `CoEmpaTeam_Unity.unitypackage` — Unity package (scene/scripts/assets) for the demo
- `backend/CoEmpaTeam_backend/` — Python backend (LLM dialogue endpoint)
- `LICENSE`

## Demo Video
A video of CoEmpaTeam is available on YouTube:  
[Watch the video](https://www.youtube.com/watch?v=ODzQGc8KNZI)

## Software Stack (from the paper)
- **Unity:** Unity3D 2022.3.51f1
- **Device:** Meta Quest Pro
- **Backend:** Python 3.10 + FastAPI (deployed on Render)
- **STT:** Local OpenAI Whisper (speech-to-text)
- **LLM:** Llama 3.1 8B Instruct (via Chat AI API)
- **TTS:** ElevenLabs (text-to-speech)
- **Lip Sync:** Oculus LipSync Unity SDK
- **Avatars:** Ready Player Me
- **Gestures:** Mixamo animations
- **Gaze:** Final IK (Look At IK)
- **Output Format:** JSON with `speaker`, `text`, `gesture`, `emotion`



## Quick Start
### Unity
1. Create a Unity 2022.3.51f1 project.
2. Import `CoEmpaTeam_Unity.unitypackage`.
3. Open the main scene in the imported project.
4. In the scene Inspector, set:
   - Whisper STT endpoint
   - LLM backend endpoint
   - TTS voice IDs (per avatar)

### Backend (example)
```bash
cd backend/CoEmpaTeam_backend
pip install -r requirements.txt
# run FastAPI (adjust module/app name if needed)
uvicorn app:app --host 0.0.0.0 --port 8000
```
---

## Configuration (minimal)
- **Whisper STT:** Unity uploads a WAV to your Whisper HTTP service and expects a JSON response:  
  - Response: `{ "text": "<transcription>" }`
- **LLM Backend:** Set the backend URL in `CoLive_manager.cs` (Inspector or code).
- **TTS:** Set voice IDs for each avatar (e.g., Alice / Benji / Caden).

## Third-Party Notes
- **FinalIK (optional):** Not included. Import from your licensed copy if you want gaze/look-at.
- **Ready Player Me:** Avatars used for reproducibility; ensure compliance with their terms.
- **Mixamo:** Animation source; ensure compliance with their terms.
- **Meta XR / Oculus XR:** Required depending on your Unity/XR setup.

## Citation
If you use this repository/package in academic work, please cite our CHI 2026 paper.  
(Citation details will be updated upon publication.)

```bibtex
@inproceedings{kong2026coempateam,
  title={CoEmpaTeam: Enhancing Cognitive Empathy using LLM-based Avatars and Dynamic Role Play in Virtual Reality},
  author={Kong, Dehui and Feick, Martin and Liu, Shi and Maedche, Alexander},
  booktitle={Proceedings of the 2026 CHI Conference on Human Factors in Computing Systems},
  pages={1--17},
  year={2026}
}

```

