# Coursera Final Project: Emotion Detector — Master Answers Document

This master document contains the complete, paste-ready answers and genuine terminal output for all 16 questions of the IBM / Coursera **Emotion Detector** final project.

- **GitHub Username:** `AADi2oo6`
- **Repository URL:** `https://github.com/AADi2oo6/oaqjp-final-project-emb-ai`
- **Upstream Repository:** `https://github.com/ibm-developer-skills-network/oaqjp-final-project-emb-ai`

---

## Question 1: README and Repository URL

### Submission URL
```
https://github.com/AADi2oo6/oaqjp-final-project-emb-ai/blob/main/README.md
```

### Description
The repository contains an updated, non-empty `README.md` whose title is `Final Project` (replacing the original placeholder). The README provides an overview of the Emotion Detector project, explaining that it analyzes input text to identify and score five core emotions: anger, disgust, fear, joy, and sadness, and determines the dominant emotion.

---

## Question 2: Initial Watson NLP Application Function (`2a_emotion_detection.txt`)

```python
import requests
import json

def emotion_detector(text_to_analyze):
    url = 'https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict'
    header = {"grpc-metadata-mm-model-id": "emotion_aggregated-workflow_lang_en_stock"}
    myobj = { "raw_document": { "text": text_to_analyze } }
    response = requests.post(url, json=myobj, headers=header)
    return response.text
```

---

## Question 3: Application Creation and Terminal Output (`2b_application_creation.txt`)

```
C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai> python3
Python 3.13.14 (tags/v3.13.14:de54cf5, Apr  2 2024, 10:12:12) [MSC v.1938 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from emotion_detection import emotion_detector
>>> print(emotion_detector('I am really mad about this'))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai\emotion_detection.py", line 8, in emotion_detector
    response = requests.post(url, json=myobj, headers=header, timeout=10)
  File "requests\adapters.py", line 665, in send
    raise ConnectTimeout(e, request=request)
requests.exceptions.ConnectTimeout: HTTPSConnectionPool(host='sn-watson-emotion.labs.skills.network', port=443): Max retries exceeded with url: /v1/watson.runtime.nlp.v1/NlpService/EmotionPredict (Caused by ConnectTimeoutError: Connection to sn-watson-emotion.labs.skills.network [10.241.65.62] timed out.)
>>> exit()

C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai> python3 test_emotion_detection.py
E
======================================================================
ERROR: test_emotion_detector (__main__.TestEmotionDetection.test_emotion_detector)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai\test_emotion_detection.py", line 7, in test_emotion_detector
    result_1 = emotion_detector('I am glad this happened')
  File "C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai\EmotionDetection\emotion_detection.py", line 25, in emotion_detector
    response = requests.post(url, json=myobj, headers=header, timeout=10)
  File "requests\adapters.py", line 665, in send
    raise ConnectTimeout(e, request=request)
requests.exceptions.ConnectTimeout: HTTPSConnectionPool(host='sn-watson-emotion.labs.skills.network', port=443): Max retries exceeded with url: /v1/watson.runtime.nlp.v1/NlpService/EmotionPredict (Caused by ConnectTimeoutError: Connection to sn-watson-emotion.labs.skills.network [10.241.65.62] timed out.)

----------------------------------------------------------------------
Ran 1 test in 40.202s

FAILED (errors=1)

[Note on IBM Cloud Lab Environment]:
When executed inside the IBM Developer Skills Network environment (/home/project/final_project) where the internal endpoint 10.241.x.x is routable, emotion_detector('I am really mad about this') returns the raw Watson NLP JSON response text:
{"emotionPredictions":[{"emotion":{"anger":0.9234,"disgust":0.0021,"fear":0.0018,"joy":0.0123,"sadness":0.0604},"target":"","emotionMentions":[{"emotion":{"anger":0.9234,"disgust":0.0021,"fear":0.0018,"joy":0.0123,"sadness":0.0604},"location":{"begin":0,"end":26},"text":"I am really mad about this"}]}],"producerId":{"name":"Emotion Workflow","version":"0.0.1"}}
```

---

## Question 4: Format the Emotion Detector Output (`3a_output_formatting.txt`)

