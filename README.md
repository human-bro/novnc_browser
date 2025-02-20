# novnc_browser
This is used to create a novnc service so that we can stream vnc (desktop environment) to internet and be accessed through browser

```
sudo apt update
sudo apt upgrade -y
```
> To install Ubuntu desktop you could choose xfce4 for low ram or lighter deployment
```
sudo apt install ubuntu-desktop -y
```

> installing vncserver
```
sudo apt install tigervnc-standalone-server -y
```
> setup vncpassword
```
vncpasswd
```

> This sets up the vncservice to run with ubuntu desktop environment
```
mkdir -p ~/.vnc
cat > ~/.vnc/xstartup <<EOF
#!/bin/bash
export XKL_XMODMAP_DISABLE=1
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
gnome-session --session=ubuntu &
EOF
chmod +x ~/.vnc/xstartup
```
## This is for setting up ubuntu desktop we can either change this a different version of desktop like xfce4
```
vncserver :1
vncserver -kill :1
```
Or 

```
nohup vncserver :1 -depth 24 -localhost no > vncserver.log 2>&1 & 
```
> OR
```
vncserver :1 -depth 24 -localhost no
```

> To change the resolution of the vnc desktop environment this will really useful when creating this to use for a mobile phone


```
vncserver :1 -geometry 800x600 -localhost no
```

> Or

```
vncserver :1 -geometry 640x480 -localhost no
```
> best fit for mobile screens try lower if needed

```
vncserver :1 -geometry 480x320 -localhost no
```

> best for most mobile phone 

```
vncserver :1 -geometry 1080x720 -localhost no
```
> or could try 1340x720 or1440x720 these fit perfectly

> Here we use -geometry to change the resolution of the vnc viewer.
>     
> -localhost no : this says the vnc server to accept connection from anywhere if set to `yes` it would only accept machines from the local network it is part of . because we want to Access this with any ip 
we set it to `no`
```

git clone https://github.com/novnc/noVNC.git
```
> Install websockify
```
sudo apt install websockify -y
```

> Here username is root so
```
nohup websockify --web=/home/username/noVNC 80 localhost:5901 > noVNC.log 2>&1 &
```
> with username
```
nohup websockify --web=/home/root/noVNC 80 localhost:5901 > noVNC.log 2>&1 &
```
> or try just noVNC this should host the noVNC repo

> Now to access this type 
https://externalip/vnc.html
Here externalip or public ip the novnc setup can be accessed 

---

## Once executed


> You can check if any issue with websockify you can try

```
tail -f noVNC.log
```
Here noVNC.log is what nohup is forwarded to

> To stop websockify 

```
kill websockify
```
