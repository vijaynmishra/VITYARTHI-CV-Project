# VISIONCOUNT AI

## Real-Time Hand and Finger Number Identifier Using Computer Vision

### Project Report

---

## Abstract

VisionCount AI is a lightweight, browser-based computer vision application designed to recognize and count the number of fingers displayed by a user in real time. The system can identify numbers from **0 to 10** using one or two hands placed in front of a standard webcam.

The application uses **Google MediaPipe Hands** for real-time hand landmark detection and employs geometric and vector-based calculations to determine whether individual fingers are extended or folded. Unlike conventional computer vision applications that depend on heavy server-side processing or locally installed machine-learning frameworks, VisionCount AI performs inference entirely within the user's browser.

The project follows a **privacy-first, client-side architecture**, ensuring that camera frames do not need to be transmitted to a remote server. HTML5, CSS3, and Vanilla JavaScript are used to construct the application interface and processing pipeline. WebAssembly and WebGL acceleration provided through the MediaPipe ecosystem enable efficient real-time processing.

The application additionally provides temporal smoothing, visual hand-skeleton overlays, finger-level status information, webcam controls, and synthesized audio feedback. These features make the system suitable for educational applications, touchless interfaces, accessibility-oriented prototypes, and demonstrations of browser-based computer vision.

**Keywords:** Computer Vision, MediaPipe Hands, Hand Gesture Recognition, WebAssembly, WebGL, Human-Computer Interaction, Finger Detection, JavaScript, Edge AI.

---

# 1. Introduction

Human-Computer Interaction (HCI) traditionally relies on physical input mechanisms such as keyboards, mice, touchscreens, and other conventional controllers. Although these methods are effective, there are situations where physical interaction is inconvenient or undesirable.

Touchless interaction can be particularly useful in environments such as healthcare facilities, public kiosks, classrooms, smart environments, and accessibility-oriented systems. Hand gestures provide a natural method of communication because they allow users to interact with digital systems without physically touching an input device.

Computer vision provides the ability to interpret visual information captured through cameras. Recent browser technologies have made it possible to perform increasingly complex computer vision operations directly on consumer devices.

**VisionCount AI** explores this capability by creating a real-time web application that detects human hands through a webcam and determines the number of extended fingers. The application recognizes numbers from **0 to 10**, allowing users to represent larger numbers by combining both hands.

The primary objective is to demonstrate that useful computer vision functionality can be implemented directly in a web browser without requiring a dedicated backend server or complex development environment.

---

# 2. Problem Statement

Traditional computer interaction systems depend heavily on physical input devices. These devices may not always be suitable for touchless environments, accessibility applications, educational demonstrations, or situations where physical contact is undesirable.

Existing computer vision and gesture-recognition systems can also introduce several challenges:

* Requirement for complex local installations.
* Dependence on large machine-learning frameworks.
* Requirement for GPU-enabled environments in some implementations.
* Potential privacy concerns when camera feeds are sent to remote servers.
* Network latency when video frames are processed remotely.
* Higher infrastructure and deployment costs.
* Difficulty for beginners who want to experiment with computer vision.

Therefore, there is a need for a lightweight system capable of recognizing basic hand gestures directly on the user's device.

VisionCount AI addresses this problem through a browser-based, client-side computer vision system that processes webcam input locally.

---

# 3. Objectives

The major objectives of VisionCount AI are:

1. To develop a real-time hand gesture recognition system using a standard webcam.
2. To recognize finger counts from **0 to 10**.
3. To detect up to five extended fingers on a single hand.
4. To combine two hands to recognize values from 6 to 10.
5. To perform computer vision processing entirely on the client side.
6. To minimize dependence on backend infrastructure.
7. To provide a privacy-oriented approach where camera frames remain on the user's device.
8. To reduce recognition flickering using temporal smoothing.
9. To provide real-time visual feedback through an interactive HUD.
10. To provide optional audio feedback whenever a stable number changes.
11. To create a zero-installation web application compatible with modern browsers.
12. To demonstrate practical applications of browser-based computer vision and HCI.

---

# 4. Scope of the Project

## 4.1 In-Scope Features

The project includes the following functionality:

### Client-Side Processing

All hand detection and classification operations are performed locally in the browser. The application does not require a dedicated backend server for video processing.

### Single-Hand Recognition

