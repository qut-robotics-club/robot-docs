# Setting Up New Pi's
Designed for use with Raspberry Pi 5's.

## Imaging SD Cards

1. Download the Raspberry Pi Imager
2. Select Pi 5
3. Select Pi OS (64-bit)
4. Select the SD card to image
5. Configure as follows - note that all options are case-sensitive!
6. Hostname: `robots101-x`, where `x` is the robot number (eg `robots101-3` for the third bot)
7. Localisation
    - Capital city: Canberra (in older versions, Wi-Fi region AU)
    - Timezone: Brisbane (AEST)
    - Keyboard: `au`
8. User:
    - Username: `qutrc`
    - Password: `qutrc`
9. WiFi:
    - SSID: `Robots101`
    - Password/PSK: `qutrc101`
10. Remote access:
    - SSH: Enable with password authentication
    - Pi Connect: Disabled
13. Imaging multiple SD cards: Select new SD card, change hostname, leave remaining settings unchanged

## On-Pi Setup
Before starting, set up the Pi WiFi network as shown [here](./network-setup.md).

1. Power on Pi using either the HAT or USB-C power supply. If using a power supply, you may need to press the power button a few seconds after plugging it in for the Pi to continue booting. If the green LED is solid on after ~10s or so, press the button and it should continue booting.
2. If the green LED is showing a 7-flash pattern, the SD card is corrupted and must be re-imaged.
3. Wait for the Pi to finish booting - it should automatically connect to the wifi network, and this will be visible in either the Unifi web console or by the connected client count on the front of the Express increasing.
4. Connect to the pi with SSH using its hostname (or IP from the console)
5. Run the following (derived from `fix-time.sh`):


``` console
sudo sed -i -e "s/#NTP=/NTP=pool.ntp.org/g" /etc/systemd/timesyncd.conf && sudo timedatectl set-ntp False && sudo timedatectl set-ntp True
```

This will set the Pi's clock so the next step will work.
After that, run the bootstrap script:

``` console
bash -c "$(curl https://raw.githubusercontent.com/qut-robotics-club/robot-software/refs/heads/main/setup/bootstrap.sh)"
```

1. Enter password for sudo when prompted.
2. Wait for the script to finish running, which will reboot the Pi.
3. Once the Pi reboots, the display should start automatically. If it does, the Pi is all ready to go!
4. If the script fails to run, either the Pi needs to be re-imaged, or the SD card is faulty.
5.  Note that if you had to press the power button for it to boot before, you *may* need to do so again. This is not required when powering from the HATs.

## Assembly

Camera:
1. The **black** side of the cable goes towards the plastic tab