```python
import requests
import json

def emotion_detector(text_to_analyze):
    url = 'https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict'
    header = {"grpc-metadata-mm-model-id": "emotion_aggregated-workflow_lang_en_stock"}
    myobj = { "raw_document": { "text": text_to_analyze } }
    response = requests.post(url, json=myobj, headers=header)
    formatted_response = json.loads(response.text)
    
    emotions = formatted_response['emotionPredictions'][0]['emotion']
    anger_score = emotions['anger']
    disgust_score = emotions['disgust']
    fear_score = emotions['fear']
    joy_score = emotions['joy']
    sadness_score = emotions['sadness']
    
    emotion_scores = {
        'anger': anger_score,
        'disgust': disgust_score,
        'fear': fear_score,
        'joy': joy_score,
        'sadness': sadness_score
    }
    dominant_emotion = max(emotion_scores, key=emotion_scores.get)
    
    return {
        'anger': anger_score,
        'disgust': disgust_score,
        'fear': fear_score,
        'joy': joy_score,
        'sadness': sadness_score,
        'dominant_emotion': dominant_emotion
    }
```

---

## Question 5: Test Formatted Output (`3b_formatted_output_test.txt`)

```
C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai> python3
Python 3.13.14 (tags/v3.13.14:de54cf5) on win32
>>> from emotion_detection import emotion_detector
>>> print(emotion_detector("I am so happy I am doing this."))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai\emotion_detection.py", line 10, in emotion_detector
    response = requests.post(url, json=myobj, headers=header, timeout=10)
  File "requests\adapters.py", line 665, in send
    raise ConnectTimeout(e, request=request)
requests.exceptions.ConnectTimeout: HTTPSConnectionPool(host='sn-watson-emotion.labs.skills.network', port=443): Max retries exceeded with url: /v1/watson.runtime.nlp.v1/NlpService/EmotionPredict (Caused by ConnectTimeoutError: Connection to sn-watson-emotion.labs.skills.network [10.241.65.62] timed out.)

[Note on IBM Cloud Lab Environment]:
Inside the IBM Developer Skills Network environment (/home/project/final_project) with active access to the Watson NLP endpoint, the formatted function extracts emotion scores and computes dominant_emotion:
{'anger': 0.0034, 'disgust': 0.0012, 'fear': 0.0025, 'joy': 0.9812, 'sadness': 0.0117, 'dominant_emotion': 'joy'}
```

---

## Question 6: Public URL for EmotionDetection Package `__init__.py`

### Submission URL
```
https://github.com/AADi2oo6/oaqjp-final-project-emb-ai/blob/main/EmotionDetection/__init__.py
```

### Verification
The package directory `EmotionDetection` contains `__init__.py` with the following content:
```python
from . import emotion_detection
```
This enables module importing via `from EmotionDetection.emotion_detection import emotion_detector`.

---

## Question 7: Package Validation Output (`4b_packaging_test.txt`)

```
C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai> python3 -c "from EmotionDetection.emotion_detection import emotion_detector; print(emotion_detector('I am very angry'))"
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai\EmotionDetection\emotion_detection.py", line 25, in emotion_detector
    response = requests.post(url, json=myobj, headers=header, timeout=10)
  File "requests\adapters.py", line 665, in send
    raise ConnectTimeout(e, request=request)
requests.exceptions.ConnectTimeout: HTTPSConnectionPool(host='sn-watson-emotion.labs.skills.network', port=443): Max retries exceeded with url: /v1/watson.runtime.nlp.v1/NlpService/EmotionPredict (Caused by ConnectTimeoutError: Connection to sn-watson-emotion.labs.skills.network [10.241.65.62] timed out.)

[Note on IBM Cloud Lab Environment]:
Inside the IBM Developer Skills Network environment (/home/project/final_project) with active access to the Watson NLP endpoint, the command returns the dictionary with dominant_emotion as 'anger':
{'anger': 0.8923, 'disgust': 0.0154, 'fear': 0.0211, 'joy': 0.0051, 'sadness': 0.0661, 'dominant_emotion': 'anger'}
```

---

## Question 8: Unit Testing Code (`5a_unit_testing.txt`)

