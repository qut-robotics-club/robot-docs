# Setting Up New Pi's
Designed for use with Raspberry Pi 5's.

## Imaging SD Cards

1. Download the Raspberry Pi Imager
2. Select Pi 5
3. Select 64-bit Raspbian
4. Hostname: `robots101-x`, where `x` is the robot number (eg `robots101-3` for the third bot)
5. User: `qutrc`, password `qutrc`
6. Localisation: AU wifi, Brisbane timezone, AU keyboard
7. WiFi: SSID `Robots101`, password `qutrc101`
8. SSH: Enabled, password authentication
9. Pi Connect: Disabled
10. Imaging multiple SD cards: Select new SD card, change hostname, leave remaining settings unchanged

## On-Pi Setup
Before starting, set up the Pi WiFi network as shown [here](./network-setup.md).

1. Power on Pi using either the HAT or USB-C power supply. If using a power supply, you may need to press the power button a few seconds after plugging it in for the Pi to continue booting. If the green LED is solid on after ~10s or so, press the button and it should continue booting.
2. Wait for the Pi to finish booting - it should automatically connect to the wifi network, and this will be visible in either the Unifi web console or by the connected client count on the front of the Express increasing.
3. Connect to the pi with SSH using its hostname (or IP from the console)
4. Copy the contents of the `fix-time.sh` script into the Pi's terminal:


``` console
sudo sed -i -e "s/#NTP=/NTP=pool.ntp.org/g" /etc/systemd/timesyncd.conf
sudo timedatectl set-ntp False
sudo timedatectl set-ntp True
```

This will set the Pi's clock so the next step will work.
From there:

1. Run the bootstrap script: `bash -c "$(curl https://raw.githubusercontent.com/qut-robotics-club/robot-software/refs/heads/main/setup/bootstrap.sh)"`
2. Enter password for sudo when prompted.
3. Select "n" when asked to reboot or not.
4. If the script finishes execution (indicated by it printing out instructions at the end), reboot the Pi.
5. If the display starts showing information, congratulations! The Pi is now ready to use. Note that if you had to press the power button for it to boot before, you may need to do so again. This is not required when powering from the HATs.