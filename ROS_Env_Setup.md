#ROS install
## Mac:

## Raspberry debian based:
1. Download operating system img file corresponding to board.
2. Extract img file if compressed.
3. Before writing to SD card, use `diskutil` to confirm you are writing to the right place.
4. Write img to SD card: `sudo dd if=/Path/to/img/file.img of=/dev/rdisk2 bs=1m`. 
5. If write successed, put SD card into board and boot.
6. Wireless startup auto connect configuration:

(1) use `ifconfig` to identify what wireless interface name is. (usually `wlan0`)

(2) open `/etc/network/interfaces` with proper privilege, replace `auto lo` or `auto eth0` with `auto wlan0`, and if there is no configuration about wlan0, add:
```
iface wlan0 inet dhcp
	wpa-ssid AUDATECH
	wpa-psk udifhduijhnklfdkahfdkahfkda
```
if thers is one, make it look like above.

(3) use `wpa_passphrase <ssid> <password>` to get wpa-psk

(4) "reboot" wireless interface:
```
sudo ifdown wlan0
sudo ifup wlan0
```