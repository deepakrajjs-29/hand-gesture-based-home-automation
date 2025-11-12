# 🤚 Hand Gesture Control System

<div align="center">

![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)
![OpenCV](https://img.shields.io/badge/OpenCV-4.5+-green.svg) 
![MediaPipe](https://img.shields.io/badge/MediaPipe-Latest-orange.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

**Control your devices with simple hand gestures! 👋**

[Features](#-features) • [Installation](#-installation) • [Usage](#-usage) • [How It Works](#-how-it-works) • [Gestures](#-gesture-controls) 

</div> 

--- 

## 📋 Overview

This intelligent gesture recognition system uses your webcam and MediaPipe's hand tracking to control virtual devices (fan and light) through intuitive hand gestures. Perfect for learning computer vision, building smart home prototypes, or creating interactive applications!

## ✨ Features

- 🎯 **Real-time Hand Detection** - Instant gesture recognition using MediaPipe
- 👆 **Finger Counting** - Accurate detection of extended fingers
- 🌀 **Fan Control** - Toggle fan with open/closed hand gestures
- 💡 **Light Control** - Control lights with 2-3 finger gestures
- 📊 **Live Status Display** - On-screen feedback of finger count and device states
- 🎨 **Visual Hand Landmarks** - See your hand skeleton in real-time

## 🛠️ Installation

### Prerequisites

- Python 3.7 or higher
- Webcam/Camera
- Operating System: Windows, macOS, or Linux

### Step 1: Clone or Download

```bash
# Create a project directory
mkdir gesture-control
cd gesture-control
```

### Step 2: Install Dependencies

```bash
# Install required packages
pip install opencv-python mediapipe
```

**Or use requirements.txt:**

```bash
# Create requirements.txt with:
opencv-python>=4.5.0
mediapipe>=0.10.0

# Then install
pip install -r requirements.txt
```

## 🚀 Usage

### Running the Application

1. **Start the program:**
   ```bash
   python gesture_control.py
   ```

2. **Position your hand** in front of the webcam (well-lit environment recommended)

3. **Perform gestures** to control devices (see gesture guide below)

4. **Exit:** Press `ESC` key to quit

### 👋 Gesture Controls

| Gesture | Fingers | Action | Device |
|---------|---------|--------|--------|
| ✋ **Open Hand** | 5 fingers up | Turn ON | 🌀 Fan |
| ✊ **Closed Fist** | 0 fingers up | Turn OFF | 🌀 Fan |
| ✌️ **Peace Sign** | 3 fingers up | Turn ON | 💡 Light |
| 🤘 **Two Fingers** | 2 fingers up | Turn OFF | 💡 Light |

### 💡 Tips for Best Results

- ✅ Use good lighting conditions
- ✅ Keep hand within frame (not too close/far)
- ✅ Make clear, distinct gestures
- ✅ Wait briefly between gesture changes
- ✅ Use a plain background for better detection

## 🔧 How It Works

### Architecture Flow

```
📹 Webcam Feed
    ↓
🖼️ Frame Capture & Flip
    ↓
🎨 BGR → RGB Conversion
    ↓
🤖 MediaPipe Hand Detection
    ↓
📊 Extract Hand Landmarks
    ↓
🔢 Count Extended Fingers
    ↓
⚙️ Gesture Recognition Logic
    ↓
🎯 Device Control Action
    ↓
📺 Display Status on Screen
```

### Core Components

#### 1. **Hand Detection** 🖐️
```python
mp_hands.Hands(max_num_hands=1, min_detection_confidence=0.7)
```
- Detects up to 1 hand
- 70% confidence threshold for stability

#### 2. **Finger Counting Algorithm** 🔢

**Thumb Detection:**
- Compares thumb tip X-position with thumb joint
- Extended if tip is left of joint

**Other Fingers:**
- Compares fingertip Y-position with finger middle joint
- Extended if tip is above (lower Y value) the joint

#### 3. **State Management** 🎛️
- Tracks `fan_on` and `light_on` boolean states
- Prevents repeated triggering with state checks
- Provides console and on-screen feedback

## 📁 Project Structure

```
gesture-control/
│
├── gesture_control.py      # Main application script
├── requirements.txt        # Python dependencies
└── README.md              # This file
```

## 🎮 Control Logic

### Fan Control Flow
```
5 Fingers Detected + Fan OFF → Turn Fan ON
0 Fingers Detected + Fan ON → Turn Fan OFF
```

### Light Control Flow
```
3 Fingers Detected + Light OFF → Turn Light ON
2 Fingers Detected + Light ON → Turn Light OFF
```

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| **Camera not opening** | Check camera permissions & close other apps using camera |
| **Poor detection** | Improve lighting, use plain background, adjust camera angle |
| **Lag/Slow performance** | Reduce `min_detection_confidence` or upgrade hardware |
| **Hand not detected** | Ensure hand is fully visible, not too close/far from camera |
| **Wrong finger count** | Make clear gestures, keep fingers straight and separated |

## 🔬 Technical Details

### MediaPipe Hand Landmarks

The system tracks 21 hand landmarks (0-20):

- **Landmark 4:** Thumb tip
- **Landmark 8:** Index finger tip
- **Landmark 12:** Middle finger tip
- **Landmark 16:** Ring finger tip
- **Landmark 20:** Pinky tip

### Key Parameters

```python
max_num_hands=1              # Track single hand
min_detection_confidence=0.7 # Detection threshold
```

## 🚀 Future Enhancements

- [ ] Add more gesture commands (volume control, etc.)
- [ ] Integrate with real IoT devices (Arduino, Raspberry Pi)
- [ ] Support for two-hand gestures
- [ ] Gesture customization interface
- [ ] Mobile app version
- [ ] Voice feedback system
- [ ] Gesture recording and playback
- [ ] Machine learning for custom gestures

## 🤝 Integration with Real Devices

To control actual hardware:

### Arduino Example
```python
import serial
arduino = serial.Serial('COM3', 9600)  # Your Arduino port

# In your gesture detection:
if finger_count == 5 and not fan_on:
    arduino.write(b'F')  # Send 'F' to Arduino
    fan_on = True
```

### Raspberry Pi Example
```python
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)
GPIO.setup(17, GPIO.OUT)  # Fan pin

# In your gesture detection:
if finger_count == 5 and not fan_on:
    GPIO.output(17, GPIO.HIGH)
    fan_on = True
```

## 📚 Learning Resources

- [MediaPipe Hands Documentation](https://google.github.io/mediapipe/solutions/hands.html)
- [OpenCV Python Tutorials](https://docs.opencv.org/master/d6/d00/tutorial_py_root.html)
- [Computer Vision Basics](https://opencv.org/)

## 🙏 Credits

Built with:
- **MediaPipe** - Google's ML solution for hand tracking
- **OpenCV** - Computer vision library
- **Python** - Programming language

## 📄 License

This project is licensed under the MIT License - feel free to use, modify, and distribute!

## 🌟 Support

If you found this helpful:
- ⭐ Star the repository
- 🐛 Report bugs via issues
- 💡 Suggest new features
- 🤝 Contribute improvements

---

<div align="center">

**Made with ❤️ and gestures 👋**

*Happy Coding! 🚀*

</div>
