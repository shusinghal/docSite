#Edit this file to view the sample code in proper intended format.

## Sample Python Code 
### Login and place trade in live market
from login.otpValidate import otpValidate
from placeOrder.placeOrder import compute
from datetime import date
from login.jwtDecode import jwtDecode
from login.accessToken import accessToken
from login.viewToken import viewToken
import time
import os.path
from keys import writeKeys, readKeys
from telegramBot import teleMsgSuccess, mayhem, userExpired
from waitTime import mrngWait
from placeOrder.orderBook import orderHistory
import webSocketSand
from schedule import marketStatus
from SLOrdercancel import SLOrderNo
from placeOrder.orderBook import openPosition

# def __init__(self, at, token, sid, hsServerId):
#     self.at = at
#     self.token = token
#     self.sid = sid
#     self.hsServerId = hsServerId

def login():
    at = accessToken()
    jwts,sid1 = viewToken(at)
    subs = jwtDecode(jwts)
    token, sid2,hsServerId, isUserPwdExpired = otpValidate(subs,sid1,jwts,at)
    if (isUserPwdExpired == True):
        userExpired()
    else:
        writeKeys(at, token, jwts, sid2,hsServerId, subs)
    
def Orders():
    if os.path.isfile("keys.xml"):
        dateTime, at, token, sid, hsServerId = readKeys()
        current = str(date.today())
        waitTime,h = mrngWait() #5,11
        if dateTime == current:
                print("Waiting for "+str(waitTime)+ " seconds.")
                webSocketSand.openTrade(token, sid, hsServerId)
                orderType="new"
                compute(at, token, sid, hsServerId,orderType)
                time.sleep(waitTime) # wait for market to open. Then check position and place SL order.
                stock_position = openPosition(at, token, sid, hsServerId)
                for stock, position, qty in stock_position:
                    teleMsgSuccess(f"{position} {qty} stocks of {stock}")
                slNList = compute(at, token, sid, hsServerId, orderType="sl")
                for nOrderN, stock in slNList:
                        if nOrderN != "00000":
                            SLOrderNo(nOrderN, stock)
                            teleMsgSuccess("SL Order")
                        else:
                            mayhem(f" SL order for  {stock} is not placed.")
        else:
            max_retries = 5
            for i in range(max_retries):
                try:
                    # Your API call here
                    marketstatus = marketStatus()
                    break
                except Exception:
                    print(f"JSONDecodeError occurred. Retrying... ({i+1}/{max_retries})")
                    time.sleep(2)  # Wait for 2 seconds before retrying
            if marketstatus.lower() in ['close', 'closed']:
                pass
            else:
                login()
                Orders()
    else:
        login()
        Orders()

# def slOrder(at, token, sid, hsServerId, avgPrc, fldQty):
#     slN = SLOrder(at, token, sid, hsServerId, avgPrc, fldQty)
#     return(slN)

Orders()
