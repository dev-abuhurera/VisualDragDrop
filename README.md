Visual Drag-and-Drop with Hand Tracking

This project implements hand gesture-based drag-and-drop using OpenCV and hand landmark detection. Users can pinch and drag semi-transparent boxes on the screen using their fingers, with real-time visual feedback.

📌 Features
✅ Hand Tracking – Detects hand landmarks using MediaPipe.
✅ Pinch-to-Drag – Uses finger distance to detect pinch gestures.
✅ Semi-Transparent Boxes – Draggable UI elements with alpha blending.
✅ Debounce Logic – Prevents false triggers by requiring sustained pinch.
✅ Multi-Box Support – Multiple draggable boxes with independent controls.

🚀 How It Works

1. Hand Detection & Landmark Tracking
Uses HandTrackingModule (based on MediaPipe) to detect hand landmarks.

Tracks index (8) and middle (12) finger positions for pinch detection.

2. Pinch Gesture Detection
   
Calculates the distance between index and middle fingers.

If distance < PINCH_THRESHOLD (default: 35px), registers as a pinch.

Uses debounce logic (DEBOUNCE_THRESHOLD = 5) to avoid accidental triggers.

3. Dragging Logic
When a pinch is detected inside a box:

The box turns green (active state).

The box moves with the average position of the two fingers + an offset for smooth dragging.

On release, the box returns to its original color (purple).

4. Visual Feedback
Semi-transparent boxes (alpha = 80) for a modern UI feel.

Red circle appears at the pinch point when dragging.

Status text shows which box is currently active.

🛠️ Code Structure
DraggableBox Class
Method	Description
__init__(pos_center, size)	Initializes box position, size, and appearance.
update(img, lm_list, ...)	Handles pinch detection, dragging logic, and position updates.
draw(img)	Renders the box with transparency and outline.
main() Function
Initializes camera (1280x720 resolution).

Creates multiple draggable boxes at predefined positions.

Processes hand tracking and updates box positions in real time.

Displays status (active box, pinch threshold).

🔧 Usage
1. Install Dependencies
bash
Copy

pip install opencv-python numpy mediapipe

3. Run the Program
bash
Copy

python drag_and_drop.py

5. Controls

Pinch inside a box to drag it.

Release fingers to drop the box.

Press 'q' to exit.

🎯 Possible Improvements
🔹 Add collision detection between boxes.
🔹 Implement snapping to a grid or other UI elements.
🔹 Add touch gestures (double-tap to delete, swipe to rotate).
🔹 Optimize performance for smoother dragging.

📸 Demo Screenshot
(Example of boxes being dragged with hand tracking)

![image](https://github.com/user-attachments/assets/a11ae582-d54c-4075-8d70-6a45cafb12ac)
