---
layout: default
---

<div style="text-align:center"><h1>Frequenty Asked Questions</h1></div>

<div style="width:80%; margin:auto">
</div>

1. **My Question is not answered here**  
   Join our [Telegram channel](https://t.me/thcorg) and ask your question. We will try to answer.

1. **Why do I get resource errors**<a id="quota"></a>  
   You likely got `out of heap memory`, `resource temporarily unavailable` or `Disk quota exceeded`. The FREE service is [restricted](../youcheapfuck) and the outbound traffic is throttled. Upgrade your server and [enjoy unlimited resources](../buy-an-upgrade).

1. **I get an SSH error**  
   Likely you got `Bad configuration option: setenv` when trying to log in to your existing server. You need to update your OpenSSH client to a newer version (`ssh -V`). Alternatively you can try `SECRET=XXX ssh -o "SendEnv SECRET" root@segfault.net` (where XXX is your _SECRET_).

1. **How can I install services or daemons**  
   Take a look at `/sec/usr/etc/rc.local`. This file is executed on bootup. There is no systemctl.

1. **How can I publish my Web Page**  
   The Web Page is automatically generated using [Pelican](https://www.getpelican.com) and the awesome Markdown syntax. All you need to do is edit the files in `/sec/www/content` and then execute:
   ```shell
   cd /sec/www && make html
   ```

1. **How do I change the password**  
   You can not. The access password is always `segfault`. However, nobody can access your server using `segfault` as a password: The system generates a unique and new `SECRET` for every new log in and then uses this SECRET to set up your private virtual server (isolated from all other servers). It is this SECRET that allows only you to access *your* server. Read the next paragraph...  

1. **How do I log back in to my server**  
   On log out you will see a *command* that allows to you to log back in to your server. It contains a `SECRET` and it is this `SECRET` that allows you access your server. The log out screen may look like this:
   ```
Access with      : ssh -o "SetEnv SECRET=XXX..." root@de.segfault.net
GOODBYE          : Join us on Telegram - https://t.me/thcorg 
```
   Use the command `ssh -o "SetEnv SECRET=XXX...` and the password `segfault` to log back in to your server. If you do not use the same SECRET and instead just do `ssh root@segfault.net` then a new server with a new /sec filesystem will be created for you.

1. **When does it self-destruct**  
   Immediately on log out. Your server shuts down and all system data and memory is wiped. Your private data in /sec and /root is only accessible while your server is running. When you log back in using the same `SECRET` then a new server is started and your (old) private data is attached again to /sec (encrypted). Type `rm -rf /sec && halt` if you also want to destroy your encrypted data.

1. **Why are my changes lost?**<a id="lost"></a>  
   Data in your home directory and in /sec, /onion and /everyone is permanent and wont get lost (unless you delete the data). Data in (/usr, /tmp, ...) is only valid for the duration of the session and will disappear when you log out. Chances are that you used `apt install` and got a warning. You can use `apt install` but the package can only be used until you log out. Alternatively you can install any package to `/sec/usr` or [pay for an upgrade](../buy-an-upgrade).

1. **Is there a list of tools**  
   The server comes with around 8GB of pre-installed tools. See the [full list](https://github.com/hackerschoice/segfault/blob/main/guest/Dockerfile). Let us know if any tool is missing and we can add it (permanently).

1. **Log in without password**  
Save this SSH key to `~/.ssh/id_sf`. 
```
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACB3jmp/3JyvY9ABgjrx4+sBnQ0T+yHsB4HTBMcJqC2OtgAAAIiJ9mzOifZs
zgAAAAtzc2gtZWQyNTUxOQAAACB3jmp/3JyvY9ABgjrx4+sBnQ0T+yHsB4HTBMcJqC2Otg
AAAEAs6YNqZSzAfZDl5/vDOB0vv7EZMxMUc/fEipuZ9A3eCHeOan/cnK9j0AGCOvHj6wGd
DRP7IewHgdMExwmoLY62AAAAAAECAwQF
-----END OPENSSH PRIVATE KEY-----
```
The same key is also available at _/config/guest/id_ed25519_. Thereafter use this command to log in:
```shell
ssh -i ~/.ssh/id_sf root@segfault.net
```

1. **How do I use reverse Port Forwarding**<a id="fwd"></a>  
   Your server runs on a private IP space. You can connect out (to the Internet) but nobody can connect to back to your server. However, every server is assigned **one** PORT on a public IP Address that is forwarded to your server. It's a different IP & PORT for every server. During log in you will see a message that looks like this (example):
   ```
[...]
Reverse Port      : 185.117.118.23:1234
[...]
```
   That's your personal IP & PORT for reverse connections. Any connection to 185.117.118.23 on Port 1234 is forwarded to your server on port 1234. You can listen for the connection like so:
```
   nc -vnlp 1234
   # If this is for a connect-back shell then you likely like to press
   # Ctrl-Z after connection and type 'stty raw -echo opost; fg'
```
   (The IP & PORT are an example. You need to read the log in message when you log in to find out your IP and PORT).


### Contact

Twitter: [https://twitter.com/hackerschoice](https://twitter.com/hackerschoice)  
Telegram: [https://t.me/thcorg](https://t.me/thcorg)  
Web: [https://www.thc.org](https://www.thc.org)  
Medium: [https://medium.com/@hackerschoice](https://medium.com/@hackerschoice)  
E-Mail: members@thc.org  