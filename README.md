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

```
opkg update && opkg install luci-theme-material mosquitto-nossl kmod-usb-net-cdc-ether usb-modeswitch

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
4. Try Restarting the Dongle Interface
5. Eventually Dongle will provide a DHCP address to the router

    Similar to the following:

        Protocol: DHCP client
        Uptime: 0h 15m 11s
        MAC: 0C:5B:8F:27:9A:64
        RX: 28.90 MB (21750 Pkts.)
        TX: 1.22 MB (11751 Pkts.)
        IPv4: 192.168.8.100/24

## Admin Interface for the Huawei E3372 Hi-Link LTE Dongle

[http://192.168.8.1](http://192.168.8.1)

### Find Data Usage for Dongle (on Optus Australia)

1. From Dongle Admin interface, select SMS
2. Text 1 to 9999
3. Review information in the reply
