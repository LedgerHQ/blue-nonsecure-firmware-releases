# Official Non Secure firmware images for Ledger Blue, version 1.1

This directory contains the deterministic hex files and signed image of the non secure (STM32) firmware images for Ledger Blue 

For this specific release, proceed as follows : 

  - First check out and perform the Secure Operating System upgrade as described on https://github.com/LedgerHQ/blue-secure-sdk/bluer11
  - Turn on Ledger Blue, keeping the button pressed until "secure bootloader", then "bootloader" is displayed
  - Update the bootloader with the following command. Following the update, the script displays an error and the device turns off

``` 
python -m ledgerblue.runScript --fileName bootloader/stm32l476_blue_bootloader_upgrade.patch_apdu      
```
  - Turn on Ledger Blue, the device displays "Upgrading Bootloader", then turns off
  - Turn on Ledger Blue, keeping the button pressed until "secure bootloader", then "bootloader" is displayed
  - Update the firmware with the following command 

```
python -m ledgerblue.runScript --fileName main/stm32l476_seproxyhal.patch_apdu
```
  - The device is back to the "Connect USB" screen, perform the remaining part of the Secure Operating System upgrade as described on https://github.com/LedgerHQ/blue-secure-sdk/bluer11  

