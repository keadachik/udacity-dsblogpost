# Stack Overflow 2024 Developer Survey Analysis

This repository contains my project for the first part of the Udacity Data Scientist Nanodegree. The goal was to explore the Stack Overflow Developer Survey 2024 dataset to understand current trends in the developer community.

## Project Motivation

As a frequent user of Stack Overflow, I was curious about the insights hidden in their annual developer survey data. This project aimed to practice the fundamental data analysis workflow – from loading and cleaning data to visualizing trends and exploring relationships using Python.

My main interests were:
*   Finding out which programming languages are most popular right now.
*   Seeing how developer salaries compare across different countries.
*   Trying to understand what factors might be linked to higher compensation.

I looked at similar analyses of previous Stack Overflow surveys on platforms like Kaggle and GitHub to get ideas on how to approach survey data and choose appropriate visualizations. Projects like [Stack Overflow Developer Survey Analysis by Raza MH](https://www.kaggle.com/code/razamh/stack-overflow-developer-survey-analysis) and [Stack-Overflow-Annual-Developer-Survey-2023-EDA by Kayne Ong](https://github.com/kayneong/Stack-Overflow-Annual-Developer-Survey-2023-EDA) were particularly helpful in structuring my approach.

## Installations

The main analysis is done in a Jupyter Notebook (`.ipynb`). To run the code, you'll need Python 3 and the following libraries:

*   pandas
*   numpy
*   matplotlib
*   seaborn
*   plotly
*   pycountry
*   scikit-learn

You can install these libraries using pip:
```bash
pip install pandas numpy matplotlib seaborn plotly pycountry scikit-learn
```
It's recommended to use a virtual environment (like `venv` or `conda`) to manage dependencies.

## File Descriptions

*   **`Stack-Overflow-Data-Analysis.ipynb`**: The main Jupyter Notebook containing the entire data analysis process: data loading, cleaning, exploratory data analysis (EDA) for the key questions, a simple linear regression model to explore compensation factors, and conclusions.
*   **`survey_results_schema.csv`**: Contains the schema mapping column names (`qname`) to the survey question text. Used for understanding the data columns.
*   **`survey_results_public.csv`**: The main dataset with survey responses. **Note: This file is very large (>100MB) and is NOT included in this repository due to GitHub file size limits.** You need to download it separately (see "How to Interact" section).
*   **`.gitignore`**: Specifies files intentionally untracked by Git (like the large data file and virtual environment files).
*   **`README.md`**: This file, providing an overview of the project.

## How to Interact with the Project

1.  Clone this repository to your local machine.
2.  Set up a Python environment and install the required libraries listed in the "Installations" section.
3.  **Download the `survey_results_public.csv` file** from the official [Stack Overflow Survey 2024 website](https://survey.stackoverflow.co/2024/) and place it in the root directory of the cloned repository.
4.  Open and run the `Stack-Overflow-Data-Analysis.ipynb` notebook using Jupyter Notebook or Jupyter Lab.

## Summary of Results

The analysis focused on three main questions:

1.  **Most Common Languages:** JavaScript, Python, and HTML/CSS were the top 3 most commonly used languages, suggesting a strong focus on web development technologies among respondents.
2.  **Compensation by Country:** Significant differences in median annual compensation were observed across countries. After filtering for countries with a sufficient number of responses (>=200), the USA, Switzerland, and Israel showed notably higher compensation levels compared to others like India or Brazil. However, the data is geographically biased towards North America and Europe.
3.  **Factors Associated with Compensation:** A simple Linear Regression model was built to explore factors linked to compensation. While the model's overall accuracy was low (R² ≈ 0.19), the analysis indicated that **years of professional experience** and **working in the United States** were the factors most strongly associated with higher predicted compensation within this model. Education level seemed to play a less significant role. The low accuracy highlights that predicting salary is complex and depends on many factors not fully captured by this simple model.

## Licensing, Authors, Acknowledgements

*   **License:** This project is licensed under the MIT License - see the LICENSE file (you would need to add an actual MIT license file if you want this) or simply state "No license specified" if you prefer. *Suggestion: Using MIT is common and simple.*
*   **Author:** [Your Name or GitHub Handle]
*   **Acknowledgements:**
    *   Thanks to Stack Overflow for making the survey data publicly available.
    *   Inspiration and guidance for data handling and visualization techniques were drawn from publicly available notebooks on Kaggle and discussions on Stack Overflow related to developer surveys.