The application recognizes values from 0 to 5 using a single hand.

Examples include:

* 0 — Closed fist
* 1 — One extended finger
* 2 — Two extended fingers
* 3 — Three extended fingers
* 4 — Four extended fingers
* 5 — Open hand

### Dual-Hand Recognition

Both hands can be detected simultaneously. Their finger counts are combined to represent numbers from 6 to 10.

### Geometric Finger Classification

The application uses hand landmarks and geometric relationships between joints to determine whether fingers are extended.

### Temporal Smoothing

A rolling-window majority voting mechanism is used to reduce temporary recognition errors and visual flickering.

### Visual Feedback

The application displays detected hand landmarks and skeletal connections over the webcam feed.

### Audio Feedback

The Web Audio API is used to generate synthesized tones when a new stable number is detected.

### Camera Controls

The application provides controls for camera selection, mirroring, and skeleton visibility.

---

## 4.2 Out-of-Scope Features

The following functionality is intentionally excluded:

* Full sign-language recognition.
* Complete ASL or BSL vocabulary recognition.
* Complex dynamic gestures such as waving or swiping.
* Gesture trajectory tracking.
* Server-side storage of camera data.
* User authentication.
* Cloud-based video processing.
* Large-scale gesture datasets and model training.

---

# 5. Target Users

VisionCount AI can be useful for several categories of users.

## 5.1 Students and Educators

The application can be used to demonstrate:

* Computer vision.
* Human-computer interaction.
* Machine learning concepts.
* Browser-based AI.
* Hand landmark detection.

It can also be incorporated into basic counting and mathematics activities.

## 5.2 Accessibility Applications

A gesture-based numerical input system can serve as a prototype for alternative interaction mechanisms for individuals who may find traditional input devices difficult to use.

## 5.3 Developers and Researchers

Developers can use the project as an example of integrating computer vision capabilities into a browser without creating a Python or C++ backend.

## 5.4 Smart Environment Designers

The project can serve as a foundation for touchless interaction systems in:

* Smart kiosks.
* Smart mirrors.
* Interactive displays.
* Gaming applications.
* Touch-free interfaces.

---

# 6. Technologies Used

| Technology         | Purpose                                        |
| ------------------ | ---------------------------------------------- |
| HTML5              | Application structure and webcam interface     |
| CSS3               | User interface styling and animations          |
| Vanilla JavaScript | Application logic and computer vision pipeline |
| MediaPipe Hands    | Hand landmark detection                        |
| WebAssembly        | Efficient browser-side execution               |
| WebGL              | Hardware-accelerated processing                |
| Web Audio API      | Audio feedback                                 |
| HTML Canvas        | Hand skeleton and visual overlay               |
| Webcam API         | Camera access                                  |

The project deliberately avoids frameworks such as React, Angular, or Vue to keep the application lightweight and easy to understand.

---

# 7. System Architecture

VisionCount AI follows a client-side processing architecture.

### High-Level Flow

```text
                 USER
                   |
                   v
             Webcam Camera
                   |
                   v
          Browser Camera API
                   |
                   v
          MediaPipe Hands
                   |
                   v
       21 Hand Landmarks / Hand
                   |
                   v
       Geometric Finger Analysis
                   |
                   v
        Finger State Detection
                   |
                   v
         Temporal Smoothing
                   |
                   v
        Number Identification
              (0 - 10)
              /       \
             /         \
            v           v
      Visual HUD    Audio Feedback
```

The important characteristic of this architecture is that processing takes place locally within the browser.

---

# 8. Working Principle

The application follows a sequence of steps to identify the user's finger count.

## Step 1: Camera Initialization

When the user selects **Launch Camera**, the browser requests permission to access the webcam.

After permission is granted, the camera continuously provides video frames.

## Step 2: Hand Detection

The webcam frames are passed to MediaPipe Hands.

MediaPipe identifies hands and provides a collection of hand landmarks.

A detected hand contains **21 landmarks** representing important locations such as:

* Wrist
* Thumb joints
* Index finger joints
* Middle finger joints
* Ring finger joints
* Pinky finger joints

## Step 3: Landmark Processing

The detected landmark coordinates are processed by JavaScript.

Instead of directly relying on the position of the hand in the image, the system evaluates geometric relationships between the landmarks.

This makes the classification less dependent on the absolute position of the hand.

## Step 4: Finger Classification

