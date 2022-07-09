# Booting from LUKS-encrypted btrfs root using Refind
1. Install refind: `apt install refind`
2. Copy refind to ESP and add entry to fwmgr: `refind-install`. No additional drivers are needed, because the kernel will be in unencrypted ESP partition.
3. Make `/boot/refind_linux.conf`. UUID is of the raw partition (for example `/dev/nvme0n1p2`).
```
"Boot with standard options"  "rootfstype=btrfs cryptdevice=UUID=xxxxxx:cryptdata:allow-discards rd.luks.options=discard root=/dev/mapper/cryptdata rootflags=subvol=@ quiet splash"
```
`allow-discards` and `discard` is for TRIM support.
4. Also add `discard` to `/etc/crypttab`:
```
cryptdata UUID=xxxxxxx none luks,discard
```
5. After each initramfs or kernel update, copy files from /boot to ESP:
```
sudo cp -rx /boot/ /boot/efi/EFI/ubuntu-boot
```