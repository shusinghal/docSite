**Trading Strategy**
====================

Define your trading strategy in the `strategy.py` file. Use the following variables to store your data:

* **StockName** (String): Name of the stock you want to trade.
* **EntryPrice** (Float): The price at which you want to enter the trade.
* **Segment** (String): The stock exchange segment (e.g., "NSE" or "BSE").
* **ProductCode** (String): Allowed values are "CNC" (Cash & Carry) and "MIS" (Margin Intraday Square Off).
* **OrderType** (String): Allowed values are "MKT" (Market Order) and "SL-M" (Stop-Loss Market Order).
* **Quantity** (Integer): The number of shares you want to buy or sell.
* **TransactionType** (String): Allowed values are "B" for buy and "S" for sell. 

**Note:** These variables are designed to be used by the system for further operations related to your trading strategy.
