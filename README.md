# Pi.Alert
<!--- --------------------------------------------------------------------- --->

WIFI / LAN intruder detector.

Scan the devices connected to your WIFI / LAN and alert you the connection of
unknown devices. It also warns if a "always connected" device disconnects.

![Main screen][main]
*(Apologies for my English and my limited knowledge of Python, php and
JavaScript)*

## Modifications within this Fork
  - Only one scan cycle
  - Modified scanmethod. If you want to go back to the original method comment line 505 and uncomment line 508 in ~/pialert/back/pialert.py
  - Because of the modified scan, the extended scan parameters in the configuration file do not work. For this reason they were removed. 
  - The Backend has the additional option "cleanup"
  - "pialert-cli" that helps to configure login, password and DB migration

## How it works
The system continuously scans the network for:
  - New devices
  - New connections (re-connections)
  - Disconnections
  - "Always Connected" devices down
  - Devices IP changes
  - Internet IP address changes

## Scan Methods
Up to three scanning methods are used:
  - **Method 1: arp-scan**. The arp-scan system utility is used to search
        for devices on the network using arp frames.
  - **Method 2: Pi-hole**. This method is optional and complementary to
        method 1. If the Pi-hole DNS server is active, Pi.Alert examines its
        activity looking for active devices using DNS that have not been
        detected by method 1.
  - **Method 3. dnsmasq**. This method is optional and complementary to the
        previous methods. If the DHCP server dnsmasq is active, Pi.Alert
        examines the DHCP leases (addresses assigned) to find active devices
        that were not discovered by the other methods.

## Components
The system consists of two parts:

### Back
In charge of:
  - Scan the network searching connected devices using the scanning methods
    described
  - Store the information in the DB
  - Report the changes detected by e-mail and/or other services (Pushsafer, NTFY, Gotify)
  - DB cleanup tasks via cron
  - a pialert-cli that helps to configure login and password

  | ![Report 1][report1] | ![Report 2][report2] |
  | -------------------- | -------------------- |

### Front
There is a configurable login to prevent unauthorized use. The default password is "123456". By default, this is disabled. If you want to use password protection, enable it in the configuration file ~/pialert/config/pialert.conf or via pialert-cli.

A web frontend that allows:
  - Manage the devices inventory and the characteristics
  - Display in a visual way all the information collected by the back
    - Sessions
    - Connected devices
    - Favorites
    - Events
    - Presence
    - Concurrent devices
    - Down alerts
    - IP's
    - ...
  - Manual Nmap scans
  - Speedtest for Device "Internet" in the details view
  - Simple Network relationship display
  - Maintenance tasks and Settings like:
    - Status Infos (active scans, database size, backup counter)
    - Theme Selection (blue, red, green, yellow, black, purple)
    - Language Selection (english, german, spanish)
    - Light/Dark-Mode Switch
    - Pause arp-scan
    - DB maintenance tools
    - DB Backup and Restore
  - Help/FAQ Section 

  | ![Screen 1][screen1] | ![Screen 2][screen2] |
  | -------------------- | -------------------- |
  | ![Screen 3][screen3] | ![Screen 4][screen4] |

![Maintain screen dark][maintain_dark]

# Installation
<!--- --------------------------------------------------------------------- --->
Initially designed to run on a Raspberry Pi, probably it can run on many other
Linux distributions.

- One-step Automated Install:
  #### `curl -sSL https://github.com/leiweibau/Pi.Alert/raw/main/install/pialert_install.sh | bash`

- [Installation Guide (step by step)](docs/INSTALL.md)


# Uninstall process
<!--- --------------------------------------------------------------------- --->
  - [Unistall process](docs/UNINSTALL.md)


# Device Management
<!--- --------------------------------------------------------------------- --->
  - [Device Management instructions](docs/DEVICE_MANAGEMENT.md)


## Other useful info
<!--- --------------------------------------------------------------------- --->

### [Versions History](docs/VERSIONS_HISTORY.md)

### Powered by:
  | Product       | Objetive                                                |
  | ------------- | ------------------------------------------------------- |
  | Python        | Programming language for the Back                       |
  | PHP           | Programming language for the Front-end                  |
  | JavaScript    | Programming language for the Front-end                  |
  | Bootstrap     | Front-end framework                                     |
  | Admin.LTE     | Bootstrap template                                      |
  | FullCalendar  | Calendar component                                      |
  | Sqlite        | DB engine                                               |
  | Lighttpd      | Webserver                                               |
  | arp-scan      | Scan network using arp commands                         |
  | Pi.hole       | DNS Server with Ad-block                                |
  | dnsmasq       | DHCP Server                                             |
  | nmap          | Network Scanner                                         |
  | zip           | Filecompression Tool                                    |
  | speedtest-cli | Python SpeedTest https://github.com/sivel/speedtest-cli |

### License
  GPL 3.0
  [Read more here](LICENSE.txt)

  Source of the animated GIF (Loading Animation)
  https://commons.wikimedia.org/wiki/File:Loading_Animation.gif
  
  Source of the selfhosted Fonts
  https://github.com/adobe-fonts/source-sans

### Contact
  pi.alert.application@gmail.com
  
  ***Suggestions and comments are welcome***

### Special thanks 🥇

  This code is a collaborative body of work, with special thanks to: 

   - [leiweibau](https://github.com/leiweibau/Pi.Alert): Things
   - [Macleykun](https://github.com/Macleykun): Help with Dockerfile clean-up
   - [Final-Hawk](https://github.com/Final-Hawk): Help with NTFY, styling and other fixes
   - [TeroRERO](https://github.com/terorero): Spanish translation
   - [jokob-sk](https://github.com/jokob-sk/Pi.Alert): Many more things

<!--- --------------------------------------------------------------------- --->
[main]:    ./docs/img/1_devices.jpg           "Main screen"
[screen1]: ./docs/img/2_1_device_details.jpg  "Screen 1"
[screen2]: ./docs/img/2_2_device_sessions.jpg "Screen 2"
[screen3]: ./docs/img/2_3_device_presence.jpg "Screen 3"
[screen4]: ./docs/img/3_presence.jpg          "Screen 4"
[report1]: ./docs/img/4_report_1.jpg          "Report sample 1"
[report2]: ./docs/img/4_report_2.jpg          "Report sample 2"
[maintain_dark]: /docs/img/5_maintain.jpg     "Maintain screen dark"

