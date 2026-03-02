SceneFuse - AI Video Processing Platform
Comprehensive Codebase Analysis & Summary
🎯 Executive Summary
SceneFuse is an advanced AI-powered video processing platform that combines two cutting-edge technologies:

ProPainter - State-of-the-art video inpainting for object removal
SAM2 (Segment Anything Model 2) - Advanced video segmentation for background replacement and object manipulation
The platform provides a unified web interface for three core video processing capabilities: Object Removal, Green Screen Effects, and Object Replacement.

📁 Project Structure
TradeShow/Frontend/final/ProPainter/
├── Core ProPainter Engine
│   ├── model/                    # Neural network models
│   │   ├── propainter.py        # Main ProPainter model
│   │   ├── recurrent_flow_completion.py
│   │   └── modules/             # Flow completion, transformers
│   ├── RAFT/                    # Optical flow estimation
│   ├── core/                    # Training & utilities
│   └── inference_propainter.py  # Main inference script
│
├── SAM2 Integration
│   └── sam2/
│       ├── claude.py            # Object replacement pipeline
│       ├── green_screen.py      # Background replacement pipeline
│       ├── generate_preview.py  # Segmentation preview
│       └── frontend/            # SAM2 web application (Port 5000)
│
└── Web Applications
    ├── web-demos/hugging_face/  # Unified demo (Port 8001)
    │   ├── app_unified_demo.py  # Main Flask application
    │   └── templates/           # HTML templates
    └── sam2/frontend/           # SAM2-only demo (Port 5000)
        ├── app_unified.py
        └── templates/
🏗️ System Architecture
Three-Tier Architecture
AI Models
Processing Layer
Frontend Layer
Web Interface - Flask
HTML5 Canvas
Interactive Object Selection
ProPainter Engine
SAM2 Segmentation
Video Frame Processor
ProPainter Model
Flow Completion Network
SAM2 Video Predictor
RAFT Optical Flow
🎨 Core Features
1. Object Removal (ProPainter)
Technology: ProPainter video inpainting model
Capability: Remove unwanted objects from videos with AI-powered content filling
Process:
User uploads video and provides mask (manual or SAM2-generated)
ProPainter analyzes optical flow using RAFT
Recurrent flow completion fills masked regions
Transformer-based refinement ensures temporal consistency
Output: Clean video with objects seamlessly removed
Key Files:

inference_propainter.py
 - Main inference pipeline
model/propainter.py
 - Core model architecture
2. Green Screen / Background Replacement (SAM2)
Technology: SAM2 video segmentation
Capability: Keep selected objects, replace entire background
Modes:
Pure green screen (solid color)
Custom image background
Custom video background (dynamic)
Process:
User clicks on object(s) to keep
SAM2 segments and tracks object across all frames
Background replaced with chosen color/image/video
Alpha blending for smooth edges
Key Files:

sam2/green_screen.py
 - Background replacement pipeline
3. Object Replacement (SAM2)
Technology: SAM2 video segmentation
Capability: Replace selected objects with custom images
Process:
Interactive frame selection with arrow key navigation
Click-based object selection
Segmentation preview and approval workflow
SAM2 tracks object across video
Replacement image scaled and applied to masked regions
Key Files:

sam2/claude.py
 - Object replacement pipeline
🌐 Web Applications
Application 1: Unified Demo (Port 8001)
File: 
web-demos/hugging_face/app_unified_demo.py

Features:

Unified interface for all three processing modes
Multi-stage workflow:
Upload - Video and optional replacement assets
Select - Interactive canvas-based object selection
Preview - Segmentation preview before processing
Process - Execute AI pipeline
Result - View and download processed video
Technology Stack:

Backend: Flask (Python)
Frontend: HTML5, JavaScript, Canvas API
Video Processing: OpenCV, FFmpeg
AI Models: ProPainter, SAM2
Key Routes:

/ - Feature selection landing page
/upload/<mode> - Upload page for each mode
/select/<session_id> - Interactive object selection
/preview/<session_id> - Segmentation preview
/process - Video processing endpoint
/result/<session_id> - Results display
Application 2: SAM2 Frontend (Port 5000)
File: 
sam2/frontend/app_unified.py

Features:

Focused on SAM2-based processing only
Similar multi-stage workflow
In-browser object selection using HTML5 canvas
Supports object replacement and background modes
🧠 AI Models & Technologies
ProPainter Model
Purpose: Video inpainting and object removal

Architecture:

RAFT Optical Flow - Estimates motion between frames
Recurrent Flow Completion - Fills flow in masked regions
ProPainter Transformer - Refines inpainting with temporal attention
Dual-Domain Propagation - Combines image and flow domains
Model Files:

weights/ProPainter.pth - Main model checkpoint
weights/recurrent_flow_completion.pth - Flow completion network
weights/raft-things.pth - RAFT optical flow model
Key Parameters:

