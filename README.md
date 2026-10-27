# Final Project

## Emotion Detection Application

This repository contains the Final Project for the IBM / Coursera course on building AI-enabled applications with Watson NLP and Flask.

### Overview

The Emotion Detection application analyzes textual input and predicts the underlying emotions expressed in the text. Using IBM Watson NLP's EmotionPredict service, it evaluates five core emotions:
- **Anger**
- **Disgust**
- **Fear**
- **Joy**
- **Sadness**

The application determines the dominant emotion based on the highest confidence score among the five emotions and presents the results through a web interface built with Flask.

### Features
- Watson NLP Emotion Detection integration.
- Custom package structure (`EmotionDetection`).
- Unit testing with Python `unittest`.
- Flask web application deployment with error handling for blank/invalid inputs.
- Static code analysis compliant with PEP 8 and Pylint.
