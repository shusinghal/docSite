## Welcome to Neo
## Commands

Welcome to neo
================

Application workflow
----------------------
* Check if the session is login.
* Check if date is today.
* Check if market is open.
* Look at algorithm and get order parameters.
* Place order and check if it is successful.
* Look at second leg of algorithm to get stop loss details.
* Place stop loss.

## Project layout

	* main.py - Entry point for the code. It acts as facilitator to connect all parts of application.
	* login/ - A folder that contains all files required for login. Neo requires 3 step login process. 
	* placeOrder - A foler that contains files to run order APIs. It has place new order, cancel order, order book, and trade book files.
	* Eveningorder.py - Entry point for the code in evening. It is similar to main.py and acts as a facilitator to close all positions if open.
	* keys.py - A file that stores session keys.
	* logfile.txt - A simple text file that captures application logs.
	* ltp.xml - A file that stores the last trade price of the stock.
	* manualUpdate.py - A file that manually updates the excel in case I make mistake or code doesn't run.
	* telegrambot.py - Sends trade relate messages to me on telegram.
	* webSocket.py - Get stock details like - open, high, low, close.
	
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
