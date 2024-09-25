
# product-review-analyzer
# Install the required libraries
# pip install textblob
# pip install nltk

from textblob import TextBlob
import nltk
from nltk.corpus import stopwords
import re

# Download stopwords
nltk.download('stopwords')
stop_words = set(stopwords.words('english'))

# Sample product reviews
reviews = [
    "This product is amazing! I love how it works, and it made my life easier.",
    "Terrible quality, broke after two days. Very disappointed!",
    "Good value for the price, but the design could be better.",
    "Absolutely fantastic! Will buy again for sure!",
    "It's okay, not great but not bad either."
]

# Function to preprocess the review text
def preprocess_text(review):
    # Remove non-alphabet characters and lowercase
    review = re.sub(r'[^a-zA-Z\s]', '', review.lower())
    # Tokenize and remove stopwords
    tokens = review.split()
    tokens = [word for word in tokens if word not in stop_words]
    return ' '.join(tokens)

# Function to analyze sentiment
def analyze_sentiment(review):
    blob = TextBlob(review)
    return blob.sentiment.polarity  # Returns a polarity score from -1 to 1

# Process and analyze each review
for review in reviews:
    cleaned_review = preprocess_text(review)
    sentiment_score = analyze_sentiment(cleaned_review)
    if sentiment_score > 0:
        sentiment = "Positive"
    elif sentiment_score < 0:
        sentiment = "Negative"
    else:
        sentiment = "Neutral"
    
    print(f"Review: {review}")
    print(f"Cleaned Review: {cleaned_review}")
    print(f"Sentiment: {sentiment}, Score: {sentiment_score}\n")

