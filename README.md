USSD-Message-read-by-GSM-Modem-Python
=====================================

USSD-Message-read-by-GSM-Modem-Python

Use GSM modem and enter your comm port manually.
import logging
from __future__ import print_function


PORT = 'Your port number'
BAUDRATE = 9600
USSD_Text = '*124#'

PIN = None

from gsmmodem.modem import GsmModem
def main():
    print('Modem Initialization...')
    
    modem = GsmModem(PORT, BAUDRATE)
    modem.connect(PIN) #not necessary
	
    modem.waitForNetworkCoverage(15)
    print('Send USSD text: {0}'.format(USSD_Text))
    response = modem.sendUssd(USSD_Text) # response type: gsmmodem.modem.Ussd
    print('USSD Message Received: {0}'.format(response.message))
    if response.sessionActive:
        print('Closing USSD session.')
        # Here we can send another message
        response.cancel()
    else:
        print('USSD session Terminated.')
    modem.close()

if __name__ == '__main__':
    main()
