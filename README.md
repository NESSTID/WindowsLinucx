[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#table-of-contents)

### Prerequisites
- Ensure you have `qemu-kvm` installed.
- Have sufficient disk space (at least 60GB) for the VM.

### Run the following commands ( Use Codespace ) :

```bash
cd /tmp && sudo rm -r * && clear
```
```bash
wget -O win.iso "https://releases.ubuntu.com/24.04.1/ubuntu-24.04.1-desktop-amd64.iso"
```
```bash
wget https://github.com/NESSTID/WindowsLinucx/raw/refs/heads/main/bios64.bin
```
```bash
sudo apt update -y
```
```bash
sudo apt install qemu-kvm -y
```
```bash
qemu-img create -f raw win.img 90G
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
sudo apt install playit -y
```
