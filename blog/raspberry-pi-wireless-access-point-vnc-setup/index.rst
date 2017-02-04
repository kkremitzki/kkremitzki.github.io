.. title: Raspberry Pi Wireless Access Point & VNC Setup
.. slug: raspberry-pi-wireless-access-point-vnc-setup
.. date: 2026-05-05 05:24:34 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

sudo apt-get install tightvncserver hostapd isc-dhcp-server

file: /etc/dhcp/dhcpd.conf

subnet 10.10.0.0 netmask 255.255.255.0 {
range 10.10.0.25 10.10.0.50;
option domain-name-servers 8.8.4.4;
option routers 10.10.0.1;
interface wlan0;
}

file: /etc/network/interfaces
  allow-hotplug wlan0
  iface wlan0 inet static
  address 10.10.0.1
  netmask 255.255.255.0

file: /etc/hostapd/hostapd.conf
  interface=wlan0
  ssid=STATION_NAME
  hw_mode=g
  channel=11
  wpa=1
  wpa_passphrase=PASSWORD
  wpa_key_mgmt=WPA-PSK
  wpa_pairwise=TKIP CCMP
  wpa_ptk_rekey=600
  macaddr_acl=0

ffile: /etc/init.d/hostapd
  DAEMON_CONF="/etc/hostapd/hostapd.conf"

create password with vncpasswd

file: /etc/systemd/system/vncserver@:1.service
  [Unit]
  Description=Remote desktop service (VNC)
  After=syslog.target network.target

  [Service]
  Type=forking
  User=pi
  PAMName=login
  PIDFile=/home/pi/.vnc/%H:%i.pid
  ExecStartPre=-/usr/bin/vncserver -kill :%i > /dev/null 2>&1
  ExecStart=/usr/bin/vncserver -depth 24 -geometry 1280x800 :%i
  ExecStop=/usr/bin/vncserver -kill :%i

  [Install]
  WantedBy=multi-user.target

sudo systemctl enable vncserver@:1
