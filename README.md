* Run `vagrant up` and wait a few seconds for the VM to boot, but vagrant will be stuck at the message `WinRM transport: plaintext`
* Once the machine boots up for the first time choose "home" or "work" network and allow it to reboot.
* After 1st reboot, make sure that you remove any other networks that you may have, typically vagrant boots up with 2 networks, allow it to reboot if asked.
* After another reboot, open terminal using "Run as administrator" and execute the following

```bash
sc config WinRM start= auto
net start WinRM
winrm quickconfig -q
winrm set winrm/config/winrs @{MaxMemoryPerShellMB="300"}
winrm set winrm/config @{MaxTimeoutms="1800000"}
winrm set winrm/config/client/auth @{Basic="true"}
winrm set winrm/config/service @{AllowUnencrypted="true"}
winrm set winrm/config/service/auth @{Basic="true"}
```

* Once you run these commands, it may take a few seconds for vagrant to continue.
