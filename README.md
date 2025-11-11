# Quantitative-Active-Management
A pedagogical implementation of the Grinold-Kahn framework for systematic portfolio construction and risk analysis.

This repository contains a pedagogical implementation of the core concepts from Grinold & Kahn's seminal book, "Active Portfolio Management." The project is organized into a series of Jupyter Notebooks that walk through the end-to-end process of building a quantitative investment framework.

## Project Goal
The primary goal of this project is to provide a clear, practical, and code-based demonstration of the key components of a systematic investment process, including:
-   Data loading and cleaning for a universe of stocks.
-   Construction of factor exposures (e.g., Value, Size).
-   Estimation of a multifactor risk model using the Fama-MacBeth procedure.
-   Definition and neutralization of an alpha signal (e.g., Momentum).
-   Construction of an optimal active portfolio based on the Value Added (VA) objective.

## Data
This project uses publicly available data from CRSP and Compustat, accessed via the Wharton Research Data Services (WRDS) cloud. The universe is a sample of US large-cap stocks.

## Structure
The project is broken down into the following notebooks:
1.  `01_Data_Preparation.ipynb`: Loading and cleaning the data.
2.  `02_Factor_Exposure_Creation.ipynb`: Building the 'X' matrix.
3.  ...and so on.

*This project is for educational and demonstrative purposes only and does not constitute investment advice.*
