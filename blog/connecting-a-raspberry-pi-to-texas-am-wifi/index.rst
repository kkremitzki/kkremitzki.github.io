.. title: Connecting a Raspberry Pi to Texas A&M Wifi via Command Line
.. slug: connecting-a-raspberry-pi-to-texas-am-wifi
.. date: 2016-04-21 18:46:17 UTC-05:00
.. tags: linux,raspberry_pi
.. category: 
.. link: 
.. description: 
.. type: text

The recommended flavor of Linux on the Raspberry Pi, Raspbian, uses the LXDE desktop environment, and using its GUI tools to set up wifi is not immediately successful.
Command-line setup involves editing two files, ``/etc/network/interfaces`` and ``/etc/wpa_supplicant/wpa_supplicant.conf``. Since these are system files, they won't be writable by a normal user. The command ``sudo -e <filename>`` can be used to edit system files with superuser privileges, using the default editor. Normally, this is the program ``nano``, which is fairly self-explanatory; make your changes using the keyboard and save the file with ``Ctrl-X``. For advanced users, this can be changed via something like ``export EDITOR=vi``.

The first file, ``/etc/network/interfaces``, needs to have the following:

.. TEASER_END

.. code-block:: bash

  allow-hotplug wlan0
  iface wlan0 inet dhcp
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

The ``allow-hotplug`` line allows the ``wlan0`` (wireless LAN) interface to be brought up when hotplugged into a running Raspberry Pi.
The ``iface ... dhcp`` line means we are requesting an IP address from the wireless network's DHCP servers, and the ``wpa-conf`` line specifies which file to use for our auth config.

In ``/etc/wpa_supplicant/wpa_supplicant.conf``, you should have:

.. code-block:: bash
  
  network={
       ssid=”tamulink-wpa”
       scan_ssid=1
       key_mgmt=WPA-EAP
       eap=PEAP
       identity=”YOUR_NET_ID”
       password=”YOUR_TAMU_PASSWORD”
       pairwise=CCMP
  }

Make sure that there is no space in ``network={``, and that the ssid, identity and passwords are wrapped in quotes.

The network can be brought up or down via ``sudo ifup wlan0`` or ``sudo ifdown wlan0``.

As a final note, be mindful of the fact that doing this leaves your TAMU password on an unencrypted device; anyone with the know-how could take an SD card with these credentials and read them. Don't neglect the physical security of your Raspberry Pi after doing this, since it will contain important information.
