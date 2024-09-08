Place order
=====================
The system uses your strategy to: 
* Place a new order
* Ensures that your order is confirmed
* Place a stop loss order 
* Sends updates via Telegram

OR

* Check your position
* Close your position
* Cancel your stop loss order
* Sends updates via Telegram

Opening a new position
----------------------------
This program checks for your active trading session.
It uses the Excel file and inputs from your strategy to place a new order.
It uses the unique order number to check for the trade status.

Checking Positions:
-----------------------
The program reads all your positions. If the difference between the total buy quantity and total sell quantity is not zero, it assumes that your position is open.

Stop-Loss Order:
--------------------
The program creates a new stop-loss order for the same quantity of the stock.

Telegram Notification:
-------------------------
The program sends you an update on the Telegram application.

Closing an existing position
----------------------------------
This program checks for your active trading session at the end of trading time.
It checks for your open positions.
The program then performs the following actions:
* Closes your positions.
* Cancels your stop-loss order.
* Updates the Excel sheet with profit and loss calculations.
* Sends you an update via Telegram.
