# Oukitel WP5 Treble Tips

Sharing my experience with flashing a GSI on a friend's Oukitel WP5 (3GB model).



## GSIs

- (The 3GB version of) the WP5 uses GSIs in the form `system-arm32_binder64-ab.img`. For example, I used `system-roar-arm32_binder64-ab-vndklite-gapps.img`.

- If the GSI is named with `vndklite` it means the system is read-write enabled.

- I wouldn't bother with Magisk (unless it's improved since May 2021).

- phhusson's AOSP can be found at https://github.com/phhusson/treble_experimentations/releases. phhusson also has a [GSI list](https://github.com/phhusson/treble_experimentations/wiki/Generic-System-Image-(GSI)-list) if you fancy something different. If you download a `.img.xz` file, you will need to extract the `.img` file inside.

  


## Installing a GSI

- You may want to backup your stock ROM first. [This guide looks promising](https://forum.hovatek.com/thread-21970.html), but I jumped right in without backing up :worried:.

- (You will need to unlock your bootloader if you haven't already. On your device, go to Developer Options and enable OEM Unlocking. Then boot to fastboot and enter the command `fastboot flashing unlock`.)

- Boot the device to fastboot. If the device is already booted, you can use `adb reboot fastboot`. Otherwise, from a shut-down WP5, press and hold the `Vol+` and `Power` buttons. Press `Vol+` until you reach fastboot, then press `Vol-` to start.

- Enter the following commands, substituting file names where needed:
  1. system: `fastboot flash system system-arm32-ab.img`.
  2. vmbeta: `fastboot flash vbmeta patched_vbmeta.img`. Flashing the stock vbmeta like this `fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img` seems to work, but I haven't tried it.

- Reboot to recovery: Press and hold `Vol+` and `Power` like before until the screen turns black. Then release the keys for 5-10 seconds, before pressing them again to get into recovery. You will then see a "No command" prompt; to get past this, briefly press `Vol+` while pressing `Power`. If you do this right, you'll be presented with a few options. Select to wipe userdata, and then select to wipe cache. This step is important!
- Finally, reboot to system and enjoy!




## Fixing a brick with SP Flash Tool

 - Use the 9.0 firmware `Oukitel_WP5_MT6761_20200114_9.0`.
 - The 10.0 firmware `OUKITEL_WP5_EEA_10.0_V09_20201119_192903` DOES NOT BOOT! (This is the one you can get from [Oukitel's download center](https://oukitel.com/pages/download-center). I assume it's for the 4GB model?)
- You can use this tool to flash back to the stock rom. The Linux version did not work for me, so either use Windows or just flash what you need with fastboot (if you can still access fastboot). The androidmtk.com guide below claims that reflashing the preloader can brick your phone, so exercise caution.
- You can find instructions and downloads on [Oukitel's download center](https://oukitel.com/pages/download-center), or see the downloads at the end. There are also plenty of guides like this one: https://androidmtk.com/flash-stock-rom-using-smart-phone-flash-tool.
 - Make sure to also wipe userdata and cache from STOCK RECOVERY (not fastboot) or you won't get to use the full 32GB storage, or the system will tell you that decryption failed.



## Magisk

- The WP5 has no boot ramdisk, so you have to flash Magisk to the recovery partition. The official installation instructions are [here](https://topjohnwu.github.io/Magisk/install.html#magisk-in-recovery), but the long and short of it is that you patch `recovery.img` (from your firmware folder) using the Magisk app, and then install the patched recovery through fastboot.
- Everytime you want to boot with magisk, you need to press the `Vol+` and `Power` combo to boot into the recovery partition. Booting without magisk will leave you without SafetyNet if that's important to you. Like I said before, I wouldn't recommend Magisk if you don't really need it.



## Downloads

I've uploaded the files I've found as they're kinda hard to find: https://mega.nz/folder/kcszXIbK#zU8v6Gyo81ZS3y2fsHHoyQ.

- `Oukitel_WP5_MT6761_20200114_9.0.7z`, needs to be extracted. Use this with the SP Flash Tool to return to stock in case something goes wrong. This worked on my model but there's no guarantee that it'll work on yours.
- `patched_vbmeta.img` This disables verified booting (AVB). Install with `fastboot flash vbmeta patched_vbmeta.img`.
- `Software upgrade operation video tutorial.mp4`  A video guide (not by me) on how to use the SP Flash Tool with Windows.
- `SP Flash Tool.7z` The SP Flash Tool itself. Contains the Linux version (not working) and the Windows version.
