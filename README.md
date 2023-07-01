# Compiling-HailoRT-PCI-Driver-in-RK3588-SDK
Compiling HailoRT PCI Driver in RK3588 SDK

# Back to SDK and following the commands to build Hailo PCI Driver
```shell
cd SDK/kernel/driver
git clone https://github.com/hailo-ai/hailort-drivers.git
```
# or specify the version to download
```shell
git clone --depth 1 -b v4.xx.x https://github.com/hailo-ai/hailort-drivers.git
```
# Important!! confirm downloaded Hailort-Driver version
```shell
git -C hailort-drivers/ log -1  # tag: v4.xx.0 

echo "obj-y       += hailort-drivers/linux/pcie/" >> Makefile
cd ../../
./build.sh kernel
```
# check if hailo_pci.ko is built file kernel/drivers/hailort-drivers/linux/pcie/hailo_pci.ko

- Compiling HailoRT PCI Driver in SDK
![Compiling HailoRT PCI Driver in SDK](./Documents/Compiling%20HailoRT%20PCI%20Driver%20in%20SDK.jpeg)

- lspci
![lspci](./Documents/lspci.jpeg)

- HailoRT Module install
```shell
sudo mkdir /usr/lib/modules/5.10.110/kernel/drivers/hailo
sudo cp hailo_pci.ko /usr/lib/modules/5.10.110/kernel/drivers/hailo
cd ~/ && git clone https://github.com/hailo-ai/hailort-drivers.git
# must download the same version with hailo_pci.ko that we built previous slice
cd hailort-drivers/
chmod 755 download_firmware.sh && ./download_firmware.sh
sudo mkdir /lib/firmware/hailo
sudo mv hailo8_fw.4.xx.0.bin /lib/firmware/hailo/hailo8_fw.bin 
sudo cp linux/pcie/51-hailo-udev.rules /etc/udev/rules.d/
sudo depmod -a
sudo modprobe hailo_pci
sudo echo hailo_pci >> /etc/modules
# Download HailoRT deb package from hailo official developer web site
# Install HailoRT library
# !!HailoRT must be same firmware version as HailoRT-Driver
sudo dpkg -i hailort_4.xx.x_arm64.deb
sudo reboot
```
![HailoRT Module install](./Documents/pcie.jpeg)
![HailoRT Module modinfo hailo_pci](./Documents/modinfo%20hailo_pci.jpg)
[ko file download](./Documents/hailo_pci.ko)

# Contacts

- Website: www.we-signage.com
- https://we-signage.en.made-in-china.com/
- E-mail: dennis@we-signage.com
- MP/Whatsapp/Wechat: + 86 13349909990
- Skype: solled686