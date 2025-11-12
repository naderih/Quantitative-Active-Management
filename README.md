# A Pedagogical Implementation of the Grinold-Kahn Framework

## Project Overview

This repository contains a simple, pedagogical implementation of the core concepts from Grinold & Kahn's seminal book, "Active Portfolio Management." The project is organized into a series of Jupyter Notebooks that walk through an end-to-end quantitative investment process, from data preparation to optimal portfolio construction and risk attribution.

**Disclaimer:** This project is for educational and demonstrative purposes only. It uses a small, static universe of stocks and simplified models. It is not intended to be a real-world investment strategy and does not constitute investment advice. The framework is designed to be a clear illustration of the theory, with the potential for future expansion and enhancement.

---

## The Core Framework: A Blueprint

The project follows the disciplined, quantitative approach to active management pioneered by Grinold & Kahn. The core idea is to separate the investment process into distinct, manageable components:

1.  **Risk Modeling:** We first build a model to understand and forecast the sources of risk. Instead of using a simple historical covariance matrix, we construct a **multifactor risk model**. This model posits that asset returns are driven by a set of common factors and a stock-specific (idiosyncratic) component. The total covariance matrix ($V$) is defined as:
    ```math
    $V = XFX^T + \Delta$
    ```
    *   $X$: The Factor Exposure matrix (the "DNA" of each stock).
    *   $F$: The Factor Covariance matrix (the "macro blueprint" of how factors interact).
    *   $\Delta$: The Specific Risk matrix (the idiosyncratic risk of each stock).

2.  **Alpha Modeling:** We then generate a forecast of **expected residual return**, or **alpha ($\alpha$)**. A key step in a professional process is to ensure these alpha signals are **benchmark-neutral**. This purifies the signal, separating true stock-selection skill from any implicit market bets.
    ```math
    h_B^T \alpha = 0```

3.  **Portfolio Construction:** Finally, we use a **quadratic optimizer** to combine our alpha signal with our risk model. The goal is to build the optimal active portfolio ($h_{PA}$) that maximizes the manager's **Value Added (`VA`)** objective function. This function creates a disciplined trade-off between the expected reward (alpha) and the active risk taken.
    ```math
    \text{Maximize:} \quad VA = \alpha_p - \lambda_R \cdot \psi_p^2
    ```
    The solution to this optimization gives us the optimal active holdings:
    ```math
    h_{PA}^* = \frac{1}{2 \lambda_R} V^{-1} \alpha
    ```

---

## Project Structure & Notebooks

The project is broken down into a sequential pipeline, with each notebook representing a key stage of the process.

**`01_Data_Preparation.ipynb`**
*   **Purpose:** Sources historical price data from `yfinance` and risk-free rate data from the Fama-French library.
*   **Output:** Cleaned time series of monthly excess returns for our stock universe.

**`02_Factor_Exposure_Creation.ipynb`**
*   **Purpose:** Constructs the Factor Exposure matrix ($X$).
*   **Process:** Calculates standardized, capitalization-weighted exposures for three classic style factors: **Size**, **Value**, and **Momentum**.
*   **Output:** The $X$ matrix, representing the "DNA" of each stock.

**`03_Risk_Model_Estimation.ipynb`**
*   **Purpose:** Estimates the components of the multifactor risk model ($F$ and $\Delta$).
*   **Process:** Implements the **Fama-MacBeth procedure** by running monthly cross-sectional regressions to generate a time series of factor returns and specific returns. These are then used to calculate the Factor Covariance matrix ($F$) and Specific Variances ($\Delta$).
*   **Output:** The core components of the risk model.

**`04_Alpha_Signal_Definition.ipynb`**
*   **Purpose:** Generates a clean, benchmark-neutral alpha signal.
*   **Process:** Uses a raw **Momentum** signal as the starting point, diagnoses its inherent benchmark bias, and then applies a **beta-adjusted neutralization** to purify the signal.
*   **Output:** The final alpha vector ($\alpha$) ready for optimization.

**`05_Portfolio_Construction.ipynb`**
*   **Purpose:** The final synthesis. Constructs the optimal active portfolio and performs risk attribution.
*   **Process:** Uses the `VA` objective function and the outputs from all previous notebooks to solve for the optimal active holdings ($h_{PA}^*$). It then analyzes the final portfolio's characteristics.
*   **Output:** A final "Risk & Attribution Report" that shows the optimal portfolio's expected alpha, beta, tracking error, and, crucially, a **decomposition of its active risk** into factor-driven and stock-specific sources.

