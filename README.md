# NTP + Timezone

Configuration in `/etc/config/system`

Change ntp server from default chinese server to ntp.cloudflare.com or any other [NTP server](https://gist.github.com/mutin-sa/eea1c396b1e610a2da1e5550d94b0453)

change timezone: Delete timezone line and edit zonename line

[TZ names](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)

Example for Europe/Berlin:

```
config system
        option hostname TinaLinux
        option zonename Europe/Berlin 
        option log_file /tmp/.lastlog
        option log_size 512
        option log_buffer_size 64

config timeserver ntp
        list server time.cloudflare.com
        option enable 1
        option enable_server 0
```
# Serial / MAC address

The device has a random mac address on every boot by default. This gets annoying because DHCP servers will assign a new IP every boot.

To fix this, we add a startup script:

# Startup script

On boot, `/usr/trimui/bin/runtrimui.sh` is executed, which in turn executes every script in `SD/System/starts/`  
To get a consistent mac address and thus IP address, we change the mac on boot:

On the SD card, create the file `System/starts/mac.sh`. Capitalizaton matters.

Content of the script. change mac address to what you want it to be (or leave it as it is).

```
#!/bin/sh

ifconfig wlan0 down                        
ifconfig wlan0 hw ether 00:00:d3:4d:b3:3f
ifconfig wlan0 up
```