# Topic-Modeling-LDA-based-Customer-Review-Analysis

InsightExtractor is a sophisticated topic modeling solution designed to unveil the underlying themes from vast collections of customer reviews. Utilizing the Latent Dirichlet Allocation (LDA) technique, this project parses through unstructured text data to extract and visualize prominent topics, providing businesses with actionable insights into customer sentiment and feedback.

Latent Dirichlet Allocation (LDA) is a generative statistical model that explains sets of observations, typically text corpora, through unobserved groups that explain why some parts of the data are similar. Here's a table that outlines why LDA is an important algorithm in the field of natural language processing and topic modeling:

| Aspect                               | Explanation                                                                                                                                                                                                                              |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Discovering Hidden Themes**        | LDA helps in discovering hidden thematic structure in large archives of documents. It can identify topics that are not explicitly labeled in the text, revealing insights that could be missed with a simple manual review.              |
| **Dimensionality Reduction**         | It reduces the dimensionality of text data by transforming the original text features (words) into a smaller number of topics, making it easier to perform other tasks such as classification or clustering on the text data.        |
| **Feature Engineering**              | Topics produced by LDA can be used as features for machine learning models. These features often improve the performance of models in tasks such as sentiment analysis, recommendation systems, and more.                             |
| **Grouping and Segmentation**        | LDA can group documents into topics, which is helpful for organizing, searching, and understanding large collections of text data. It can also be used for customer segmentation based on textual feedback or reviews.                  |
| **Trend Analysis**                   | By analyzing topics over time, LDA can help identify trends and changes in discourse, which is valuable for market research, tracking policy changes, or monitoring public interest in different subjects.                          |
| **Content Recommendation**           | LDA can improve content recommendation systems by matching users' interests with topic distributions, enhancing the relevance of recommendations in systems like news feeds or product suggestions.                                   |
| **Enhancing Information Retrieval**  | LDA can enhance information retrieval systems by allowing searches to be performed based on topics, which can provide more relevant results compared to keyword searches, especially when the exact keywords may not be known.       |

## Project Overview:    
**Objective:** Discover the main topics from a collection of customer reviews.            
**Method:** Latent Dirichlet Allocation (LDA) for topic modeling.                
**Tools:** Python, pandas, nltk, gensim, and pyLDAvis for visualization.               
**Dataset:** An Excel file containing fabricated customer reviews.


## Features
- Text preprocessing including tokenization, stopword removal, and lemmatization.
- Generation of a document-term matrix required for LDA analysis.
- Implementation of LDA for topic discovery and distribution analysis.
- Interactive visualization of topics using pyLDAvis for easy interpretation.
- Coherence score evaluation to assess the quality of the topic modeling.
 
## Data Collection:
Using Reddit's API for predicting Posts

In this project I have collected data uding Reddit's API. The goal for this project is to using NLP and Machine Leaning models, build a binary predictor to determine which subreddit a given post is coming from.

## Step 1: Load the Data
First, load the data from the Excel file into a pandas DataFrame. 

## Step 2: Preprocess the Data
Define and apply a preprocessing function to clean the text data. This includes converting to lowercase, removing punctuation and stopwords, and lemmatizing the words.

## Step 3: Create Dictionary and Corpus for LDA
Prepare the data for LDA analysis by creating a dictionary and corpus using gensim.

## Step 4: LDA Model Training
Train the LDA model using the corpus and dictionary prepared in the previous step.

## Step 5: Visualizing the Topics
Use pyLDAvis to visualize the topics for better understanding and interpretation.

![image](https://github.com/TaranehAskarzadeh/Topic-Modeling-LDA-based-Customer-Review-Analysis/assets/65934906/9d68c565-4a88-4025-908c-944b5943fe61)


