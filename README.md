# AI-Powered Data Analysis of Olympic History 🥇

This project demonstrates how to use a large language model (Google's Gemini API) to perform automated data analysis and visualization on the "120 years of Olympic history" dataset. The Python script takes natural language questions, asks the AI to generate corresponding `pandas` and `matplotlib`/`seaborn` code, and then executes that code locally to produce answers and charts.

## Features

-   **Natural Language to Code:** Translates plain English questions into executable Python code.
-   **Multi-Level Analysis:** Answers basic, intermediate, and advanced analytical questions.
-   **On-the-Fly Feature Engineering:** Capable of generating code that creates new columns (e.g., BMI, Decade) for deeper analysis.
-   **Automated Visualization:** Generates various plots (bar charts, histograms, scatter plots, etc.) from natural language requests.
-   **File-Based Output:** Saves all generated visualizations as `.png` image files.

---

## ⚙How It Works

The project's core is a "generate and execute" pattern. Instead of sending the entire (potentially large) dataset to the AI, we only send the *structure* of the data and ask the AI to write a script. We then run that script on our local data.

### 1. For Data Analysis

1.  A natural language question (e.g., "What are the top 5 teams with the most medals?") is sent to the Gemini API.
2.  The prompt instructs the AI to return **only** a Python script that operates on a DataFrame `df` and stores the final answer in a variable named `result`.
3.  The returned code string is executed in the local Python environment using `exec()`. This environment is given access to the `df` DataFrame and the `pandas` and `numpy` libraries.
4.  The script then prints the value stored in the `result` variable.

### 2. For Visualizations

1.  A natural language request for a plot (e.g., "Generate a bar chart showing the top 10 countries...") is sent to the Gemini API.
2.  The prompt instructs the AI to return a Python script that uses `matplotlib` and `seaborn`.
3.  **Crucially**, the prompt forbids the AI from using `plt.show()` and instead forces it to save the plot to a file using `plt.savefig('filename.png')`.
4.  The script is executed locally using `exec()`, which is given access to all necessary libraries (`pandas`, `numpy`, `matplotlib.pyplot`, `seaborn`).
5.  A success message is printed, and a new `.png` image file appears in your project directory.

---
