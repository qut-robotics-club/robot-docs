# Setting Up New Pi's
Designed for use with Raspberry Pi 5's.

## Imaging SD Cards

1. Download the Raspberry Pi Imager
2. Select Pi 5
3. Select 64-bit Raspbian
4. Hostname: `robots101-x`, where `x` is the robot number (eg `robots101-3` for the third bot)
5. User: `qutrc`, `qutrc`
6. Localisation: AU wifi, Brisbane timezone, AU keyboard
7. WiFi: `Robots101`, `qutrc101`
8. SSH: Enabled, password
9. Pi Connect: Disabled
10. Imaging multiple SD cards: Select new SD card, change hostname, leave remaining settings unchanged

## On-Pi Setup
1. [Set up Pi network](./network-setup.md)
2. Power on Pi
3. Connect to the pi using its hostname
4. Copy the contents of the `fix-time.sh` script into the Pi's terminal:
    ```console
    sudo sed -i -e "s/#NTP=/NTP=pool.ntp.org/g" /etc/systemd/timesyncd.conf
    sudo timedatectl set-ntp False
    sudo timedatectl set-ntp True
    ```
5. Run the bootstrap script: (curl instructions here): `bash -c "$(curl https://raw.githubusercontent.com/qut-robotics-club/robot-software/refs/heads/main/setup/bootstrap.sh)"`