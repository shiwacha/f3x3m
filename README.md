# f3x3m - Automated NIFTY Options Trading Strategy

This project contains a Jupyter Notebook (`02_10_2025_7AM_Experiment_f3x3m_LATEST_1.ipynb`) that implements an automated trading strategy for NIFTY options. It connects to the Zerodha Kite API to execute trades based on a specific set of rules and user-configurable parameters.

## Strategy Overview: "f3x3m"

The "f3x3m" strategy is designed to identify and act on trading opportunities within the first few minutes of the market open.

1.  **Signal Identification:** The strategy monitors the first three 3-minute candles of the trading day (from 9:15 AM to 9:24 AM IST). A "signal bar" is identified if a candle's **open price is below the cumulative VWAP** and its **close price is above the cumulative VWAP**.

2.  **Entry Trigger:** After a signal is found, the strategy waits for an entry trigger. An entry is triggered if the live traded price (LTP) of the option is at or below a level calculated from the VWAP and a user-defined **Entry Trigger Offset (ETO)**.

3.  **Order Placement:** When the entry is triggered, a BUY LIMIT order is placed. The limit price is calculated using the VWAP and a user-defined **Entry Order Offset (EOO)**.

4.  **Automated SL/Target:** Once the entry order is filled (either partially or fully), the strategy immediately calculates and places a Stop-Loss (SL) and Target order.
    *   The **Stop-Loss** is determined by the open price of the signal bar and two user-defined offsets: **Stop Loss Trigger Offset (SLTO)** and **Stop Loss Limit Offset (SLLO)**.
    *   The **Target** is calculated based on the entry price, the stop-loss level, and a user-defined **Risk-to-Reward Ratio (RRR)**.

## Features

*   **Kite API Integration:** Securely connects to your Zerodha account to fetch data and place live orders.
*   **Interactive UI:** A user-friendly interface built with `ipywidgets` allows you to configure all strategy parameters without editing the code.
*   **Automated Execution:** Handles the entire trade lifecycle, from signal detection to entry, stop-loss placement, and target monitoring.
*   **Configurable Parameters:** Easily adjust key strategy parameters like Risk-to-Reward, Capital Allocation, Entry/Exit Offsets, and more.
*   **Manual Overrides:** Provides options to manually set the expiry date and strike prices.
*   **Real-time Monitoring:** Displays live updates on order status, prices, and strategy state directly in the notebook.

## Prerequisites

*   A Zerodha Kite developer account with API key and secret.
*   Python environment with Jupyter Notebook or Google Colab.
*   Required Python libraries: `kiteconnect`, `pandas`, `pytz`, `ipywidgets`.

## How to Use

1.  **Installation:**
    *   Open the `02_10_2025_7AM_Experiment_f3x3m_LATEST_1.ipynb` notebook in Google Colab or a local Jupyter environment.
    *   The first cell will automatically install the necessary libraries, including `kiteconnect`.

2.  **Authentication:**
    *   Run the first two cells of the notebook.
    *   In the **Cell no. = 2**, you will be prompted to enter your `api_key` and `api_secret`.
    *   A login URL will be generated. Open it, log in to your Kite account, and you will be redirected to a URL containing a `request_token`.
    *   Copy this `request_token` and paste it back into the input field in the notebook.

3.  **Configuration:**
    *   **Set Manual Expiry Dates (Cell `c75237e7`):** Before running the main UI, configure your desired weekly and monthly expiry dates in this cell.
    *   **Run the UI (Cell `lnhaR_wLGbS9`):** Execute this cell to display the main strategy configuration interface.
    *   **Configure Parameters:** Use the interactive UI to set all your desired trading parameters:
        *   **Exit Half:** Configure partial profit-taking.
        *   **Expiry Selection:** Choose between the pre-configured weekly or monthly expiry.
        *   **Strike Selection:** Use "Auto Strike" (calculated from the day's open) or manually enter CE/PE strike prices.
        *   **RRR & Capital:** Set your desired Risk-to-Reward Ratio and the capital (in thousands) to be deployed.
        *   **Offsets (ETO, EOO, SLTO, SLLO):** Configure the percentage-based offsets for entry and stop-loss calculations.
        *   **Validity:** Set the time duration for which the entry trigger will remain valid after a signal is found.

4.  **Execution:**
    *   Once all parameters are configured, click the **"Run f3x3m"** button.
    *   The notebook will start monitoring the market for signals and will execute trades automatically based on your configuration.
    *   The output area below the UI will display live logs, order updates, and the current state of the strategy.

## Disclaimer

This project is for educational and experimental purposes only. Automated trading involves significant risk, including the potential for capital loss. The author is not responsible for any financial losses incurred from using this software. Always test thoroughly in a simulated environment before deploying with real capital. Use at your own risk.