# Advanced Android Hidden Backdoor

This type of backdoor is different from any other, due to the fact that it goes beyond the limitations of all the techniques commonly used in this context. It can be hidden in any other application and it is resistant to rebooting or connectivity drop (thanks to Giovanni Colonna code that modified the msfvenom generated code, link [here](https://github.com/giovannicolonna/msfvenom-backdoor-android)).
In order to do that, the activity of the backdoor is no more related with the starting of the hosting app.

**The backdoor is invoked by two events:**

* The phone has been switched on or rebooted.
* There has been a connectivity change

In this two cases, the connectivity is checked:
* if the phone is connected, the backdoor tries to instantiate the connection with the attacker and launches a background service that retry every X minutes. (Preconfigured at 30 minutes)
* if it is disconnected and the service has been launched, the backdoor's background service is killed.

**The service will show in the list of all processes with the name of the hosting app**

# HOW TO
This procedure allows you to insert the backdoor code inside the host application without modifying its original code (like any other backdoor seen before).
```
Decompile the generated backdoor apk and, if not already done before the compilation, modify attacker's host and port in the /app/src/main/java/livingbox/Connect.java(String URL line). Then decompile the app we want to insert the code in, copy all the files in /app/src/main/java/livingbox/ to a new subfolder in the original decompiled app, in /smali/livingbox (you have to create it).
After all, modify the original AndroidManifest adding the missing permission and the rest of the lines about service and receiver wrote in this project's AndroidManifest.
Rebuild the original app and sign it!
```
**In order to make the backdoor working, you need to launch the hosting app at least one time.**

**Permission needs to be granted to the hosting app for accessing to that particular resources you are asking for.**

## Use it at your own risk
Tested on Nexus 5, Android 7.1.1
