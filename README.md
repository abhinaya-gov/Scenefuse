Here is your content structured as a clean, professional **GitHub README.md** file in proper Markdown format:

---

# 🎬 SceneFuse – AI Video Processing Platform

## 🎯 Executive Summary

**SceneFuse** is an advanced AI-powered video processing platform that integrates two state-of-the-art technologies:

- **ProPainter** – High-quality video inpainting for object removal  
- **SAM2 (Segment Anything Model 2)** – Advanced video segmentation for background replacement and object manipulation  

The platform provides a unified web interface for three core capabilities:

- 🧹 Object Removal  
- 🟢 Green Screen / Background Replacement  
- 🖼️ Object Replacement  

---

# 📁 Project Structure

```
TradeShow/Frontend/final/ProPainter/
├── Core ProPainter Engine
│   ├── model/
│   │   ├── propainter.py
│   │   ├── recurrent_flow_completion.py
│   │   └── modules/
│   ├── RAFT/
│   ├── core/
│   └── inference_propainter.py
│
├── SAM2 Integration
│   └── sam2/
│       ├── claude.py
│       ├── green_screen.py
│       ├── generate_preview.py
│       └── frontend/
│
└── Web Applications
├── web-demos/hugging_face/
│   ├── app_unified_demo.py
│   └── templates/
└── sam2/frontend/
├── app_unified.py
└── templates/
```
---

# 🏗️ System Architecture

## Three-Tier Architecture

### 1️⃣ AI Model Layer
- ProPainter Model  
- Recurrent Flow Completion  
- RAFT Optical Flow  
- SAM2 Video Predictor  

### 2️⃣ Processing Layer
- Frame Extraction  
- Segmentation  
- Inpainting  
- Video Reconstruction  

### 3️⃣ Frontend Layer
- Flask Web Server  
- HTML5 + CSS3  
- JavaScript  
- Canvas-based Interactive Selection  

---

# 🎨 Core Features

## 1️⃣ Object Removal (ProPainter)

Removes unwanted objects using transformer-based video inpainting.

**Pipeline:**
1. Upload video + mask  
2. Optical flow estimation (RAFT)  
3. Flow completion  
4. Transformer refinement  
5. Export clean video  

**Key Files:**
- `inference_propainter.py`
- `model/propainter.py`

---

## 2️⃣ Green Screen / Background Replacement (SAM2)

Keep selected objects and replace the background.

**Modes:**
- Solid green background  
- Custom image background  
- Dynamic video background  

**Key File:**
- `sam2/green_screen.py`

---

## 3️⃣ Object Replacement (SAM2)

Replace selected objects with custom images.

**Workflow:**
1. Frame selection  
2. Click-based segmentation  
3. Preview & approve  
4. Object tracking  
5. Apply replacement  

**Key File:**
- `sam2/claude.py`

---

# 🌐 Web Applications

## 🔹 Unified Demo (Port 8001)

**File:** `web-demos/hugging_face/app_unified_demo.py`

### Features:
- Unified interface for all three modes
- Multi-stage workflow:
  ```
  Upload → Select → Preview → Process → Result
  ```

### Key Routes:
- `/` – Landing page  
- `/upload/<mode>`  
- `/select/<session_id>`  
- `/preview/<session_id>`  
- `/process`  
- `/result/<session_id>`  

---

## 🔹 SAM2 Frontend (Port 5000)

**File:** `sam2/frontend/app_unified.py`

Focused interface for segmentation-based tasks.

---

# 🧠 AI Models

## 🟣 ProPainter

**Purpose:** Video inpainting  

**Architecture Components:**
- RAFT Optical Flow  
- Recurrent Flow Completion  
- Transformer Refinement  
- Dual-Domain Propagation  

### Model Weights
weights/ProPainter.pth
weights/recurrent_flow_completion.pth
weights/raft-things.pth

---

## 🟢 SAM2 (Segment Anything Model 2)

**Purpose:** Interactive video segmentation & tracking  

**Capabilities:**
- Click-based object selection  
- Multi-object segmentation  
- Real-time preview  
- Video propagation  

Supports:
- CPU  
- CUDA  
- Apple Silicon (MPS)  

---

# 💻 Technology Stack

## Backend
- Python 3.8+
- Flask
- PyTorch
- Torchvision
- OpenCV
- NumPy / SciPy
- Pillow
- FFmpeg

## Frontend
- HTML5
- CSS3
- JavaScript
- Canvas API

## ML Libraries
- segment-anything
- timm
- einops
- addict

---

# 🔧 Installation

git clone https://github.com/sczhou/ProPainter.git
cd ProPainter

conda create -n propainter python=3.8 -y
conda activate propainter

pip install -r requirements.txt

---

# 🚀 Running the Applications

## Unified Demo (Port 8001)

cd web-demos/hugging_face
python app_unified_demo.py

Open:

http://127.0.0.1:8001


---

## SAM2 Frontend (Port 5000)

cd sam2/frontend
python app_unified.py

Open:

http://127.0.0.1:5000

---

## ProPainter CLI

python inference_propainter.py \
  --video inputs/video.mp4 \
  --mask inputs/mask.png \
  --height 480 \
  --width 640 \
  --fp16

---

# ⚡ Performance & Memory

| Resolution | 50 Frames          | 80 Frames  |
| ---------- | ------------------ | ---------- |
| 1280x720   | 28GB / 19GB (fp16) | OOM / 25GB |
| 720x480    | 11GB / 7GB         | 13GB / 8GB |
| 640x480    | 10GB / 6GB         | 12GB / 7GB |
| 320x240    | 3GB / 2GB          | 4GB / 3GB  |

### Optimization Flags

* `--fp16`
* `--resize_ratio`
* `--neighbor_length`
* `--ref_stride`
* `--subvideo_length`

---

# 🎯 User Workflows

## Object Removal

```
Upload → Mask → Process → Download
```

## Green Screen

```
Upload → Select Object → Preview → Replace Background → Download
```

## Object Replacement

```
Upload → Select Frame → Click Object → Preview → Replace → Download
```

---

# 🔐 Session Management

```python
session_data = {
    'session_id': {
        'video_path': str,
        'mode': str,
        'replacement_path': str,
        'background_path': str,
        'points': list,
        'frame_count': int,
        'fps': float,
        'width': int,
        'height': int
    }
}
```

---

# ✨ Key Strengths

* ✅ Intuitive Multi-Stage Workflow
* ✅ State-of-the-Art AI Models
* ✅ Cross-Platform (CUDA / CPU / MPS)
* ✅ Memory Optimized
* ✅ Clean & Modern UI

---

# 📈 Future Improvements

* WebSocket real-time progress
* Cloud deployment
* REST API support
* Batch processing
* User accounts
* Timeline-based editing

---

# 📚 References

* ProPainter – ICCV 2023
* GitHub: [https://github.com/sczhou/ProPainter](https://github.com/sczhou/ProPainter)
* License: NTU S-Lab License 1.0 (Non-commercial use)
* SAM2: Meta Segment Anything License

---

# 🎬 Conclusion

SceneFuse demonstrates the practical integration of **ProPainter** and **SAM2**, delivering professional-grade AI video editing through an intuitive web interface.

It combines advanced deep learning, interactive segmentation, and optimized processing pipelines to make cutting-edge video manipulation accessible to professionals and creators alike.

---

*Generated February 2026*