Each finger is classified as either:

```text
EXTENDED
or
FOLDED
```

The system evaluates distances and geometric relationships involving the relevant finger joints and palm/wrist landmarks.

For example, an extended finger generally places its fingertip farther from the palm compared with a folded finger.

## Step 5: Finger Counting

After determining the state of each finger, the application counts the extended fingers.

For a single hand:

```text
0 + 0 + 0 + 0 + 0 = 0
```

through

```text
1 + 1 + 1 + 1 + 1 = 5
```

When two hands are detected:

```text
Left-hand count + Right-hand count
```

can produce values up to 10.

## Step 6: Temporal Smoothing

Individual video frames can occasionally produce incorrect classifications because of:

* Hand movement.
* Camera noise.
* Partial occlusion.
* Borderline finger positions.
* Detection jitter.

To reduce these effects, VisionCount AI stores recent predictions in a rolling window.

The most frequently occurring prediction in that window is treated as the stable result.

## Step 7: Output

The final result is displayed through the application's HUD.

The interface can show:

* Current number.
* Hand landmarks.
* Finger states.
* Hand information.
* Camera status.
* Audio feedback.

---

# 9. MediaPipe Hands

MediaPipe Hands is the primary computer vision component used by the application.

Instead of requiring the developer to manually implement a complete hand-detection model, MediaPipe provides hand landmark estimation.

The output consists of 21 landmarks for each detected hand.

A simplified representation is:

```text
                 Fingertips
              8   12   16   20
              |    |    |    |
             Index Middle Ring Pinky
              |    |    |    |
              |    |    |    |
              5    9   13   17
               \    |    |   /
                  Palm
                    |
                   0
                 Wrist
```

These landmarks form the basis of the geometric finger classification system.

---

# 10. Finger Classification Algorithm

The classification engine determines whether each finger is extended.

The basic concept is based on geometric relationships between the fingertip, finger joints, palm, and wrist.

For a finger, the application can analyze the relative position and distance of its fingertip compared with relevant lower joints.

A simplified distance calculation can be represented as:

$$
d = \sqrt{(x_2-x_1)^2+(y_2-y_1)^2}
$$

where:

* \(x_1,y_1\) represent one landmark.
* \(x_2,y_2\) represent another landmark.
* \(d\) represents the Euclidean distance between them.

By comparing appropriate distances, the system determines whether the finger is likely extended.

This approach avoids requiring a separate machine-learning classifier for every possible finger-count gesture.

---

# 11. Temporal Smoothing

Raw computer vision predictions can change rapidly between frames.

For example:

```text
Frame 1 → 3
Frame 2 → 3
Frame 3 → 4
Frame 4 → 3
Frame 5 → 3
```

Displaying every raw prediction would cause the UI to flicker.

VisionCount AI instead maintains a rolling prediction window:

```text
[3, 3, 4, 3, 3]
```

The system determines the most frequent result.

In this example:

```text
3 → 4 occurrences
4 → 1 occurrence
```

Therefore, the stable output becomes:

```text
3
```

This significantly improves the perceived stability of the application.

---

# 12. User Interface

The project uses a cyber-glass or futuristic HUD-style interface.

Major UI components include:

### Webcam Display

Shows the live camera feed.

### Skeleton Overlay

Displays detected hand landmarks and connections.

### Number Badge

Displays the currently recognized number prominently.

### Finger Indicators

Shows the state of:

* Thumb
* Index
* Middle
* Ring
* Pinky

for detected hands.

### Status Indicators

Provide information about:

* Camera state.
* Detection state.
* Current gesture.
* Audio state.

---

# 13. Audio Feedback

VisionCount AI incorporates the Web Audio API to provide optional audio feedback.

When a new stable number is recognized, the application can generate a synthesized tone.

For example:

```text
Detected number changes:
2 → 3
```

The application produces an audio chime corresponding to the new stable detection.

This provides feedback without requiring the user to continuously look at the screen.

---

# 14. Camera Management

The application supports multiple camera-related controls.

Users can:

* Select available camera devices.
* Switch between front and rear cameras where supported.
* Enable or disable horizontal mirroring.
* Enable or disable the hand skeleton overlay.

These features make the application more adaptable to different devices and usage environments.

---

# 15. Privacy and Security

Privacy is an important design principle of VisionCount AI.

