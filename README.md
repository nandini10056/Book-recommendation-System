# Book Recommendation System

A Book Recommendation System developed using the **Book-Crossing dataset** to explore and compare different recommendation techniques, including popularity-based filtering, collaborative filtering, content-based filtering, and a hybrid recommendation approach.

## Project Overview

The objective of this project is to develop a recommendation system that suggests books to users based on popularity, user preferences, book similarities, and book metadata.

The project explores multiple recommendation algorithms and compares their performance to understand their strengths and limitations.

## Dataset

This project uses the Book-Crossing dataset, which contains three main files:

| File | Description |
|---|---|
| `Books.csv` | Book information, including ISBN, title, author, publication year, and publisher |
| `Ratings.csv` | User ratings for different books |
| `Users.csv` | User information |

The dataset is organized into three CSV files inside the `dataset/` directory.

**Note:** The raw dataset is not included in this repository. 

## Project Structure

```text
Book-recommendation-System/
│
├── dataset/
│   ├── Books.csv
│   ├── Ratings.csv
│   └── Users.csv
│
├── notebooks/
│   ├── Book_Recommendation_Analysis.ipynb
│   └── results/
│       ├── final_hybrid_recommendations.csv
│       └── rating_model_comparison.csv
│
├── models/
│
├── .gitignore
└── README.md
```

## Recommendation Techniques Implemented

### 1. Popularity-Based Recommendation

Recommends books based on their overall popularity and rating information.

### 2. User-Based Collaborative Filtering

Identifies users with similar rating preferences and recommends books based on the preferences of similar users.

### 3. Item-Based Collaborative Filtering

Identifies similarities between books using user-rating patterns.

Two neighbourhood configurations were explored:

- Item-Based Collaborative Filtering (K = 20)
- Item-Based Collaborative Filtering (K = 50)

### 4. Content-Based Filtering

Uses book metadata to identify books with similar characteristics.

TF-IDF (Term Frequency-Inverse Document Frequency) and cosine similarity are used to calculate similarity between books based on their metadata.

### 5. Hybrid Recommendation System

Combines collaborative-filtering and content-based recommendation signals.

The implemented approach:

- Generates candidates using both content-based filtering and Item-Based Collaborative Filtering.
- Uses a combined score when both recommendation signals are available.
- Uses an available individual signal when only one is available.
- Applies a diversity constraint by reserving up to two positions for content-informed recommendations.
- Fills the remaining positions using Item-CF recommendations.
- Removes duplicate book titles for each user.

The final output contains 10 unique book recommendations for each of 32 users.

## Model Evaluation

The collaborative-filtering rating prediction models were evaluated using:

- **RMSE (Root Mean Squared Error):** Measures the average magnitude of prediction errors, with greater penalties for larger errors.
- **MAE (Mean Absolute Error):** Measures the average absolute difference between actual and predicted ratings.

Lower values indicate better rating prediction performance.

### Evaluation Results

| Model | RMSE | MAE |
|---|---:|---:|
| Item-Based Collaborative Filtering (K=50) | **1.468959** | **0.933052** |
| Item-Based Collaborative Filtering (K=20) | 1.538742 | 0.951834 |
| User-Based Collaborative Filtering | 1.808619 | 1.409231 |

**Observation:** Item-Based Collaborative Filtering with K=50 achieved the lowest RMSE and MAE among the three evaluated rating prediction models.

RMSE and MAE comparisons are reported only for the collaborative-filtering models for which rating predictions were evaluated. The Hybrid recommendation output has not yet undergone a sufficiently reliable independent evaluation using ranking metrics.

## Final Hybrid Recommendation Output

The final Hybrid recommendation file contains:

| Metric | Result |
|---|---:|
| Users | 32 |
| Total recommendations | 320 |
| Recommendations per user | 10 |
| Duplicate user-title pairs | 0 |

### Recommendation Signal Distribution

| Recommendation Signal | Count |
|---|---:|
| Item-CF only | 264 |
| Content only | 37 |
| Content + Item-CF | 19 |

The Hybrid output uses a diversity-constrained ranking strategy. These results describe the generated recommendations and signal distribution, not an improvement in predictive accuracy.

## Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Scikit-learn
- TF-IDF
- Cosine Similarity
- Collaborative Filtering
- Git and GitHub

## How to Run the Project

### Prerequisites

- Python installed
- Visual Studio Code
- Jupyter Notebook extension in VS Code

### Setup

Clone the repository:

```bash
git clone https://github.com/nandini10056/Book-recommendation-System.git
```

Navigate to the project directory:

```bash
cd Book-recommendation-System
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate the environment on Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

Install the required libraries:

```bash
pip install pandas numpy scipy scikit-learn matplotlib seaborn jupyter
```

Place the three dataset files inside the `dataset/` directory.

Open the project in VS Code and run:

```text
notebooks/Book_Recommendation_Analysis.ipynb
```

Execute the notebook cells in order.

## Limitations

- The recommendation system currently generates Hybrid recommendations for a limited set of 32 users.
- Content-based and collaborative-filtering signals are not available for every candidate book.
- The final Hybrid ranking uses a diversity constraint, which influences the recommendation distribution.
- The Hybrid approach requires further evaluation using appropriate ranking metrics such as Precision@K, Recall@K, and NDCG@K.
- Sparse user-rating data can limit the effectiveness of collaborative filtering.
- The system currently focuses on book recommendations using the available dataset rather than real-time user interactions.

## Future Improvements

- Evaluate recommendation quality using Precision@K, Recall@K, and NDCG@K.
- Improve the balance between content-based and collaborative-filtering signals.
- Experiment with different Hybrid scoring weights.
- Explore matrix factorization techniques.
- Improve recommendations for users with limited rating history.
- Develop an interactive interface for users to receive personalized book recommendations.

## Author

**Nandini Gupta**

B.Tech – Computer Science and Engineering (Health Informatics)

VIT Bhopal University

---

*This project was developed as an exploration of recommendation algorithms and their application to personalized book discovery.*