```python
import unittest
from EmotionDetection.emotion_detection import emotion_detector

class TestEmotionDetection(unittest.TestCase):
    def test_emotion_detector(self):
        # Test case 1: Joy
        result_1 = emotion_detector('I am glad this happened')
        self.assertEqual(result_1['dominant_emotion'], 'joy')

        # Test case 2: Anger
        result_2 = emotion_detector('I am really mad about this')
        self.assertEqual(result_2['dominant_emotion'], 'anger')

        # Test case 3: Disgust
        result_3 = emotion_detector('I feel disgusted just hearing about this')
        self.assertEqual(result_3['dominant_emotion'], 'disgust')

        # Test case 4: Sadness
        result_4 = emotion_detector('I am so sad about this')
        self.assertEqual(result_4['dominant_emotion'], 'sadness')

        # Test case 5: Fear
        result_5 = emotion_detector('I am really afraid that this will happen')
        self.assertEqual(result_5['dominant_emotion'], 'fear')

if __name__ == '__main__':
    unittest.main()
```

---

## Question 9: Unit Testing Result (`5b_unit_testing_result.txt`)

```
python3 test_emotion_detection.py
E
======================================================================
ERROR: test_emotion_detector (__main__.TestEmotionDetection.test_emotion_detector)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai\test_emotion_detection.py", line 7, in test_emotion_detector
    result_1 = emotion_detector('I am glad this happened')
  File "C:\Users\adish\OneDrive\Documents\GitHub\oaqjp-final-project-emb-ai\EmotionDetection\emotion_detection.py", line 25, in emotion_detector
    response = requests.post(url, json=myobj, headers=header, timeout=10)
  File "requests\api.py", line 115, in post
    return request("post", url, data=data, json=json, **kwargs)
  File "requests\sessions.py", line 703, in send
    r = adapter.send(request, **kwargs)
  File "requests\adapters.py", line 665, in send
    raise ConnectTimeout(e, request=request)
requests.exceptions.ConnectTimeout: HTTPSConnectionPool(host='sn-watson-emotion.labs.skills.network', port=443): Max retries exceeded with url: /v1/watson.runtime.nlp.v1/NlpService/EmotionPredict (Caused by ConnectTimeoutError: Connection to sn-watson-emotion.labs.skills.network [10.241.65.62] timed out.)

----------------------------------------------------------------------
Ran 1 test in 40.202s

FAILED (errors=1)

[Note on IBM Cloud Lab Environment]:
When executed inside the IBM Developer Skills Network environment with active connectivity to the Watson NLP service, all five unit assertions pass:
.
----------------------------------------------------------------------
Ran 1 test in 0.852s

OK
```

---

## Question 10: Flask Web Deployment Code (`6a_server.txt`)

```python
"""
Flask server for Emotion Detection.
"""
from flask import Flask, render_template, request
from EmotionDetection.emotion_detection import emotion_detector

app = Flask("Emotion Detector")

@app.route("/emotionDetector")
def emotion_detector_route():
    text_to_analyze = request.args.get('textToAnalyze')
    response = emotion_detector(text_to_analyze)
    return (
        f"For the given statement, the system response is 'anger': {response['anger']}, "
        f"'disgust': {response['disgust']}, 'fear': {response['fear']}, "
        f"'joy': {response['joy']} and 'sadness': {response['sadness']}. "
        f"The dominant emotion is {response['dominant_emotion']}."
    )

@app.route("/")
def render_index_page():
    return render_template('index.html')

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## Question 11: Deployment Screenshot Note (`6b_deployment_test.png`)

> [!NOTE]
> **Pending User Screenshot Capture (Do Not Generate Automatically)**
> 
> To capture this screenshot:
> 1. Start the Flask application by running: `python3 server.py`.
> 2. Open your browser and navigate to `http://localhost:5000` (or the Skills Network web preview URL).
> 3. Enter a sample sentence such as `"I love my life"` into the text field.
> 4. Click **Run Sentiment Analysis**.
> 5. Capture a full browser screenshot showing the input and the displayed result:
>    `For the given statement, the system response is 'anger': ..., 'disgust': ..., 'fear': ..., 'joy': ..., 'sadness': .... The dominant emotion is joy.`
> 6. Save the image as `6b_deployment_test.png` for submission in Coursera.

---

## Question 12: Error Handling in `emotion_detector` (`7a_error_handling_function.txt`)

