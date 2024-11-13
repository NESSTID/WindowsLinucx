[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#table-of-contents)

## Setting up a Windows VM using QEMU
<p align="center">
    <img src="https://raw.githubusercontent.com/NeofetchNpc/bios-windows/refs/heads/main/media/8731aff209e78665c65cafbf51a9c00e.jpg" width="100%" style="margin-left: auto;margin-right: auto;display: block;">
</p>

> Run Sh as usual and don't forget to change the config.json!
> 
> With this you can run Windows on Linux, Ubuntu, Debian and so on
> 
> Exemple iso "https://go.microsoft.com/fwlink/?linkid=2270353&clcid=0x409&culture=en-us&country=us" Windows 11 Ltsc
>
> Don't use this script for anything illegal! 

### Prerequisites
- Ensure you have `qemu-kvm` installed.
- Have sufficient disk space (at least 60GB) for the VM.

### Run the following commands ( Use Codespace ) :

```bash
cd /tmp && sudo rm -r * && clear
```
```bash
wget -O win.iso "https://go.microsoft.com/fwlink/?linkid=2270353&clcid=0x409&culture=en-us&country=us"
```
```bash
wget https://github.com/HindiaFtNpc/WindowsLinucx/raw/main/bios64.bin
```
```bash
sudo apt update
```
```bash
sudo apt install qemu-kvm -y
```
```bash
qemu-img create -f raw win.img 60G
```
```bash
sudo qemu-system-x86_64 -m 8G -smp 4 -cpu host -boot order=c -drive file=win.iso,media=cdrom -drive file=win.img,format=raw -device usb-ehci,id=usb,bus=pci.0,addr=0x4 -device usb-tablet -vnc :0 -smp cores=4 -device e1000,netdev=n0 -netdev user,id=n0 -vga qxl -accel kvm -bios bios64.bin
```
```bash
curl -SsL https://playit-cloud.github.io/ppa/key.gpg | gpg --dearmor | \
sudo tee /etc/apt/trusted.gpg.d/playit.gpg >/dev/null
echo "deb [signed-by=/etc/apt/trusted.gpg.d/playit.gpg] \
https://playit-cloud.github.io/ppa/data ./" | sudo tee \
/etc/apt/sources.list.d/playit-cloud.list
sudo apt update
sudo apt install playit
```
