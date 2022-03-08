### Unlock Delta Debugging on Windows and store the log file on disk

You basically can create a debug log for the Detla updates from `brave_installer-delta-x64.exe` which allows you to see several things. This change explained on this page here is only interesting and relevant if you work with Dev Builds and want to check if you get the updates or not.


**Example log**

```sh
[03/01/22 22:01:34.779][BraveUpdate:goopdate][2561:4326][Running installer][C:\Program Files (x86)\BraveSoftware\Update\Install\{EA78FFA4-26E6-459D-9D48-03CA7B5750EE}\brave_installer-delta-x64.exe][][{AFK6A192-C873-4hh1-AC78-6CC90DG45365}]
```

### Needed Registry changes

You need to enable `#use-dev-updater-url` flag and then run PowerShell with admin rights, an Brave Dev build higher than 1.36.x + run the following commands with admin rights. Make sure you add both entries. An OS restart is not required.

```Powershell
New-Item –Path "HKLM:\SOFTWARE\WOW6432Node\BraveSoftware" –Name UpdateDev
New-ItemProperty -Path "HKLM:\SOFTWARE\WOW6432Node\BraveSoftware\UpdateDev" -Name "IsEnabledLogToFile" -Value ”1”  -PropertyType "DWord"
```

Restart your Brave Browser, if it is still running, make sure all processed are killed and restart the Brave Browser, go into `brave://settings/help` and wait until you get an update. 

### Update log location

Once you did all mentioned steps above, you can see a new file under `C:\ProgramData\BraveSoftware\Update\Log\`, it is called `BraveUpdate.log`.


### Additional Debugging flags

Those flas are usually inactive because they depend on other things or disabled by default and need to be manually enabled in order to reveal more debugging information.

- [#conversion-measurement-debug-mode](chrome://flags/#conversion-measurement-debug-mode) | Conversion Measurement Debug Mode | ❌ Disabled by default
- [#debug-packed-apps](chrome://flags/#debug-packed-apps) | Debugging for packed apps | ❌ Disabled by default
- [#enable-debug-for-secure-payment-confirmation](chrome://flags/#enable-debug-for-secure-payment-confirmation) | Secure Payment Confirmation Debug Mode | ✔️ default but inactive
- [#enable-debug-for-store-billing](chrome://flags/#enable-debug-for-store-billing) | Web Payments App Store Billing Debug Mode | ✔️ default but inactive
- [#record-web-app-debug-info](chrome://flags/#record-web-app-debug-info) | Record web app debug info | ✔️ default but inactive
- [#ui-debug-tools](chrome://flags/#ui-debug-tools) | Debugging tools for UI | ❌ Disabled by default