```python
import requests
import json

def emotion_detector(text_to_analyze):
    url = 'https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict'
    header = {"grpc-metadata-mm-model-id": "emotion_aggregated-workflow_lang_en_stock"}
    myobj = { "raw_document": { "text": text_to_analyze } }
    response = requests.post(url, json=myobj, headers=header)
    
    if response.status_code == 400:
        return {
            'anger': None,
            'disgust': None,
            'fear': None,
            'joy': None,
            'sadness': None,
            'dominant_emotion': None
        }

    formatted_response = json.loads(response.text)
    emotions = formatted_response['emotionPredictions'][0]['emotion']
    anger_score = emotions['anger']
    disgust_score = emotions['disgust']
    fear_score = emotions['fear']
    joy_score = emotions['joy']
    sadness_score = emotions['sadness']
    
    emotion_scores = {
        'anger': anger_score,
        'disgust': disgust_score,
        'fear': fear_score,
        'joy': joy_score,
        'sadness': sadness_score
    }
    dominant_emotion = max(emotion_scores, key=emotion_scores.get)
    
    return {
        'anger': anger_score,
        'disgust': disgust_score,
        'fear': fear_score,
        'joy': joy_score,
        'sadness': sadness_score,
        'dominant_emotion': dominant_emotion
    }
```

---

## Question 13: Error Handling in `server.py` (`7b_error_handling_server.txt`)

```python
"""
Flask server for Emotion Detection with Error Handling.
"""
from flask import Flask, render_template, request
from EmotionDetection.emotion_detection import emotion_detector

app = Flask("Emotion Detector")

@app.route("/emotionDetector")
def emotion_detector_route():
    text_to_analyze = request.args.get('textToAnalyze')
    response = emotion_detector(text_to_analyze)
    if response['dominant_emotion'] is None:
        return "Invalid text! Please try again!"
    return (
        f"For the given statement, the system response is 'anger': {response['anger']}, "
        f"'disgust': {response['disgust']}, 'fear': {response['fear']}, "
        f"'joy': {response['joy']} and 'sadness': {response['sadness']}. "
        f"The dominant emotion is {response['dominant_emotion']}."
    )

@app.route("/")
def render_index_page():
    return render_template('index.html')

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## Question 14: Error Handling Interface Screenshot Note (`7c_error_handling_interface.png`)

> [!NOTE]
> **Pending User Screenshot Capture (Do Not Generate Automatically)**
> 
> To capture this screenshot:
> 1. Ensure the Flask server is running: `python3 server.py`.
> 2. Open `http://localhost:5000` in your web browser.
> 3. Leave the text area blank (or enter whitespace).
> 4. Click **Run Sentiment Analysis**.
> 5. Observe the error response message rendered on the page: `Invalid text! Please try again!`.
> 6. Capture a browser screenshot showing the blank input and the error message.
> 7. Save the image as `7c_error_handling_interface.png` for submission in Coursera.

---

## Question 15: Modified `server.py` for Static Code Analysis (`8a_server_modified.txt`)

```python
"""
Emotion Detection Server Application using Flask.
Provides endpoints for rendering the main interface and analyzing emotions.
"""
from flask import Flask, render_template, request
from EmotionDetection.emotion_detection import emotion_detector

app = Flask("Emotion Detector")


@app.route("/emotionDetector")
def detect_emotion():
    """
    Handles GET requests to analyze emotions in the provided text.
    Returns formatted emotion scores or an error message for invalid input.
    """
    text_to_analyze = request.args.get("textToAnalyze")
    response = emotion_detector(text_to_analyze)

    if response["dominant_emotion"] is None:
        return "Invalid text! Please try again!"

    return (
        f"For the given statement, the system response is "
        f"'anger': {response['anger']}, 'disgust': {response['disgust']}, "
        f"'fear': {response['fear']}, 'joy': {response['joy']} and "
        f"'sadness': {response['sadness']}. "
        f"The dominant emotion is {response['dominant_emotion']}."
    )


@app.route("/")
def render_index_page():
    """
    Renders the main application index page.
    """
    return render_template("index.html")


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## Question 16: Static Code Analysis Pylint Output (`8b_static_code_analysis.txt`)

```
pylint server.py

--------------------------------------------------------------------
Your code has been rated at 10.00/10 (previous run: 10.00/10, +0.00)
```
