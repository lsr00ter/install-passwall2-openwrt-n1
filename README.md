# Install PassWall2 on Phicomm N1 OpenWrt router (AArch64 : Cortex-A53)
[فارسی](https://github.com/Ramtiiin/iran-ip/blob/main/README.fa.md)

⚠️ This configuration has been tested on a Phicomm N1 running OpenWrt version ImmortalWrt 24.10-SNAPSHOT r33004-bca880a0e8. Ensure that your router has **at least 128MB of storage** before executing these commands. ⚠️

## 1. Initial Settings

### Configuring IP Address, WiFi, and Password

Read more about [OpenWrt initial settings](https://github.com/Ramtiiin/Install-PassWall-OpenWrt/blob/main/Openwrt-initial-setting.md).

## 2. Install Passwall

### SSH into the Router

1. Open your terminal (or SSH client) and connect to the router:
   ```sh
   ssh root@192.168.1.1

2. Update the package list:
   ```sh
   opkg update

3. Remove the default dnsmasq and install dnsmasq-full:
   ```sh
   opkg remove dnsmasq
   opkg install dnsmasq-full

4. Install required kernel modules if not installed:
   ```sh
   opkg install kmod-nft-tproxy kmod-nft-socket
   
5. Download and add the Passwall public key:
   ```sh
   wget -O passwall.pub https://master.dl.sourceforge.net/project/openwrt-passwall-build/passwall.pub
   opkg-key add passwall.pub

6. Set up custom feeds for Passwall:
```sh
   release=24.10
   arch=aarch64_cortex-a53

   for feed in passwall_packages passwall2; do
     echo "src/gz $feed https://master.dl.sourceforge.net/project/openwrt-passwall-build/releases/packages-$release/$arch/$feed" >> /etc/opkg/customfeeds.conf
   done
```

7. Update the package list again to include Passwall feeds:
   ```sh
   opkg update

8. Install luci-app-passwall2 and v2ray-geosite-ir:
   ```sh
   opkg install luci-app-passwall2 v2ray-geosite-ir
   
