# 🖐️ Visual Drag-and-Drop with Hand Tracking  

![Demo GIF](https://github.com/user-attachments/assets/a11ae582-d54c-4075-8d70-6a45cafb12ac)  
*(Replace with your actual demo GIF/video)*  

## 📌 Project Overview  
This project implements **real-time hand gesture-based drag-and-drop** using OpenCV and MediaPipe. Users can pinch and drag semi-transparent UI boxes with visual feedback.  

---

## ✨ Key Features  
| Feature | Description |
|---------|-------------|
| **Precise Hand Tracking** | MediaPipe-based 21-landmark detection |
| **Intuitive Pinch-to-Drag** | Threshold-controlled gesture recognition |
| **Semi-Transparent UI** | 80% alpha blended draggable boxes |
| **Debounce System** | Prevents false triggers (5-frame threshold) |
| **Multi-Object Control** | Simultaneous management of multiple boxes |

---

## 🚀 How It Works  

### 1. Hand Detection Pipeline  
- Uses `HandTrackingModule` (MediaPipe wrapper)  
- Tracks specific landmarks:  
  - Index finger (Landmark 8)  
  - Middle finger (Landmark 12)  

### 2. Pinch Gesture Logic  

# Pinch detection formula
finger_distance = math.hypot(x2-x1, y2-y1)
if finger_distance < PINCH_THRESHOLD:  # Default: 35px
    activate_drag()
3. Dragging Mechanics
State	Visual Feedback	Behavior
Idle	Purple box	Waiting for input
Active	Green box + red circle	Follows finger midpoint
Released	Returns to purple	Maintains new position
4. Visual Feedback System
Real-time status overlay

Color-coded box states

Pinch point indicator

🛠️ Technical Implementation
Core Classes
DraggableBox Class
Method	Parameters	Functionality
__init__	pos_center, size	Initializes box properties
update	img, lm_list	Handles gesture detection
draw	img	Renders with alpha blending
Main Process Flow
Camera initialization (1280×720)

Box instantiation at predefined positions

Continuous tracking loop:

python
while True:
    success, img = cap.read()
    hands = detector.findHands(img)
    for box in boxes:
        box.update(img, hands)
        box.draw(img)
🏁 Getting Started
Installation
bash
pip install -r requirements.txt  # Contains:
# opencv-python==4.5.5.64
# mediapipe==0.8.11
# numpy==1.21.5
Usage
bash
python drag_and_drop.py
Controls:

Pinch inside box → Drag

Release fingers → Drop

Q key → Exit program

🔮 Future Enhancements
Priority	Feature	Status
P1	Collision detection	Planned
P2	Grid snapping	Researching
P3	Gesture controls (rotate/delete)	Backlog
P4	Performance optimization	In Progress
