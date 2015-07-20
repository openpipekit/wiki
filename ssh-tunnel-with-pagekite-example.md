# Example of creating an SSH Tunnel with Pagekite.me using autorun.sh and autorunonce.sh

Set up pagekite and login on your Pi. Ideally this would go in `autorunonce.sh` but I haven't figured out how to run `pagekite.py --signup` in a noninteractive way.
```
curl -s https://pagekite.net/pk/ |sudo bash
pagekite.py --signup
```

In `autorunonce.sh`, install pagekite and register this device. Replace things in angle brackets with your info. 
```
# connect to wifi
pirateship defaults
pirateship adapter <wifi network name> WPA <wifi password> 
ifdown wlan0
ifup wlan0
# install pagekite
pagekite.py --add 22 ssh:<user>.pagekite.me
```


In `autorun.sh`. Note the ampersand after the pagekite command. This keeps pagekite from stopping execution of the following watch command.
```
#!/bin/bash

pagekite.py &

watch -n15 "./opk-cli--yoctopuce-temperature/pull  | ./opk-cli--phant/push  --public_key AJOJ0mxKQDtJ2qdMV7rM --private_key rzvzj651MXc5Vqn6Kgl6 --url data.sparkfun.com --field_name temp"
```


Per the Pagekite docs, on your own machine that you will SSH from, add this to your `~/.ssh/config` file.
```
Host *.pagekite.me
  CheckHostIP no
  ProxyCommand /bin/nc -X connect -x %h:443 %h %p`
```
If you are on a Mac, change `/bin/nc` to `/usr/bin/nc`.

Plug everything in and then ssh in by doing...
```
ssh pi@<user>.pagekite.me
```
