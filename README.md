# 🏋️ AI Real-Time Gym Coach

Track your reps, check your form, and get spoken feedback while you work out, all through your webcam.

I built this to make solo workouts easier to follow. It uses MediaPipe pose landmarks to count repetitions and check exercise-specific form, then turns workout events into short voice coaching with an LLM.

🔗 **[Live Demo](YOUR_LIVE_DEMO_LINK)**

## ✨ What it does

- Tracks five exercises: squats, push-ups, biceps curls, shoulder press, and lunges
- Counts reps and sets from joint angles and movement stages, not a timer
- Flags form issues like hip sagging, elbow drift, torso swinging, and balance changes
- Sends workout events and form issues to GPT-OSS-120B (via Groq), then reads the feedback out loud with gTTS
- Lets you pick an exercise, sets, and reps before you start
- Saves completed sets, reps, and workout duration in SQLite and shows your workout history

## 🛠️ Tech Stack

| Area | Tools |
| --- | --- |
| Computer vision | MediaPipe Pose Landmarker, OpenCV |
| Real-time video | Streamlit WebRTC, PyAV |
| Exercise analysis | Python, joint-angle calculations, rule-based state tracking |
| AI voice coach | Groq API (`openai/gpt-oss-120b`), gTTS |
| App and storage | Streamlit, SQLite, Pandas |

## ⚙️ How It Works

1. Choose an exercise and set your rep and set targets
2. Start the webcam. MediaPipe Pose Landmarker finds body landmarks in each frame
3. The exercise's detector calculates joint angles, counts completed reps, and flags form issues
4. The Streamlit dashboard updates live, and completed sets are saved to SQLite
5. When a workout event or form issue comes up, the Groq-powered coach writes a short message and gTTS speaks it

## 📷 Tips for Best Results

- Keep your full body in the frame
- Use good, even lighting
- Place the camera at a steady height, a few feet away
- Wear clothes that don't hide your joints

## 📁 Project Structure

```text
AI-REALTIME-GYM-COACH-V2/
├── main.py
├── requirements.txt
├── core/
│   └── base_exercise.py
├── detectors/
│   ├── squat.py
│   ├── pushup.py
│   ├── biceps_curl.py
│   ├── shoulder_press.py
│   └── lunges.py
├── services/
│   ├── auth/
│   ├── coaching/
│   ├── config/
│   ├── persistence/
│   ├── state/
│   ├── tracking/
│   ├── ui/
│   └── vision/
├── ml_models/
│   └── pose_landmarker_full.task
└── static/
    └── style.css
```

## 🚀 Run Locally

**1. Clone the repository**

```bash
git clone https://github.com/Faizan-2419/AI_GYM_COACH.git
cd AI_GYM_COACH/AI-REALTIME-GYM-COACH-V2
```

**2. Create a virtual environment**

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

macOS / Linux:

```bash
source .venv/bin/activate
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

**4. Add your Groq API key**

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key
```

Don't commit `.env` or any API key to GitHub. Without a key, the app still runs and counts reps, but you won't get voice coaching.

**5. Check the pose model**

The pose model is at `ml_models/pose_landmarker_full.task`. Keep it in that folder, because the app loads it from there.

**6. Start the app**

```bash
streamlit run main.py
```

Enter a username, set your workout plan, and allow camera access. The SQLite tables are created automatically on first run.

## ⚠️ Limitations

- Form checks use landmark geometry and thresholds I set by hand, so results can change with camera angle and body proportions
- Poor lighting or a partly hidden body lowers detection quality
- This is a project prototype, not a replacement for a qualified trainer or medical advice

## 💡 What I Learned

This project taught me how to connect real-time pose estimation, movement logic, an LLM, text-to-speech, and workout storage in one app. The hardest part was turning raw frame-by-frame landmarks into feedback that is actually useful, instead of just drawing a skeleton on screen.

## 👤 Author

**Faizanur Rahman**
B.Tech, Computer Science & Engineering
Interested in AI, Machine Learning, and Computer Vision.