The application is designed around client-side processing.

The general data flow is:

```text
Camera
   ↓
User Device
   ↓
Browser
   ↓
MediaPipe
   ↓
Prediction
```

There is no requirement for:

```text
Camera
   ↓
Internet
   ↓
Remote Server
```

for the core computer vision operation.

Consequently, the project does not need to upload raw webcam frames to a backend server.

This architecture can reduce privacy risks associated with transmitting camera footage and also eliminates the need to maintain video-processing infrastructure.

However, users still need to grant their browser permission to access the camera.

---

# 16. Cross-Platform Compatibility

The application is designed to operate in modern web browsers supporting the required web APIs and MediaPipe functionality.

Potential supported environments include:

* Google Chrome
* Microsoft Edge
* Mozilla Firefox
* Safari

The application can be used on:

* Desktop computers.
* Laptops.
* Compatible smartphones.
* Devices with external webcams.

Actual performance may vary depending on the device's CPU, GPU, browser implementation, camera resolution, and available hardware acceleration.

---

# 17. Project Structure

The project consists of a small number of files:

```text
VisionCount-AI/
│
├── index.html
│
├── style.css
│
├── app.js
│
└── README.md
```

### index.html

Contains the structure of the web application, including the camera interface, HUD elements, controls, and dashboard components.

### style.css

Responsible for:

* Glassmorphism styling.
* Layout.
* Animations.
* HUD effects.
* Status indicators.
* Responsive design.

### app.js

Contains the core application logic, including:

* MediaPipe initialization.
* Webcam handling.
* Hand landmark processing.
* Finger classification.
* Number calculation.
* Temporal smoothing.
* Audio feedback.
* Canvas rendering.

### README.md

Contains project documentation, installation instructions, usage information, and deployment instructions.

---

# 18. Implementation and Deployment

One of the major advantages of VisionCount AI is its simple deployment process.

No traditional backend installation is required.

For local development, a basic HTTP server can be used:

```bash
git clone <repository>
cd VITYARTHI-CV-Project
python -m http.server 8080
```

The application can then be accessed through:

```text
http://localhost:8080
```

The project can also be deployed using static hosting platforms such as GitHub Pages, Netlify, or Vercel.

This makes the application suitable for demonstrations and educational environments.

---

# 19. Advantages

VisionCount AI provides several advantages.

### 19.1 No Backend Required

The application does not need a dedicated server for its core processing.

### 19.2 Privacy-Oriented

Camera processing is performed locally rather than requiring raw video transmission to a remote server.

### 19.3 Easy Deployment

The application consists primarily of static web files.

### 19.4 Low Entry Barrier

Users do not need to install Python, PyTorch, TensorFlow, or other heavy development environments.

### 19.5 Real-Time Interaction

The system is designed for continuous webcam processing and immediate feedback.

### 19.6 Accessibility Potential

The project demonstrates an alternative method of numerical input that does not require traditional physical controls.

### 19.7 Educational Value

The project combines several important technologies:

* Computer vision.
* Geometry.
* JavaScript.
* Web APIs.
* WebAssembly.
* Human-computer interaction.

---

# 20. Limitations

Despite its advantages, the system has several limitations.

## 20.1 Lighting Conditions

Poor lighting can negatively affect hand landmark detection.

## 20.2 Occlusion

When fingers overlap significantly, classification can become difficult.

## 20.3 Extreme Hand Angles

Although geometric calculations improve robustness, extreme rotations or orientations may still cause incorrect predictions.

## 20.4 Camera Quality

Low-resolution or noisy cameras may reduce detection accuracy.

## 20.5 Gesture Ambiguity

Some finger configurations may be difficult to distinguish using simple geometric heuristics.

## 20.6 Browser Performance

Real-time performance depends on the user's device and browser.

## 20.7 Limited Gesture Vocabulary

The application recognizes numerical finger counts rather than a complete sign language.

---

# 21. Applications

The technology demonstrated by VisionCount AI can be extended to several applications.

### Educational Applications

The system can be used for:

* Counting exercises.
* Interactive mathematics.
* Children's learning games.
* Computer vision demonstrations.

### Touchless Kiosks

Users could interact with a kiosk without touching the screen.

### Smart Classrooms

Teachers could use gestures as an input mechanism for interactive presentations or quizzes.

### Gaming

