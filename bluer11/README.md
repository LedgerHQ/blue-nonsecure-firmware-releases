# Official Non Secure firmware images for Ledger Blue, version 1.1

This directory contains the deterministic hex files and signed image of the non secure (STM32) firmware images for Ledger Blue 

This release also includes a Secure Operating System update. 

To install it, proceed as follows : 

  - Make sure to install the Python loader application from https://github.com/LedgerHQ/blue-loader-python (latest version or release 1.1) and operate in the same Python virtual environment
  - Check out the Secure Operating System update from https://github.com/LedgerHQ/blue-secure-firmware-releases/tree/master/bluer11 
  - Install Protocol Buffers

```
pip install protobuf
```
  - Turn on Ledger Blue, keeping the button pressed until "secure bootloader" is displayed
  - Update the Operating System (hash 07c9d1b82709d0babe5159836d0c85f3cefd1db8328ac970e95cca9bf0ec6a3f) from the Secure Operating System update directory - the device turns off

```
python updateFirmware.py --url https://shop.hardwarewallet.com/hsm/process --perso perso_10 --firmware upgrade_bluer11 --firmwareKey upgrade_bluer11_key
```
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
  - When this is done, the device is back to the "Connect USB" screen. Finalize the firmware personalization from the Secure Operating System directory with
``` 
python refactory.py --url https://shop.hardwarewallet.com/hsm/process --perso perso_10 --persoNew perso_11
```

