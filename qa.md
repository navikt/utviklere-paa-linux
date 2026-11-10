## How do I connect to the "NAV" Wi-Fi at Fyrstikkallèen 1?
Fill in the information as shown in the screenshot below:![wifi.png](wifi.png)


## How do I print from Fyrstikkallèen 1?
https://github.com/navikt/ny-i-nav/blob/main/ny-unix.md#skrive-ut
https://github.com/navikt/ny-i-nav/blob/main/add_nav_printers.sh


## Where can I find other useful resources?
https://navikt.github.io/ny-i-nav/ny-unix


## How do I set up Ubuntu on a Lenovo ThinkPad P16s G4?
UEFI BIOS Version: R2XET35W (1.15)
This unit comes without an operating system installed.
Before you begin:

- Have a USB flash drive ready containing the latest Ubuntu LTS (the Service Desk at Fyrstikkallèen 1 can lend out empty USB drives).

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
9. Verify that SecureBoot is enabled:
```
ubuntu@ubuntu:~$ sudo mokutil --sb-state 
SecureBoot enabled
```
10. Start Ubuntu installation
11. Install Ubuntu with full disk encryption [FDE] (https://documentation.ubuntu.com/security/security-features/storage/encryption-full-disk/)
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
15. Connect to naisdevice. You should now have access to Nav resources on Ubuntu.
16. Verify Outlook works: https://outlook.office365.com/mail/


## Zoom repo for easier installation/update
```
# 0. prereqs
sudo apt-get install ca-certificates curl apt-transport-https gnupg

# 1. add repo signing key
curl -sfSL "https://europe-north1-apt.pkg.dev/doc/repo-signing-key.gpg" | sudo dd of="/etc/apt/keyrings/nais-ppa-zoom.asc"

# 2. add repository
echo "deb [signed-by=/etc/apt/keyrings/nais-ppa-zoom.asc] https://europe-north1-apt.pkg.dev/projects/nais-ppa zoom main" | sudo tee /etc/apt/sources.list.d/nais-ppa-zoom.list

# 3. update repo
sudo apt update

# 4. install zoom
sudo apt install zoom
```