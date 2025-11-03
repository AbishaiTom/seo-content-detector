# SEO Content Quality & Duplicate Detector

This repository contains the solution for the Data Science Assignment. It's a Python pipeline built in a Jupyter Notebook that processes website HTML, engineers features, detects duplicate content, and predicts content quality using a machine learning model.

---

### Project Overview

The pipeline ingests a CSV of raw HTML content and performs the following steps:
1.  **HTML Parsing:** Extracts the title and clean body text from raw HTML.
2.  **Feature Engineering:** Calculates features like word count, readability (Flesch score), sentence count, and top keywords.
3.  **Duplicate Detection:** Generates vector embeddings for each document and uses cosine similarity to find pairs with >80% similarity.
4.  **Quality Modeling:** Trains a Logistic Regression model to classify content as 'High', 'Medium', or 'Low' quality based on business rules.
5.  **Real-Time Demo:** A final function allows for on-demand analysis of any live URL.

---

### How to Run

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/](https://github.com/)[YOUR_USERNAME]/seo-content-detector.git
    cd seo-content-detector
    ```

2.  **Create a virtual environment (Recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook notebooks/seo_pipeline.ipynb
    ```

5.  **Run the notebook:**
    Once open, you can run all cells from top to bottom. The notebook will read from `data/data.csv` and generate all other output files (`extracted_content.csv`, `features.csv`, etc.) in the `data/` directory.

---

### Key Decisions & Project Structure

* **HTML Parsing:** Used `BeautifulSoup` with a fallback strategy (`<article>` -> `<main>` -> all `<p>` tags) to robustly handle different website layouts.
* **Duplicate Detection:** Chose `sentence-transformers` ('all-MiniLM-L6-v2') to generate semantic embeddings. This is more powerful than TF-IDF as it understands the *meaning* of the text, not just keywords.
* **Quality Model:** Used `LogisticRegression` as it's a simple, fast, and interpretable baseline model. Given the small dataset (68 samples), a more complex model would likely overfit.
* **Error Handling:** All parsing and I/O functions are wrapped in `try-except` blocks to handle missing data or parsing failures gracefully.

**File Structure:**

seo-content-detector/
├── data/
│   └── data.csv  <-- Original data
├── notebooks/
│   └── seo_pipeline.ipynb 
├── .gitignore
├── README.md
├── requirements.txt

---

### Results Summary

* **Total Pages Processed:** 68
* **Duplicate Pairs Found:** 10
* **Thin Content Pages (<500 words):** 36
* **Model Performance:**
    * The model achieved an F1-score of  0.41.
    * *Note: Model performance is based on a very small test set (~21 samples) due to the small initial dataset. Results would be more robust with more data.*