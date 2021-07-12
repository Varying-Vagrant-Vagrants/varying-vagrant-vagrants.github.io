---
category: 5. Troubleshooting
order: 9
title: VirtualBox
description: VirtualBox installation issues.
permalink: /docs/en-US/troubleshooting/virtualbox
---

## Updating to MacOS Big Sur or Newer

You need to update to a newer version of VirtualBox. Download the latest version of VirtualBox and install it.

## Apple Silicon

VirtualBox does not support Apple Silicon, you will need to find an alternative provider. We currently do not have hardware to test this, and there are no recommended providers. We may provide docker as a provider in the future, but there is no timeframe on this. When we do, we will announce it, so if you don't see documentation for Docker, then it is not supported or usable. We do however want help with this!

## VirtualBox Installer/Update Failing on MacOS

When installing VirtualBox, MacOS should present a security window asking if you want to allow the installation of kernel extensions. Sometimes this does not happen and the installer fails instead.

There are several solutions which work for different situations:

 - The security pane in System preferences
 - Restarting your computer
 - Clearing staged kernel extensions

After each of these, run the uninstaller if updating, and re-run the VirtualBox installer. Always use the latest version of VirtualBox that you can.

_Note:  Vagrant and VirtualBox are different pieces of software. You do not have to reinstall Vagrant or VVV to upgradee VirtualBox._

### The Security & Privacy Pane in System Preferences

After the installer fails, close the installer and head to the system preferences app. Then, open the Security & Privacy settings. There should be a message in that window about Oracle with an Allow button. Click this button, restart the machine, and run the VirtualBox installer again.

### Restarting your computer

Turning your Mac off and on again with a hard reboot can solve lots of problems related to VirtualBox installations.

### Clearing staged kernel extensions

Sometimes the installer can't add the necessary kernel extensions due to a prior failed install.

1. Uninstall VirtualBox with the uninstall tool found in the dmg
2. Restore SIP to default: `sudo csrutil clear`
3. Reboot
4. Clear staging: `sudo kextcache --clear-staging`
5. Reboot
6. Install VirtualBox and follow system prompt to allow Oracle

### Accepting Oracle Extensions Manually in Recovery Mode

Restart your Mac into recovery mode, and run this command in the terminal:

```shell
sudo /usr/sbin/spctl kext-consent add VB5E2TV963
```

This command will only work in recovery mode. If it responds with `spctl: failed to store new configuration.` then you are not in recovery mode.

After doing this, reboot back into normal mode and re-run the VirtualBox installer.

### Helpful Commands for MacOS

You can run this command on MacOS to confirm if the VirtualBox kernel extensions are loaded:

```shell
sudo kextstat | grep -i virtualbox
```

For example, here is what success might look like:

```shell
❯ sudo kextstat | grep -i virtualbox
Password:
Executing: /usr/bin/kmutil showloaded
No variant specified, falling back to release
  178    3 0xffffff7fa2326000 0xb2000    0xb2000    org.virtualbox.kext.VBoxDrv (6.1.16) DAF044F0-5043-3B8E-8758-5A462567BDAA <8 6 5 3 1>
  183    0 0xffffff7fa2403000 0x5000     0x5000     org.virtualbox.kext.VBoxUSB (6.1.16) CA33FA52-5933-3F0E-9B40-8B1ECF4D6A36 <182 178 66 8 6 5 3 1>
  184    0 0xffffff7fa23fe000 0x4000     0x4000     org.virtualbox.kext.VBoxNetFlt (6.1.16) C93EAF6A-676F-3370-BAE2-BDFD2BF16582 <178 8 6 5 3 1>
  185    0 0xffffff7fa23f8000 0x2000     0x2000     org.virtualbox.kext.VBoxNetAdp (6.1.16) 76200407-D2F0-3D84-BCCF-7EEA18F16654 <178 6 5 1>
```

If no Virtualbox kernel extensions are loaded it will look like this:

```shell
❯ sudo kextstat | grep -i virtualbox
Executing: /usr/bin/kmutil showloaded
No variant specified, falling back to release
```

## Corrupted Virtual Machines

It's possible but rare that the Virtual Machine file system can become corrupted. This might happen if your VM didn't shut down correctly, perhaps there was a power cut or your laptop ran out of power unexpectedly.

In this scenario, your files should be safe on the host filesystem. If you have run `vagrant halt` recently, a database backup will be available. Using these, the site can be recovered from a fresh VVV box.

Follow the [starting from fresh](#starting-from-fresh) instructions at the top of this document to recover.

For more information on backups, see the [backups](#backups) section below.

### VirtualBox Cleanup Issues When Destroying and Recreating VVV

If your `vagrant up --provision` fails with an error like this:

```
VirtualBox error:

VBoxManage.exe: error: Could not rename the directory 'C:\Users\<username>\VirtualBox VMs\ubuntu-cloudimg-trusty-vagrant-amd64_1534242157844_99798' to 'C:\Users\<username>\VirtualBox VMs\localdev_306449ed646' to save the settings file (VERR_ALREADY_EXISTS)
VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component SessionMachine, interface IMachine, callee IUnknown
VBoxManage.exe: error: Context: "SaveSettings()" at line 3111 of file VBoxManageModifyVM.cpp
```

Then the `vagrant destroy` command didn't manage to clean things up properly.

The default location for these files is:

 - Windows: `C:\Users\<username>\VirtualBox VMs`
 - Mac/*nix: `~/VirtualBox VMs`

Delete the folder name that matches the path in error above. In the example aboves case it would look **similar** to this:

    ....VirtualBox VMs\localdev_306449ed646\

Then go back and run `vagrant up --provision` again.
