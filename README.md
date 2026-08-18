# 🎵 Hand Gesture Volume Control

A real-time **hand gesture volume control system** built with Python, OpenCV, and MediaPipe. The application uses the computer's webcam to track the user's hand and controls the system volume based on the distance between the **thumb** and **index finger**.

## 📌 Project Overview

This project demonstrates how computer vision and hand tracking can be used to create a **touch-free human-computer interaction system**.

The application detects the user's hand through the webcam and tracks specific hand landmarks:

- **Landmark 4** → Thumb tip
- **Landmark 8** → Index finger tip

The distance between these two points determines whether the system increases or decreases the volume.

### 🤏 How the Gesture Works

```text
Thumb + Index Finger

   👆
    |
    |       Close
    ↓        ↓
   ●──●     🔉 Volume Down


   ●             ●
   ↑             ↑
 Thumb        Index
      Far Apart
          ↓
       🔊 Volume Up
```

The farther the thumb and index finger are from each other, the stronger the volume-up gesture. When they are close together, the application triggers volume down.

## 🛠️ Technologies Used

- **Python**
- **OpenCV** — webcam access and image processing
- **MediaPipe** — real-time hand landmark detection
- **PyAutoGUI** — sending system volume keyboard commands
- **Computer Vision**
- **Gesture Recognition**

## 📂 Project Structure

```text
hand_gesture/
│
├── volume_control.py
├── requirements.txt
└── README.md
```

## ⚙️ Installation

It is recommended to use a **Python 3.11** environment for compatibility with MediaPipe.

Install the required dependencies:

```bash
pip install opencv-python mediapipe==0.10.21 pyautogui
```

Or, if a `requirements.txt` file is included:

```bash
pip install -r requirements.txt
```

## 🚀 How to Run

Clone the repository:

```bash
git clone https://github.com/USERNAME/REPOSITORY_NAME.git
```

Navigate to the project:

```bash
cd hand_gesture
```

Run the program:

```bash
python volume_control.py
```

Your webcam will open and begin detecting your hand.

### ⌨️ Controls

Press **ESC** to stop the program and close the webcam window.

## 🧠 How It Works

### 1. Webcam Capture

OpenCV accesses the computer's webcam:

```python
webcam = cv2.VideoCapture(0)
```

Each frame is captured and processed in real time.

### 2. Hand Detection

MediaPipe Hands detects the hand and its landmarks:

```python
my_hands = mp.solutions.hands.Hands()
```

The image is converted to RGB before being processed:

```python
rgb_image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
output = my_hands.process(rgb_image)
```

### 3. Landmark Tracking

The program tracks the coordinates of the thumb and index fingertips:

```python
if id == 8:
    x1, y1 = x, y

if id == 4:
    x2, y2 = x, y
```

The coordinates are converted into pixel positions:

```python
x = int(landmark.x * frame_width)
y = int(landmark.y * frame_height)
```

### 4. Distance Calculation

The Euclidean distance between the thumb and index finger is calculated:

```python
dist = ((x2 - x1) ** 2 + (y2 - y1) ** 2) ** 0.5
```

A scaling factor is then applied to the distance.

### 5. Volume Control

The distance determines which keyboard command is sent:

```python
if dist > 50:
    pyautogui.press("volumeup")
else:
    pyautogui.press("volumedown")
```

Therefore:

| Gesture | Action |
|---|---|
| 🤏 Fingers close | Volume Down |
| 🤌 Fingers far apart | Volume Up |

## 🔍 Key Concepts

This project demonstrates several important computer vision concepts:

- Real-time video processing
- Hand detection
- Hand landmark extraction
- Coordinate transformation
- Euclidean distance calculation
- Gesture-based interaction
- Human-computer interaction
- Automation with Python

## ⚠️ Current Limitations

The current implementation is a simple demonstration and has some limitations:

- The volume changes repeatedly while a gesture is maintained.
- There is no smooth volume scaling.
- The distance threshold is fixed.
- Lighting conditions can affect hand detection.
- The system is primarily designed for one hand.
- `PyAutoGUI` sends volume keyboard commands rather than directly setting the exact system volume.

## 🚀 Future Improvements

Possible improvements include:

- 🎚️ Map finger distance directly to **0–100% volume**
- 📈 Add smooth volume transitions
- ⏱️ Add a delay/debounce mechanism to prevent repeated commands
- ✋ Support multiple hand gestures
- 👌 Add mute/unmute gestures
- 📊 Display the current volume level on screen
- 🔊 Use `PyCaw` for precise Windows volume control
- 🖐️ Add gesture recognition for play/pause and next/previous track
- 🎨 Improve the graphical interface

## 🎯 Learning Objectives

This project was created to explore how **computer vision and hand tracking can be combined with system automation** to create intuitive, touch-free interfaces.

It provides a foundation for more advanced gesture-controlled applications such as:

- Media controllers
- Presentation controllers
- Smart home interfaces
- Touchless computer interaction
- Accessibility tools
- Gesture-controlled applications

## 👩‍💻 Author

**Meriem Regoui**

Data Science & Artificial Intelligence  
École Nationale Polytechnique, Algeria

## 📄 License

This project is intended for educational and experimental purposes.