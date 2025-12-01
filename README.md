# DataExplain Agent: Automated Exploratory Data Analysis Using AI Agents

## 1. Introduction

Exploratory Data Analysis (EDA) is essential for understanding new datasets, but it is often time-consuming and repetitive.
DataExplain Agent is an AI-powered multi-agent system that automates EDA by analyzing uploaded datasets, generating visualizations, and producing clear, structured insights.

This project was developed as part of the Google 5-Day AI Agents Intensive, demonstrating how multiple agents and tools can collaborate to produce meaningful, high-quality data analysis.

## 2. Problem Statement

Many analysts and data scientists spend significant time:

<ul><li>Loading and inspecting new datasets</li>
<li>Checking missing data</li>
<li>Exploring distributions and categorical balance</li>
<li>Creating multiple visualizations</li>
<li>Manually writing summary insights</li></ul>

This slows down project workflows and creates inconsistency—especially when multiple users work across different datasets.

There is a need for an intelligent system that can automate the initial EDA process in a reliable, consistent, and easy-to-use manner.

## 3. Solution Overview

DataExplain Agent is a multi-agent workflow that:

<ol><li>Accepts any CSV dataset</li>

<li>Loads and inspects the data</li>

<li>Generates grouped visualizations:

<ul><li>Histograms (numeric)</li>
<li>Boxplots (numeric)</li>
<li>Bar charts (categorical)</li>
<li>Correlation heatmap</li></ul>
<li>Computes summary statistics</li>
<li>Uses an LLM (Gemini) to produce insights</li>
<li>Uses a critic model to refine the insights</li>
<li>Produces a structured, readable EDA report in Markdown</li>
<li>Answers natural-language questions about the dataset</li></ul></ol>

This workflow reduces effort, standardizes output, and makes EDA accessible even to non-technical users.

## 4. Multi-Agent Architecture

The system uses a sequential multi-agent workflow, where each agent has a clearly defined role.

### 4.1 EDA Agent

<ul><li>Loads the dataset using load_csv_tool</li>
<li>Generates all visualizations using generate_plots_tool</li>
<li>Computes basic statistics using basic_stats_tool</li></ul>

### 4.2 Insight Agent

<ul><li>Uses Gemini to interpret the dataset characteristics</li>
<li>Produces a detailed narrative describing trends and patterns</li></ul>

### 4.3 Critic Agent

<ul><li>Evaluates the first draft of insights</li>

<li>Identifies missing details or unclear reasoning</li></ul>

### 4.4 Refinement Agent

<ul><li>Produces the final polished report</li>

<li>Includes structured sections such as:

<ul><li>Dataset overview<li>

<li>Numeric variable analysis</li>

<li>Categorical variable analysis</li>

<li>Correlation summary</li>

<li>Suggested next steps</li></ul></li></ul>

### 4.5 Ask-My-Data

A simple natural-language Q&A interface that answers questions such as:

<ul><li>What is the average Age?</li>

<li>How many unique classes are there?</li>
<li>What percent of the Cabin column is missing?</li></ul>

## 5. Tools Implemented
### 5.1 load_csv_tool

Reads the dataset and returns:

<ul><li>Columns</li>

<li>Data types</li>

<li>Row/column count</li>

<li>Sample preview</li></ul>

### 5.2 generate_plots_tool

Automatically generates:

<ul><li>Histogram grid for numeric columns</li>

<li>Boxplot grid for numeric columns</li>

<li>Bar charts for categorical columns</li>

<li>Correlation heatmap</li>
</ul>
All plots are saved to a folder and displayed in the notebook.

### 5.3 basic_stats_tool

Computes key statistics:

<ul><li>Mean</li>

<li>Median</li>

<li>Missing percentage</li>

<li>Unique count</li></ul>

### 5.4 ask_data

Uses Gemini to identify:

<ul><li>The column referenced in the question</li>

<li>The statistic requested</li>
</ul>
Then uses the tools to compute the answer.


## 6. DataExplain Workflow
### Step 1: Upload CSV

User uploads any .csv file in the notebook.

### Step 2: Run the Agent
```
session = run_data_explain(
    file_bytes=file_bytes,
    user_goal="Understand key patterns in the dataset",
    user_id="user123"
)
```
### Step 3: View the Report
```
from IPython.display import Markdown, display
display(Markdown(session["final_report"]))
```
### Step 4: Optional Q&A
ask_data("How many unique Species are there?", file_bytes)


## 7. Example Output

The final Markdown report includes:

<ul><li>Dataset dimensions</li>

<li>Summary of numeric column distributions</li>

<li>Categorical breakdown</li>

<li>Correlation analysis</li>

<li>Notable patterns identified by the LLM</li>

<li>A refined and structured narrative</li></ul>

Plots appear inline and are also saved in a directory.

## 8. Setup Instructions
### Environment

<ul><li>Kaggle notebook</li>

<li>Gemini API key stored securely in GOOGLE_API_KEY via Kaggle secrets</li></ul>

### How to Use

<ol><li>Add your Google API key in Kaggle → Settings → Secrets</li>

<li>Upload your CSV file</li>

<li>Run the notebook from start to finish</li>

<li>The report and plots will be generated automatically</li></ol>

## 9. Limitations

<ul><li>Not optimized for extremely large datasets</li>

<li>Insight quality depends on the LLM response</li>

<li>Visualizations may be dense if dataset has many columns</li>

<li>No cloud deployment included</li></ul>


## 10. Future Enhancements

<ul><li>Automated missing-value handling</li>

<li>Outlier detection</li>

<li>Feature importance ranking</li>

<li>Additional visualization types</li>

<li>Integration with dashboards or web UI</li></ul>

## 11. Conclusion

DataExplain Agent demonstrates how multi-agent workflows, tools, and LLM-based reasoning can automate Exploratory Data Analysis.
It provides analysts and data scientists with faster, more consistent insights while reducing manual effort.

This project reflects practical agent design, tool integration, and the application of generative AI for real-world data analysis.

