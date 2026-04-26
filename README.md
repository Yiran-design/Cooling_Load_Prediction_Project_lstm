# Cooling Load Prediction Project (LSTM Focus)

## Project Overview

This repository documents a set of experiments on short-term building cooling load forecasting using weather variables, time-related features, and historical cooling load information. The main focus of the repository is the **LSTM baseline vs refined workflow**, while related subgroup results from **Weekly Average**, **ARIMA**, and **XGBoost** are also summarized for broader methodological comparison.

The study uses cooling load and weather data for **Buildings A, B, C, and D** in **May 2024**. Because the May 2024 data for **Building B** were incomplete or unavailable, the detailed notebook workflow and final refined experiments focus on **Buildings A, C, and D**, with **Building C** used as the main illustrative case study.

## Main Objectives

- Review the baseline LSTM cooling load forecasting notebook.
- Identify limitations in preprocessing, feature representation, and training strategy.
- Implement and evaluate practical refinements.
- Summarize and compare forecasting performance across buildings and models.

## Methods Covered

### Main workflow in this repository
- **LSTM Baseline**
- **LSTM Refined**

### Comparative methods reported in subgroup experiments
- **Weekly Average**
- **ARIMA**
- **XGBoost**

## Key LSTM Refinements

The refined LSTM workflow retained the overall one-step-ahead forecasting structure but introduced several practical changes:

1. **Historical CoolingLoad added to the sequence input**  
   This is the most important refinement. The effective input changed from **14 engineered weather/time features** to **15 channels** by adding past CoolingLoad values directly into the sequence.

2. **Improved training configuration**  
   For Buildings C and D, the LSTM activation was changed from `relu` to `tanh`, and the loss function was changed from `MSE` to `Huber`.

3. **Lookback testing**  
   A 24-hour lookback window was tested, but it did **not** provide systematic gains compared with the 12-hour configuration.

## Final Experimental Results

### LSTM Baseline vs Refined (Buildings A, C, and D)

| Building | Model    | MAE    | RMSE    | MAPE (%) | sMAPE (%) |
|----------|----------|--------|---------|----------|-----------|
| A        | Baseline | 297.33 | 599.48  | 2893.20  | 146.38    |
| A        | Refined  | 27.28  | 421.41  | 7169.06  | 141.03    |
| C        | Baseline | 1076.99| 1757.29 | 602.51   | 44.28     |
| C        | Refined  | 457.33 | 807.10  | 643.41   | 20.72     |
| D        | Baseline | 106.08 | 174.67  | 128.32   | 74.49     |
| D        | Refined  | 84.49  | 136.08  | 154.60   | 75.88     |

### Cross-Model Comparison

| Model                      | MAE    | RMSE    | MAPE (%) | sMAPE (%) |
|---------------------------|--------|---------|----------|-----------|
| Weekly Average            | 60.35  | 103.45  | 40.81    | --        |
| ARIMA                     | 123.35 | 260.05  | 136.27   | --        |
| XGBoost                   | 390.33 | 605.35  | 594.17   | --        |
| LSTM Baseline (Building C)| 1076.99| 1757.29 | 602.51   | 44.28     |
| LSTM Refined (Building C) | 457.33 | 807.10  | 643.41   | 20.72     |

## Main Findings

- The **most consistently effective refinement** was the inclusion of **historical CoolingLoad** in the input sequence.
- This modification provided the clearest improvement across the LSTM experiments, especially for **Building C**.
- Additional changes such as `tanh` activation and `Huber` loss were useful mainly for **Buildings C and D**.
- Extending the lookback window from **12 hours to 24 hours** did **not** produce systematic gains.
- Overall, the experiments suggest that **input representation matters more than simply increasing model complexity**.

## Repository Contents

This repository contains:

- baseline and refined Colab notebooks,
- saved notebook snapshots corresponding to completed runs,
- exported metric summaries in JSON format,
- train/test calendar plots,
- training-history figures,

## Reproducibility

All final LSTM experiments were conducted in **Google Colab** using an **NVIDIA T4 GPU** runtime. Results were exported and organized in a structured format so that baseline and refined outputs can be traced independently by building and experiment type.

## GitHub Repository

Repository URL: https://github.com/Yiran-design/Cooling_Load_Prediction_Project_lstm

## Notes

- Building B is excluded from the detailed refined workflow because the required May 2024 data were incomplete or unavailable.
- The main narrative of the accompanying report uses **Building C** as the detailed case study, while **Buildings A and D** are included for cross-building comparison.
- The LSTM notebook refinement study is the primary focus of this repository, while Weekly Average, ARIMA, and XGBoost results are included for methodological comparison.
