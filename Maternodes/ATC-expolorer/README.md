## ATC BLOCKCHAIN EXPOLORER

## ATC-Masternode TX

Simple bash script for listing masternode payments in USD.
Usage:

    save ATC-mnTax.sh and execute chmod 755 ATC-mnTax.sh
    Usage: bash ATC-mnTax.sh <ATC> [<START ATC> <END DATE>]
    Example: bash ATC-mnTax.sh RXXdEmOjfadjfiieur8fjdkewi7849jfdls "2017-01-01 00:00:00" "2017-12-31 23:59:59"

## Description:

This script will list all masternode payments (earliest starting August 2017) and their US Dollar value at that given time.

## Algorithm:

    Get MN transaction data from ATC block explorer
    
    Printing History and calculating Total USD Income

Initial release
