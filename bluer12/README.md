# Official Non Secure firmware images for Ledger Blue, version 1.2

This directory contains the deterministic hex files and signed image of the non secure (STM32) firmware images for Ledger Blue 

This release also includes a Secure Operating System update. 

To install it, proceed as follows : 

  - Make sure to install the Python loader application from https://github.com/LedgerHQ/blue-loader-python (latest version or release 1.2) and operate in the same Python virtual environment
  - Check out the Secure Operating System update from https://github.com/LedgerHQ/blue-secure-firmware-releases/tree/master/bluer12 
  - Install Protocol Buffers
  - Install update 1.1 following instructions on https://github.com/LedgerHQ/blue-nonsecure-firmware-releases/tree/master/bluer11 if not done already

```
pip install protobuf
```
  - Turn on Ledger Blue, keeping the button pressed until "secure bootloader" is displayed
  - Update the Operating System (hash a678156396388945ea9fc188008ac922f0944315565e44f6733d1bbbfbc7c626) from the Secure Operating System update directory - the device turns off

```
python updateFirmware.py --url https://hsmprod.hardwarewallet.com/hsm/process --perso perso_11 --firmware upgrade_bluer12 --firmwareKey upgrade_bluer12_key --targetId=0x31000002
```
  - Turn on Ledger Blue, keeping the button pressed until "secure bootloader", then "bootloader" is displayed
  - Update the bootloader with the following command. Following the update, the script displays an error and the device turns off

``` 
 python -m ledgerblue.loadMCU --targetId 0x04000001 --fileName bootloader/stm32l476_blue_bootloader_upgrade.hex --bootAddr 0x08013188 
```
  - Turn on Ledger Blue, the device displays "Upgrading Bootloader", then turns off
  - Turn on Ledger Blue
  - Update the firmware with the following command 

```
 python -m ledgerblue.loadMCU --targetId 0x04000001 --fileName main/stm32l476_seproxyhal.loadable.hex --bootAddr 0x08011988 
```

