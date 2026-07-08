Final project

# Emotion Detection Web Application

A Flask-based web application that analyzes the emotional tone of a given piece of text using the IBM Watson NLP library. The app detects five core emotions — **anger**, **disgust**, **fear**, **joy**, and **sadness** — and identifies the dominant emotion in the text.

## Overview

This project was built as part of the IBM AI Engineering / Developer Skills Network capstone. It demonstrates how to:

- Call an embedded Watson NLP `EmotionPredict` service via a REST API
- Parse and format the API response into a clean, usable output
- Package Python code into a reusable module
- Write and run unit tests
- Deploy a Python function as a web application using Flask
- Handle errors gracefully for invalid/blank input
- Pass static code analysis (PyLint) with a perfect score

## Features

- 🔍 Analyzes text and returns scores for anger, disgust, fear, joy, and sadness
- 🏆 Identifies the dominant (highest-scoring) emotion
- 🌐 Simple web interface for entering text and viewing results
- ⚠️ Graceful error handling for blank/invalid input
- ✅ Fully unit tested
- 🧹 PyLint-compliant codebase (10/10)

## Project Structure

```
final_project/
├── README.md
├── server.py                          # Flask application entry point
├── test_emotion_detection.py          # Unit tests
├── EmotionDetection/                  # Application package
│   ├── __init__.py
│   └── emotion_detection.py           # Core emotion detection logic
├── templates/
│   └── index.html                     # Web UI (provided)
└── static/
    └── mywebscript.js                 # Front-end JS (provided)
```

## Requirements

- Python 3.x
- Flask
- requests

Install dependencies:

```bash
python3 -m pip install flask requests
```

## How It Works

1. The user submits text through the web interface (or a query parameter).
2. `server.py` receives the request at the `/emotionDetector` endpoint and passes the text to the `emotion_detector` function.
3. `emotion_detector` (in `EmotionDetection/emotion_detection.py`) sends the text to the Watson NLP `EmotionPredict` API:

   ```
   POST https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict
   ```

4. The JSON response is parsed to extract emotion scores, and the dominant emotion is calculated.
5. If the input text is blank, the Watson API returns a `400` status code, and the function returns a dictionary of `None` values instead of scores.
6. The formatted result (or an error message) is returned to the user.

## API Endpoint

### `GET /emotionDetector`

**Query parameter:**

| Parameter      | Type   | Description                  |
|----------------|--------|-------------------------------|
| `textToAnalyze` | string | The text to analyze for emotion |

**Example request:**

```
GET /emotionDetector?textToAnalyze=I love this new technology.
```

**Example response:**

```
For the given statement, the system response is 'anger': 0.006274985, 'disgust': 0.0025598293, 'fear': 0.009251528, 'joy': 0.9680386 and 'sadness': 0.049744144. The dominant emotion is joy.
```

**Blank input response:**

```
Invalid text! Please try again!
```

## Running the Application

1. Clone this repository and navigate into the project folder:

   ```bash
   git clone https://github.com/<your-username>/oaqjp-final-project-emb-ai.git final_project
   cd final_project
   ```

2. Install dependencies:

   ```bash
   python3 -m pip install flask requests
   ```

3. Start the Flask server:

   ```bash
   python3 server.py
   ```

4. Open your browser to:

   ```
   http://localhost:5000
   ```

5. Enter a statement in the text box and click the button to see the detected emotions and dominant emotion.

## Running Unit Tests

The project includes unit tests covering all five core emotions:

```bash
python3 test_emotion_detection.py
```

Expected output:

```
.
----------------------------------------------------------------------
Ran 1 test in 1.234s

OK
```

## Static Code Analysis

`server.py` is fully PyLint-compliant:

```bash
pylint server.py
```

Expected output:

```
Your code has been rated at 10.00/10
```

## Example Usage

| Input                                     | Dominant Emotion |
|--------------------------------------------|-------------------|
| I am glad this happened                     | joy               |
| I am really mad about this                  | anger             |
| I feel disgusted just hearing about this    | disgust           |
| I am so sad about this                      | sadness           |
| I am really afraid that this will happen    | fear              |

## Acknowledgements

This project uses the **IBM Watson NLP Library** (`EmotionPredict` function) as part of the IBM Developer Skills Network coursework, built on the [oaqjp-final-project-emb-ai](https://github.com/ibm-developer-skills-network/oaqjp-final-project-emb-ai) starter repository.

## License

This project is for educational purposes as part of an IBM Developer Skills Network course.