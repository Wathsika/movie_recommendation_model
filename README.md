# Hybrid Movie Recommendation System

## 1. Project Overview
The goal of this project was to build a machine learning pipeline that recommends movies to users by combining two primary recommendation strategies: Content-Based Filtering and Collaborative Filtering. By merging these approaches, we created a Hybrid Recommendation System that delivers more accurate and diverse suggestions than any single model alone.

## 2. Dataset
Source: MovieLens 100K Dataset (Small)

Files used:
- movies.csv → Movie IDs, Titles, and Genres
- ratings.csv → User IDs, Movie IDs, and Ratings (0.5 to 5.0)

## 3. Machine Learning Concepts Used

- Feature Extraction (TF-IDF): Converts text-based genres into numerical vectors.
- Cosine Similarity: Measures similarity between movie vectors in multi-dimensional space.
- K-Nearest Neighbors (KNN): Finds movies with similar user rating patterns.
- Sparse Matrices: Optimizes memory usage for large datasets with many zero values.
- Rank Fusion: Combines outputs from multiple models into a final ranked list.
- Root Mean Square Error (RMSE): Evaluates prediction accuracy of the model.

## 4. Development Pipeline

### Phase 1: Content-Based Filtering
- Recommends movies based on genre similarity
- Tool: TfidfVectorizer
- Logic: Assigns higher weight to unique genres and lower weight to common ones

### Phase 2: Collaborative Filtering
- Recommends movies based on user behavior
- Tool: NearestNeighbors (KNN)
- Logic: Builds a user-item matrix where rows = movies and columns = users, then finds similar rating patterns

### Phase 3: Hybridization
The final system combines both models:

When a user selects a movie:
- 20 similar movies are found using genre similarity
- 20 similar movies are found using user rating similarity
- Lists are merged and duplicates removed
- Results are ranked using average community rating

## 5. Problems Faced & Solutions

### Problem 1: Cold Start Problem
Issue: Collaborative filtering fails for new movies with no ratings  
Fix: Content-based filtering is used as a fallback  

### Problem 2: Strict Input Matching
Issue: Users had to enter exact movie titles  
Fix: Implemented partial string matching using str.contains()

### Problem 3: Memory Explosion (774 MB File)
Issue: Precomputing full similarity matrix created ~94M cells  
Fix: Switched to On-the-Fly computation, reducing size to ~50 MB

## 6. Python Libraries Used
- Pandas → Data manipulation
- NumPy → Numerical computations
- Scikit-Learn → TF-IDF, Cosine Similarity, KNN
- SciPy → Sparse matrix optimization
- Scikit-Surprise → Model evaluation
- Pickle → Model serialization

## 7. Model Evaluation
- Method: 5-Fold Cross Validation
- Metric: RMSE (Root Mean Square Error)
- Result: ~0.90 – 1.02

Interpretation:
The model’s predicted ratings are typically within ~1 star of actual user ratings, which is a strong result for the MovieLens 100K dataset.

## 8. Final Conclusion
This project successfully evolved from a basic genre-matching system into a production-ready hybrid recommendation engine. By combining collaborative and content-based filtering and solving memory and scalability issues, the system is now suitable for deployment as a lightweight web application.
