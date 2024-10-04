# Quora Duplicate Question Detection

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-0.24%2B-orange?style=for-the-badge&logo=scikit-learn)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-1.4%2B-red?style=for-the-badge&logo=xgboost)](https://xgboost.readthedocs.io/)
[![Streamlit](https://img.shields.io/badge/Streamlit-0.80%2B-FF4B4B?style=for-the-badge&logo=streamlit)](https://streamlit.io/)

<div align="center">
  <img src="https://images.squarespace-cdn.com/content/v1/639b5b5db16dac1afbf2ca5c/627bdaaf-d0c6-4718-9b34-f0db82c1939b/Logo_Screen_Red_RGB_1024.png" width="200"/>
</div>

This project implements an **NLP-based solution** to detect duplicate questions on Quora, a key issue that reduces platform efficiency and user satisfaction. By identifying duplicate questions, we can prevent redundant answers and enhance the user experience.

## Table of Contents
- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Features Extracted](#features-extracted)
- [Methodology](#methodology)
- [Models & Performance](#models--performance)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Web Application](#web-application)
- [Authors & Acknowledgments](#authors--acknowledgments)
- [License](#license)

## Project Overview

This project aims to efficiently detect duplicate questions on Quora using Natural Language Processing (NLP) and machine learning techniques. By building predictive models, we aim to identify pairs of questions that essentially seek the same information despite differences in phrasing.

## Problem Statement

Duplicate questions cause inefficiencies in platforms like Quora, where many similar questions get asked repeatedly. Instead of manually filtering these, our solution automates the process of recognizing when two questions are duplicates, improving user experience by:
1. Preventing redundant answers.
2. Guiding users to existing responses that satisfy their query.

For example:
- **Q1:** "What is the capital of France?"
- **Q2:** "Which city is the capital of France?"

Though phrased differently, these questions ask the same thing and should be treated as duplicates.

## Features Extracted

To solve this, we extracted a variety of features from the question pairs:

1. **Basic Features**:
   - Length of each question.
   - Number of words in each question.
   - Common words between the questions.
   - Word share ratio: Common words divided by total words.

2. **Advanced Features**:
   - `cwc_min`, `cwc_max`: Ratios of common words relative to the lengths of the smaller/larger question.
   - `ctc_min`, `ctc_max`: Ratios of common tokens between questions.
   - First and last word equality: Whether the first or last word in both questions matches.
   - Fuzzy matching features: Using the `fuzzywuzzy` library, we extracted ratios like `fuzz_ratio`, `token_sort_ratio`, and more.

3. **Bag-of-Words (BoW)**:
   - Vectorized representation of the questions, providing a numerical feature set for model training.

## Methodology

Our approach involved several steps:

1. **Data Preprocessing**:
   - Cleaning and normalizing text.
   - Removing special characters, HTML tags, and contractions.
   - Generating token and length-based features.

2. **Modeling**:
   - **Random Forest Classifier**: A robust, ensemble learning method.
   - **XGBoost Classifier**: A powerful gradient boosting model.
   - Both models were trained on preprocessed features to classify whether a pair of questions is a duplicate or not.

3. **Evaluation**:
   - We split the data into training and testing sets and evaluated the models using accuracy, precision, recall, and confusion matrices.

## Models & Performance

- **Random Forest Classifier**:
  - Achieved an accuracy of **79.05%**.
  - Confusion matrix results showed a good balance between precision and recall.

- **XGBoost Classifier**:
  - Achieved a slightly better accuracy of **79.46%**.
  - Its confusion matrix highlighted improved classification of non-duplicate pairs.

## Installation

To get started with this project locally, follow these steps:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Hemanth1818/Identifying-Similar-Questions-on-Quora.git
   cd Identifying-Similar-Questions-on-Quora
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the Streamlit Web Application**:
   ```bash
   streamlit run app.py
   ```

## Usage

The project provides a pre-built web interface powered by **Streamlit**. Once installed, simply run the web application where users can input two questions, and the system will classify them as either duplicates or not.

For instance:
- **Input**: 
  - Question 1: "Where is the capital of India?"
  - Question 2: "What is the capital city of India?"
- **Output**: "These questions are duplicates."

The web app also provides a detailed explanation of the features used in the prediction.

## Results

The models performed well on a dataset of 30,000 Quora question pairs. Here's a summary of the performance:

- **Random Forest**: 79.05% accuracy
- **XGBoost**: 79.46% accuracy

We saved the trained models and text vectorizers as `.pkl` files for easy deployment.

## Web Application

A Streamlit-based interactive web application allows users to input question pairs and receive instant predictions on whether they are duplicates. The application is easy to use and integrates seamlessly with the trained machine learning models.

## Authors & Acknowledgments

This project was developed by:

- **Hemanth Kakkireni** – Algorithm & Model Research
- **Sai Shreekar Reddi Maligireddi** – Exploratory Data Analysis
- **Shashank Mutyala** – Algorithm Development & Coding
- **Srinivas Nalla** – Integration & Testing
- **Sai Varun Padmanabham** – Data Collection & Preprocessing

Special thanks to our course **AI 3106: Foundations of NLP** for providing the framework for this project.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
