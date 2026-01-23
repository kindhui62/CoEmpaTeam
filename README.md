# CoEmpaTeam
CoEmpaTeam: Enhancing Cognitive Empathy using LLM-based Avatars and Dynamic Role Play in Virtual Reality.

This repository accompanies our CHI 2026 submission and provides a reproducible prototype setup.
Some third-party assets/plugins are not redistributed due to licensing.

## Contents
- `CoEmpaTeam_Unity.unitypackage` — Unity package (scene/scripts/assets) for the demo
- `backend/CoEmpaTeam_backend/` — Python backend (LLM dialogue endpoint)
- `LICENSE`

## Quick Start
### Unity
1. Create a Unity 2022.3 (URP) project.
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



