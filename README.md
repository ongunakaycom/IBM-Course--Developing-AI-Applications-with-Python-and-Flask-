# IBM Emotion Detection App - Python Flask AI Microservice

**IBM Emotion Detection** is a lightweight AI-powered web app that analyzes emotions in text using IBM Watson’s NLP service. It’s built using Python and Flask, perfect for understanding emotion semantics in user-generated content, customer feedback, and social posts.

---

## 🚀 Project Overview

- **Frontend:** HTML + JavaScript
- **Backend:** **Python Flask** app
- **AI Service:** IBM Watson NLP for Emotion Prediction
- **Styling & UI:** Minimal HTML + JS
- **Deployment:** Can be deployed locally or on IBM Cloud
- **CI/CD:** GitHub + optional Flask deployment workflows

---

## 🛠️ Key Features

- Real-time emotion detection from raw text input
- Uses IBM Watson NLP for sentiment & emotion classification
- RESTful API endpoint for emotion prediction
- Clean and minimal HTML frontend
- Returns scores for: joy, anger, sadness, fear, and disgust
- Highlights **dominant emotion** detected from text

---

## ⚙️ DevOps & CI/CD Setup (Optional)

You can set up GitHub Actions or other CI/CD tools for:

- Linting (via `flake8`)
- Unit testing (via `unittest` or `pytest`)
- Automated deployment (to Heroku, IBM Cloud, etc.)

---

## 🔧 Getting Started

### Prerequisites

- Python 3.10+
- `requests`, `Flask`, etc.

### Setup

```bash
git clone https://github.com/ongunakaycom/ibm-emotion-detection-flask-app.git
cd ibm-emotion-detection-flask-app

python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

pip install -r requirements.txt
python EmotionDetection/emotion_detection.py  # test module
flask run
```

> App runs locally at: http://127.0.0.1:5000

---

## 🧪 Testing

You can run basic Python tests for your `emotion_detection.py` module:

```bash
python -m unittest discover
# or run specific test file if available
```

---

## 📁 Project Structure Highlights

```
/
├── EmotionDetection/
│   └── emotion_detection.py   # Core logic to call Watson NLP API
├── static/
│   └── mywebscript.js         # JS for frontend interaction
├── templates/
│   └── index.html             # HTML interface
├── .gitignore
├── .gitattributes
├── LICENSE
└── README.md
```

---

## 📦 Sample Emotion Detection Code

```python
import requests
import json

def emotion_detector(text_to_analyze):
    URL = 'https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict'
    header = {"grpc-metadata-mm-model-id": "emotion_aggregated-workflow_lang_en_stock"}
    input_json = { "raw_document": { "text": text_to_analyze } }
    response = requests.post(URL, json=input_json, headers=header)
    formated_response = json.loads(response.text)

    if response.status_code == 200:
        return formated_response
    elif response.status_code == 400:
        return {
            'anger': None,
            'disgust': None, 
            'fear': None, 
            'joy': None, 
            'sadness': None, 
            'dominant_emotion': None
        }

def emotion_predictor(detected_text):
    if all(value is None for value in detected_text.values()):
        return detected_text
    if detected_text['emotionPredictions'] is not None:
        emotions = detected_text['emotionPredictions'][0]['emotion']
        return {
            'anger': emotions['anger'],
            'disgust': emotions['disgust'],
            'fear': emotions['fear'],
            'joy': emotions['joy'],
            'sadness': emotions['sadness'],
            'dominant_emotion': max(emotions, key=emotions.get)
        }
```

---

## 🤝 Contributing

Pull requests and feedback are welcome! If you'd like to contribute improvements, feel free to fork and submit a PR.

---

## About Me

I'm Ongun Akay, a Senior Full-Stack Developer with expertise across various technologies.

- 👀 I specialize in full-stack development with extensive experience in frontend and backend technologies.
- 🌱 Currently, I'm sharpening my skills in advanced concepts of web development.
- 💞️ I’m always open to exciting collaborations and projects that challenge my abilities.
- 📫 You can reach me at [info@ongunakay.com](mailto:info@ongunakay.com).

---

## 📄 License

This project is licensed under the [Apache-2.0 license](./LICENSE) — see the LICENSE file for details.
