# Linksys WRT 1900 ACS with Huawei E3372 Hi-Link LTE Dongle

## Linksys WRT 1900 ACS OpenWRT Firmware

[Linksys WRT 1900 ACS OpenWRT Firmware](https://openwrt.org/toh/views/toh_fwdownload?dataflt%5BModel*%7E%5D=wrt1900acs)

## Default openWRT Admin Interface

[http://192.168.1.1](http://192.168.1.1)

## Plug in Huawei E3372 Hi-Link LTE Dongle

Plug Huawei E3372 Hi-Link LTE Dongle in to USB1

## Huawei E3372 Hi-Link LTE Dongle Support and Optional Packages

[Using the Huawei E3372 Hi-Link LTE Dongle with OpenWRT](https://protyposis.net/blog/using-the-huawei-e3372-hi-link-lte-dongle-with-openwrt)

Install:

1. Huawei E3372 Hi-Link LTE Dongle: kmod-usb-net-cdc-ether usb-modeswitch
2. Mosquitto: mosquitto-nossl
3. Material Theme: luci-theme-material

I like luci-theme-material

```bash
opkg update && opkg install luci-theme-material mosquitto-nossl kmod-usb-net-cdc-ether usb-modeswitch nano git

```

## Update Existing Packages

```bash
opkg list-upgradable | cut -f 1 -d ' ' | xargs opkg upgrade
```

## Configure Huawei E3372 Hi-Link LTE Dongle

From Network -> Interfaces -> Add New Interface

- Name of new interface: Dongle
- Protocol: DHCP Client
- Cover the following interface: eth2

From Network -> Interfaces -> Edit Dongle -> Firewall Settings

- Add Dongle to **wan** group

## Setting WAN Priority

Generally want to use Broadband first then fall back to LTE Dongle. This is done by setting a gateway metric - low numbers = highest priority

Network -> Interfaces -> WAN -> Advanced Settings

- Use gateway metric: 10

Network -> Interfaces -> Dongle -> Advanced Settings

- Use gateway metric: 20

## Activate Huawei E3372 Hi-Link LTE Dongle

1. Ensure dongle is activated with the SIM Carrier
2. On Dongle Teal light will glow solidly (no blink)
3. You may need to disconnect Internet/Broadband connection and reboot
4. Try **Stopping** and **Connecting** the Dongle Interface
5. Eventually Dongle will provide a DHCP address to the router

    Similar to the following:

    ```text
    Protocol: DHCP client
    Uptime: 0h 15m 11s
    MAC: 0C:5B:8F:27:9A:64
    RX: 28.90 MB (21750 Pkts.)
    TX: 1.22 MB (11751 Pkts.)
    IPv4: 192.168.8.100/24
    ```

## Admin Interface for the Huawei E3372 Hi-Link LTE Dongle

[http://192.168.8.1](http://192.168.8.1)

### Find Data Usage for Dongle (on Optus Australia)

1. From Dongle Admin interface, select SMS
2. Text 1 to 9999
3. Review information in the reply

## Auto Mounting a USB Flash Drive

[Quick Start for Adding a USB drive](https://openwrt.org/docs/guide-user/storage/usb-drives-quickstart)

[Using storage devices](https://openwrt.org/docs/guide-user/storage/usb-drives)

```bash
opkg update && opkg install e2fsprogs kmod-usb-storage kmod-usb2 kmod-usb3 kmod-usb-storage-uas usbutils gdisk block-mount f2fs-tools kmod-fs-f2fs
```

## Very Secure FTP Server (vsftpd) with Anonymous Access

[Very Secure FTP Server](https://openwrt.org/docs/guide-user/services/nas/ftp.overview)

Install:

```bash
opkg update && opkg install vsftpd
```

nano ***/etc/vsftpd.conf***

replace existing contents with thg following

```text
background=YES
listen=YES
anonymous_enable=YES
ftp_username=nobody
anon_root=/mnt/sda1/lab
no_anon_password=YES
local_enable=NO
write_enable=NO
local_umask=022
check_shell=NO
dirmessage_enable=YES
ftpd_banner=Welcome to Glovebox FTP service.
session_support=NO
#syslog_enable=YES
#userlist_enable=YES
#userlist_deny=NO
#userlist_file=/etc/vsftpd/vsftpd.users
#xferlog_enable=YES
#xferlog_file=/var/log/vsftpd.log
#xferlog_std_format=YES
###
### TLS/SSL options
### example key generation: openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/vsftpd/vsftpd_privkey.pem -out /etc/vsftpd/vsftpd_cert.pem -subj >
#ssl_enable=YES
#allow_anon_ssl=NO
#force_local_data_ssl=NO
#force_local_logins_ssl=NO
#ssl_tlsv1=YES
#ssl_sslv2=NO
#ssl_sslv3=NO
#rsa_cert_file=/etc/vsftpd/vsftpd_cert.pem
#rsa_private_key_file=/etc/vsftpd/vsftpd_privkey.pem

#local_root=/mnt/sda1/lab
```

### Reload and Start Very Secure FTP Services

```bash
/etc/init.d/vsftpd reload
/etc/init.d/vsftpd start
```

## Install wget

```bash
opkg update && opkg install wget libustream-openssl ca-bundle ca-certificates
```

### wget Visual Studio Code Insider Builds

```bash
wget https://go.microsoft.com/fwlink/?LinkID=760865  # .deb64
wget https://go.microsoft.com/fwlink/?LinkId=723966  # macOS
wget https://aka.ms/win32-x64-user-insider           # Windows 64
```

## GitHub

Note: use **git:** rather than **https:** transport

```bash
git clone --depth 1 git://github.com/gloveboxes/PyCon-Hands-on-Lab.git
```

## Python3

```bash
python3 -m pip install ...
```

### CPU Temperature

```bash
cat /sys/class/thermal/thermal_zone0/temp 
```