Finger-count recognition could be used as a simple game-control mechanism.

### Accessibility

The system could serve as a prototype for alternative input interfaces.

### Smart Environments

Gesture recognition can be incorporated into smart mirrors, displays, and other interactive environments.

---

# 22. Future Enhancements

The project can be extended in several directions.

## 22.1 Gesture Recognition

Additional static gestures could be recognized beyond numerical finger counts.

## 22.2 Sign Language Recognition

The system could be expanded toward recognition of a larger vocabulary of sign-language gestures.

## 22.3 Dynamic Gesture Recognition

Future versions could recognize gestures such as:

* Swipe.
* Wave.
* Circular movement.
* Pointing.
* Drawing in the air.

## 22.4 Machine-Learning Classifier

A trained classifier could potentially improve recognition of more complex gestures.

## 22.5 Accessibility Controls

The system could be integrated with keyboard shortcuts, screen controls, or assistive technologies.

## 22.6 Gesture-Based Applications

The recognition engine could be used to control:

* Slideshows.
* Music players.
* Games.
* Smart-home interfaces.

## 22.7 Improved Mobile Optimization

Further optimization could improve battery usage and performance on smartphones.

---

# 23. Testing

Testing should be performed under different environmental and user conditions.

| Test Condition                   | Expected Result |
| -------------------------------- | --------------- |
| Closed fist                      | 0               |
| One finger extended              | 1               |
| Two fingers extended             | 2               |
| Three fingers extended           | 3               |
| Four fingers extended            | 4               |
| Open palm                        | 5               |
| Two hands totaling six fingers   | 6               |
| Two hands totaling seven fingers | 7               |
| Two hands totaling eight fingers | 8               |
| Two hands totaling nine fingers  | 9               |
| Two open hands                   | 10              |

Additional testing should be performed under:

* Different lighting conditions.
* Different camera distances.
* Different hand orientations.
* Different webcams.
* Different browsers.
* Single- and dual-hand scenarios.

---

# 24. Expected Results

The completed application is expected to:

1. Access the user's webcam after permission is granted.
2. Detect one or two hands.
3. Identify the relevant hand landmarks.
4. Determine the state of individual fingers.
5. Calculate the total number of extended fingers.
6. Stabilize predictions using temporal smoothing.
7. Display the detected number in real time.
8. Display the hand skeleton and finger status.
9. Provide optional audio feedback.
10. Operate without requiring a dedicated backend server.

The expected output is a responsive and interactive browser-based finger-counting system.

---

# 25. Conclusion

VisionCount AI demonstrates how modern browser technologies can be combined with computer vision to create an interactive, lightweight, and privacy-oriented human-computer interaction system.

The project uses MediaPipe Hands to detect hand landmarks and applies geometric reasoning to classify individual fingers. The resulting finger counts are combined to recognize numbers from 0 to 10. Temporal smoothing improves stability, while the cyber-glass HUD and audio feedback provide an interactive user experience.

One of the most significant aspects of the project is its client-side architecture. By processing camera input locally within the browser, VisionCount AI avoids the need for a dedicated video-processing backend and reduces the need to transmit raw camera footage over a network.

The project therefore serves both as a practical gesture-recognition application and as an educational demonstration of **computer vision, browser-based AI, WebAssembly, WebGL, JavaScript, and human-computer interaction**.

With further development, the same architecture could serve as the foundation for more advanced touchless interfaces, accessibility tools, educational systems, and gesture-controlled applications.

---

# 26. References

1. Google MediaPipe — Hand Landmark Detection documentation.
2. Web APIs — MediaDevices and MediaStream documentation.
3. Web Audio API documentation.
4. HTML5 Canvas API documentation.
5. WebAssembly documentation.
6. WebGL documentation.
7. JavaScript documentation.
8. VisionCount AI project source repository and project documentation.

---

## Project Summary

**Project Name:** VisionCount AI

**Domain:** Computer Vision / Human-Computer Interaction

**Frontend:** HTML5, CSS3, Vanilla JavaScript

**Computer Vision:** MediaPipe Hands

**Recognition Range:** 0–10

**Processing:** Client-side

**Backend:** Not required

**Input:** Webcam

**Output:** Finger count, visual HUD, audio feedback

**Deployment:** Static web hosting

**Primary Goal:** Real-time, privacy-oriented finger-count recognition directly in a web browser.