neighbor_length (default: 10) - Local temporal neighbors
ref_stride (default: 10) - Global reference frame spacing
subvideo_length (default: 80) - Frames per processing batch
fp16 - Half precision for memory efficiency
SAM2 (Segment Anything Model 2)
Purpose: Video object segmentation and tracking

Capabilities:

Interactive segmentation - Click-based object selection
Video propagation - Tracks objects across frames
Multi-object support - Segment multiple objects simultaneously
Real-time preview - Shows segmentation before processing
Model Configuration:

Model: sam2_hiera_l.yaml (Large hierarchical model)
Checkpoint: Auto-downloaded on first run
Device: Supports CPU, CUDA, MPS (Apple Silicon)
MPS Compatibility:

Custom patches for Apple Silicon (M1/M2/M3)
Float32 enforcement for matrix operations
Comprehensive compatibility layer
💻 Technology Stack
Backend
Python 3.8+
Flask - Web framework
PyTorch ≥1.7.1 - Deep learning framework
Torchvision ≥0.8.2 - Computer vision utilities
OpenCV - Video processing
NumPy, SciPy - Numerical computing
Pillow - Image processing
imageio-ffmpeg - Video encoding/decoding
Frontend
HTML5 - Structure
CSS3 - Styling with modern design
JavaScript (Vanilla) - Interactivity
Canvas API - Interactive object selection
Google Fonts (Inter) - Typography
AI/ML Libraries
segment-anything - SAM2 integration
timm - Vision transformer models
einops - Tensor operations
addict - Configuration management
Development Tools
Git - Version control
YAML - Configuration files
tqdm - Progress bars
psutil - System monitoring
🎯 User Workflows
Workflow 1: Object Removal
Upload Video
Upload/Draw Mask
ProPainter Processing
Download Result
Workflow 2: Green Screen
Yes
No
Upload Video
Select Objects to Keep
Preview Segmentation
Approve?
SAM2 Processing
Choose Background
Download Result
Workflow 3: Object Replacement
Yes
No
Upload Video + Image
Select Frame
Click on Object
Preview Segmentation
Approve?
SAM2 Tracking
Apply Replacement
Download Result
🎨 UI/UX Design
Design Principles
Modern & Clean - Minimalist interface with focus on functionality
Gradient Accents - Blue gradient theme (#2563eb to #1d4ed8)
Card-Based Layout - Feature cards with hover effects
Responsive Design - Adapts to different screen sizes
Visual Feedback - Loading states, progress indicators, previews
Key UI Components
Landing Page - Feature selection with three cards
Upload Form - Drag-and-drop file upload with validation
Canvas Selector - Interactive object selection with visual feedback
Preview Panel - Side-by-side comparison (original vs segmented)
Results Page - Video player with download option
Color Palette
Primary: #2563eb (Royal Blue)
Secondary: #1d4ed8 (Darker Blue)
Background: #f8fafc (Light Gray)
Text: #1a1a1a (Near Black)
Muted: #64748b (Slate Gray)
Success: #166534 (Green)
Warning: #92400e (Amber)
🔧 Configuration & Setup
Installation
bash
# Clone repository
git clone https://github.com/sczhou/ProPainter.git
# Create conda environment
conda create -n propainter python=3.8 -y
conda activate propainter
# Install dependencies
pip install -r requirements.txt
Running Applications
Unified Demo (Port 8001):

bash
cd web-demos/hugging_face
python app_unified_demo.py
# Access at http://127.0.0.1:8001
SAM2 Frontend (Port 5000):

bash
cd sam2/frontend
python app_unified.py
# Access at http://127.0.0.1:5000
ProPainter CLI:

bash
python inference_propainter.py \
  --video inputs/video.mp4 \
  --mask inputs/mask.png \
  --height 480 --width 640 \
  --fp16
Memory Optimization
--fp16 - Use half precision (reduces memory by ~40%)
--resize_ratio - Scale down video resolution
--neighbor_length - Reduce temporal neighbors (default: 10)
--ref_stride - Increase reference frame spacing (default: 10)
--subvideo_length - Reduce batch size (default: 80)
GPU Memory Requirements:

Resolution	50 frames	80 frames
1280x720	28GB / 19GB (fp16)	OOM / 25GB (fp16)
720x480	11GB / 7GB (fp16)	13GB / 8GB (fp16)
640x480	10GB / 6GB (fp16)	12GB / 7GB (fp16)
320x240	3GB / 2GB (fp16)	4GB / 3GB (fp16)
📊 Key Metrics & Performance
Processing Speed
ProPainter: ~1-2 seconds per frame (GPU)
SAM2 Segmentation: ~0.5 seconds per frame (GPU)
Total Pipeline: Depends on video length and resolution
Quality Metrics
Temporal Consistency: High (transformer-based attention)
Edge Quality: Smooth alpha blending
Object Tracking: Robust across occlusions
Supported Formats
Input: MP4 video, PNG/JPEG images
Output: MP4 video (H.264 codec)
Max Resolution: Limited by GPU memory
🔐 Session Management
Session Data Structure
python
session_data = {
    'session_id': {
        'video_path': str,
        'mode': str,  # 'object_removal', 'greenscreen', 'object_replacement'
        'replacement_path': str,  # Optional
        'background_path': str,   # Optional
        'points': List[Tuple[int, int]],
        'frame_count': int,
        'fps': float,
        'width': int,
        'height': int
    }
}
File Organization
unified_uploads/          # Uploaded files
├── <session_id>/
│   ├── video.mp4
│   ├── replacement.png
│   └── background.mp4
unified_outputs/          # Processed results
├── <session_id>/
│   └── output.mp4
unified_frames/           # Temporary frames
├── <session_id>/
│   ├── frame_0000.jpg
│   └── ...
🚀 Advanced Features
1. Interactive Frame Selection
Arrow key navigation (LEFT/RIGHT or A/D)
SPACE to select multiple frames
Visual feedback with frame counter
Implemented in 
claude.py
2. Segmentation Preview
Side-by-side comparison
Overlay visualization
Approve/reject workflow
Re-selection capability
3. Multi-Object Support
Multiple click points
Combined segmentation masks
Simultaneous tracking
4. Background Modes
Solid Color: Green screen effect
Static Image: Custom background image
Dynamic Video: Video background with looping
5. MPS (Apple Silicon) Support
Automatic device detection
Float32 enforcement patches
Optimized for M1/M2/M3 chips
📈 Recent Development History
Based on conversation history:

Recent Refactoring (Feb 2026)
Unified Demo Refactoring

Adopted multi-stage pipeline interface
Consistent UX across all three modes
Upload → Segment → Track → Process flow
In-Browser Object Selection

Replaced popup windows with HTML5 canvas
Integrated object selection interface
Improved user experience
Segmentation Preview

Added preview before processing
Approve/reject workflow
Better user control
🎓 Use Cases
Professional Applications
Video Production: Remove unwanted objects, boom mics, wires
Content Creation: Replace backgrounds for YouTube/TikTok
Film/TV Post-Production: Clean up scenes, remove crew/equipment
Marketing: Product placement, background customization
Education: Create teaching materials with custom backgrounds
Creative Applications
Artistic Effects: Surreal object replacements
Meme Creation: Replace objects with funny images
Social Media: Custom backgrounds for videos
Virtual Production: Green screen effects without physical setup
🔬 Technical Innovations
ProPainter Innovations
Dual-Domain Propagation: Combines image and flow information
Recurrent Flow Completion: Handles large masked regions
Transformer Attention: Ensures temporal consistency
Memory-Efficient Design: Processes long videos in sub-batches
SAM2 Integration
Interactive Segmentation: Click-based object selection
Video Propagation: Automatic tracking across frames
Real-Time Preview: Immediate feedback before processing
Multi-Modal Support: Handles various background types
📝 Code Quality & Patterns
Design Patterns
MVC Architecture: Separation of concerns (Flask routes, processing logic, templates)
Session Management: Stateful processing with unique session IDs
Lazy Loading: Models loaded on first use
Error Handling: Comprehensive try-catch blocks with user feedback
Code Organization
Modular Structure: Separate files for each processing mode
Reusable Functions: Shared utilities for frame extraction, video saving
Configuration Management: YAML-based model configs
Type Hints: Limited but present in newer code
🎯 Future Enhancement Opportunities
Potential Improvements
Real-Time Processing: WebSocket-based progress updates
Batch Processing: Multiple videos at once
Cloud Deployment: Scalable infrastructure
API Endpoints: RESTful API for programmatic access
User Accounts: Save projects, history
Advanced Editing: Timeline-based editing interface
Mobile Support: Responsive design for tablets/phones
Export Options: Multiple format/quality options
📚 Documentation & Resources
Official Links
ProPainter Paper: ICCV 2023
Project Page: shangchenzhou.com/projects/ProPainter
GitHub: sczhou/ProPainter
Hugging Face Demo: sczhou/ProPainter
License
ProPainter: NTU S-Lab License 1.0 (Non-commercial use only)
SAM2: Meta's Segment Anything License
🎬 Conclusion
SceneFuse represents a sophisticated integration of two state-of-the-art AI technologies:

ProPainter for professional-grade video inpainting
SAM2 for advanced video segmentation
The platform provides an intuitive web interface that makes complex AI video processing accessible to both professionals and enthusiasts. With its multi-stage workflow, interactive object selection, and real-time preview capabilities, SceneFuse demonstrates the practical application of cutting-edge research in computer vision and deep learning.

Key Strengths
✅ User-Friendly: Intuitive multi-stage workflow
✅ Powerful: State-of-the-art AI models
✅ Flexible: Multiple processing modes
✅ Efficient: Memory-optimized for various hardware
✅ Modern: Clean, responsive web interface

Technical Excellence
✅ Modular Architecture: Clean separation of concerns
✅ Robust Processing: Comprehensive error handling
✅ Cross-Platform: Supports CUDA, CPU, and Apple Silicon
✅ Production-Ready: Session management, file handling, security

This summary was generated on February 10, 2026
