# 📘 Sentiment Analyzer (Streamlit + MongoDB + Logistic Regression)

A comprehensive web application for analyzing customer review sentiment (Positive / Neutral / Negative) using:

* **Streamlit** (Web UI)
* **MongoDB** (Database)
* **Logistic Regression** (Machine Learning Model)
* **TF-IDF Vectorizer**

---

## 🚀 Features

* **Single Review Prediction**: Enter a review and the ML model predicts its sentiment with a confidence score.
* **Batch CSV Upload**: Upload a CSV file with a `Text` column to analyze multiple reviews at once.
* **MongoDB Storage**: All reviews (original text, cleaned text, predicted sentiment) are saved in MongoDB.
* **Analytics Dashboard**: Visualize sentiment distribution with bar and pie charts and view recent reviews.

---

## 🏗 Project Structure

```
project/
├── app.py                 # Main Streamlit application
├── model.pkl              # Trained Logistic Regression model
├── vectorizer.pkl         # TF-IDF vectorizer
├── utils.py               # Helper functions (text cleaning, MongoDB connection)
├── requirements.txt       # Python dependencies
└── README.md              # Project documentation
```

---

## 🛠 Installation

### 1️⃣ Install dependencies

```bash
pip install -r requirements.txt
```

### 2️⃣ Run the application

```bash
streamlit run app.py
```

---

## 🗄 MongoDB Setup

Update your MongoDB connection details in the code or via a `.env` file:

```python
MONGO_URL = "mongodb+srv://username:password@cluster-url.mongodb.net/"
DB_NAME = "sentiment_db"
COLLECTION_NAME = "reviews"
```

---

## 🤖 How the Model Works (Logistic Regression)

1. **Text Cleaning**:

   * Convert text to lowercase
   * Remove punctuation and special characters
   * Remove stopwords

2. **Text Vectorization using TF-IDF**:

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer()
X_vec = vectorizer.fit_transform(cleaned_texts)
```

3. **Train Logistic Regression Model**:

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)
```

4. **Predict Sentiment**:

```python
X_new = vectorizer.transform([new_review])
prediction = model.predict(X_new)[0]           # Predicted sentiment
confidence = model.predict_proba(X_new).max()  # Confidence score
```

5. **Save results to MongoDB** and display in Streamlit.

---

## 📤 Batch CSV Upload

* The CSV must contain a column named `Text`.
* The app will clean text, predict sentiment for each row, and save results to MongoDB.
* Displays processed data in a table after uploading.

Example CSV:

```csv
Text
This product is amazing!
I didn't like the service.
It was okay.
```

---

## 📈 Analytics Page

The Analytics section provides:

* Total number of reviews analyzed
* Most common sentiment
* Sentiment distribution (Bar and Pie charts)
* Recent 10 reviews from MongoDB

---

## 🧹 Cache Refresh

After saving data, Streamlit cache is cleared:

```python
st.cache_data.clear()
```

This ensures analytics always reflect the latest data.

---

## 🧑‍💻 Built With

* Python 3.10+
* Streamlit
* MongoDB Atlas
* scikit-learn (Logistic Regression)
* pandas
* plotly

---

## 📧 Support & Contributions

Feel free to contribute or suggest improvements:

* Enhance ML model performance
* Improve UI/UX
* Deployment on Streamlit Cloud, Docker, or Render

For issues, feedback, or collaboration, please contact the d
