# RepSense --- AI Gym Coach

RepSense is a computer vision-based gym coach that tracks exercises,
analyzes form, counts repetitions, and provides real-time voice
feedback.

## Features

-   Real-time exercise tracking using a webcam
-   Human pose detection with MediaPipe
-   Automatic repetition counting
-   Exercise-specific form analysis
-   Joint-angle based movement detection
-   Support for multiple exercises
-   AI-generated coaching feedback using Groq
-   Text-to-speech feedback using gTTS
-   Interactive Streamlit interface
-   Workout session and exercise metrics tracking

## Supported Exercises

-   Squats
-   Push-ups
-   Biceps Curls (Dumbbell)
-   Shoulder Press
-   Lunges

## How It Works

``` text
Webcam
   ↓
WebRTC Video Stream
   ↓
MediaPipe Pose Detection
   ↓
Exercise Detector
   ↓
Joint Angle & Form Analysis
   ↓
Rep / Set Tracking
   ↓
Groq LLM
   ↓
Coaching Feedback
   ↓
gTTS
   ↓
Voice Feedback
```

## Tech Stack

  Technology         Purpose
  ------------------ -------------------------------------------
  Python             Core development
  Streamlit          Web application interface
  Streamlit-WebRTC   Real-time webcam streaming
  MediaPipe          Pose and landmark detection
  OpenCV             Computer vision processing
  Groq               LLM-based coaching feedback
  gTTS               Text-to-speech
  SQLite             Data persistence
  Pandas             Data handling
  python-dotenv      Environment variable management
  uv                 Python package and environment management

## Project Structure

``` text
RepSense/
│
├── core/
│   └── base_exercise.py
│
├── detectors/
│   ├── squat_detector.py
│   ├── pushup_detector.py
│   ├── biceps_curl_detector.py
│   ├── shoulder_press_detector.py
│   └── lunge_detector.py
│
├── ml_models/
│
├── services/
│   ├── auth/
│   ├── coaching/
│   │   ├── llm.py
│   │   ├── tts.py
│   │   └── voice_pipeline.py
│   ├── config/
│   ├── persistence/
│   ├── state/
│   ├── tracking/
│   ├── ui/
│   └── vision/
│
├── static/
├── main.py
├── requirements.txt
├── .env
└── data.db
```


## Run the Application

``` bash
streamlit run main.py
```

Open the local Streamlit URL shown in the terminal and allow webcam
access.

## Exercise Detection

RepSense uses pose landmarks to calculate joint angles and determine
exercise stages.

For example, during a squat:

``` text
Hip → Knee → Ankle
```

The knee angle is calculated using the three landmarks.

A simplified squat flow is:

``` text
Standing
   ↓
Knee angle decreases
   ↓
Down position
   ↓
Knee angle increases
   ↓
Standing position
   ↓
Rep counted
```

The system also checks landmark visibility before using pose data to
reduce unreliable detections.

## AI Coaching Pipeline

The coaching system works in four main stages:

1.  The exercise detector identifies movement and form metrics.
2.  The coaching pipeline identifies relevant form issues.
3.  Groq generates a short coaching response.
4.  gTTS converts the response into speech.

Example:

``` text
Form Issue:
User is leaning too far forward during the squat.

AI Feedback:
"Keep your chest up and brace your core."
```

## Key Concepts

### Pose Detection

MediaPipe detects body landmarks such as the shoulders, hips, knees, and
ankles from the camera feed.

### Angle Calculation

Three landmarks are used to calculate a joint angle. The angle helps
determine exercise movement instead of relying only on raw pixel
coordinates.

### Rep Counting

The system uses movement stages and angle thresholds. A repetition is
counted only after the user moves through the required stages, helping
prevent multiple counts from a single position.

### Visibility Filtering

Landmarks with low visibility are ignored to reduce incorrect exercise
measurements when body parts are difficult to detect.

## Future Improvements

-   More exercise detectors
-   Improved form analysis
-   Personalized workout plans
-   Workout history and analytics
-   Better real-time audio streaming
-   More robust pose tracking under different camera angles
-   Mobile-friendly interface
-   Personalized coaching based on workout history

## Author

**Anurag Prajapati**

GitHub: https://github.com/Anurag1466
