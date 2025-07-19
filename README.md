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


## 🛠️ Technical Implementation

### Core Classes

#### `DraggableBox` Class

| Method       | Parameters            | Functionality                          |
|--------------|-----------------------|----------------------------------------|
| `__init__()` | `pos_center`, `size`  | Initializes position, size, and visual properties |
| `update()`   | `img`, `lm_list`      | Handles pinch detection and dragging logic |
| `draw()`     | `img`                 | Renders box with transparency and border |

### Main Process Flow

1. **Camera Setup**  
   - Initializes video capture at 1280×720 resolution  
   - Configures frame rate and exposure settings  

2. **UI Initialization**  
   
   boxes = [
       DraggableBox([400, 300], [200, 200]),
       DraggableBox([800, 300], [200, 200])
   ]

### Main Tracking Loop

```python
while True:
    # Capture frame from webcam
    success, img = cap.read()
    img = cv2.flip(img, 1)  # Mirror display for intuitive movement
    
    # Hand detection (without drawing landmarks)
    hands = detector.findHands(img, draw=False)
    
    # Update and draw all draggable boxes
    for box in boxes:
        box.update(img, hands)  # Handle gestures and position
        box.draw(img)           # Render with transparency
    
    # Display performance metrics
    cv2.putText(img, f"FPS: {int(fps)}", (10, 70), 
               cv2.FONT_HERSHEY_PLAIN, 3, (255, 0, 255), 3)
    
    # Show final frame
    cv2.imshow("Hand-Controlled UI", img)
    
    # Exit when 'q' is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
