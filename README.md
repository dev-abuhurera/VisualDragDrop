# 🖐️ Visual Drag-and-Drop with Hand Tracking  
*  

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


### 3. Dragging Mechanics

| State      | Visual Feedback          | Behavior                      |
|------------|--------------------------|-------------------------------|
| **Idle**   | <span style="color:purple">■</span> Purple box | Waits for user input |
| **Active** | <span style="color:green">■</span> Green box + 🔴 Red circle | Follows midpoint between fingers |
| **Released**| <span style="color:purple">■</span> Returns to purple | Maintains new position |

### 4. Visual Feedback System

- **Real-time status overlay** (shows active box and pinch state)
- **Color-coded states**:
  - <span style="color:purple">■</span> Purple = Ready
  - <span style="color:green">■</span> Green = Dragging
- **Pinch point indicator** (red circle at contact point)
