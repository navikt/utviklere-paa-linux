## How do I connect to the "NAV" Wi-Fi at Fyrstikkallèen 1?
Fill in the information as shown in the screenshot below:![wifi.png](wifi.png)


## How do I print from FA1?
https://github.com/navikt/ny-i-nav/blob/main/ny-unix.md#skrive-ut
https://github.com/navikt/ny-i-nav/blob/main/add_nav_printers.sh


## Where can I find other useful resources?
https://navikt.github.io/ny-i-nav/ny-unix


## How do I set up Ubuntu on a Lenovo ThinkPad P16s G4?
UEFI BIOS Version: R2XET35W (1.15)
This unit comes without an operating system installed.
Before you begin:

- Have a USB flash drive ready containing the latest Ubuntu LTS (the Service Desk can lend out empty USB drives).

Før man installerer Linux på laptopen så må man enable SecureBoot:

> [!CAUTION]
> Before installing Linux on the laptop, you must enable Secure Boot:

Steps:
1. Turn on the machine
2. Press ENTER to interrupt startup (Lenovo logo)
3. Press F1 to enter the BIOS Setup Utility
4. Go to the Security menu :arrow_right: Secure Boot (see image)
   ![secureboot.jpg](secureboot.jpg)
    1. Set Secure Boot (On)
    2. Set Allow Microsoft 3rd Party UEFI CA (On)
    3. Select Exit Deployed Mode (Secure Boot Mode should be User Mode)


5. Tast F10 Save and Exit
6. Insert the flash drive containing the latest Ubuntu LTS and boot the computer from it.
7. During Ubuntu setup, select Try Ubuntu.
8. Press CTRL+ALT+T to open Terminal
9. Verifiser at SecureBoot er enabled:
```
ubuntu@ubuntu:~$ sudo mokutil --sb-state 
SecureBoot enabled
```
10. Start Ubuntu installation
11. Installer Ubuntu med Full disk encryption [FDE] (https://documentation.ubuntu.com/security/security-features/storage/encryption-full-disk/)
    1. "Encrypt with passphrase" suitable for most people
    2. "Use hardware-backed encryption"[hardware-backed-disk-encryption](https://ubuntu.com/desktop/docs/en/latest/explanation/hardware-backed-disk-encryption/) if you manage to get it working
12. Go through the other steps
13. Once the Ubuntu installation is complete and the machine has been restarted, verify that Secure Boot is enabled in the Terminal:
```
bruker@maskin:~$ sudo dmesg | grep -i secureboot
[sudo: authenticate] Password: 
[    0.000000] secureboot: Secure boot enabled
[    0.003709] secureboot: Secure boot enabled
```
14. Install naisdevice and check that Kolide is satisfied: https://doc.nais.io/operate/naisdevice/how-to/install/
15. Connect to naisdevice. You should now have access to NAV resources on Ubuntu.
16. Verify Outlook works: https://outlook.office365.com/mail/

