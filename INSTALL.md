## How to install the file system on a mothership

1. Clone the git repository
2. Install docker compose
3. Create environment variable files (from template)
4. Set up Camera Symbolic Link
5. Run Docker Compose



### Clone the git repository
1. go to folder where it will live
2. git clone <repo>

### Install docker compose
Run these commands
```
sudo apt-get install libffi-dev libssl-dev python3-dev python3 python3-pip -y
Set the default version of Python and Pip (Optional)

sudo nano ~/.bashrc
On the top, paste this code:

alias python=python3
alias pip=pip3
Save and exit.

Paste this code:

source ~/.bashrc
We can now install the docker compose using pip

sudo pip3 install docker-compose
Let check the version of docker compose

docker-compose --version
#-->docker-compose version 1.29.1, build unknown
Finally, reboot your Raspberry Pi

sudo reboot
```

See https://www.diyhobi.com/install-docker-and-compose-on-raspberry-pi-4/ for more details

### Create environment variable files (from template)
1. Make a copy of each `xxx.template.env` but name it `xxx.env` (remove `.template`)
2. In each file fill out the variables

### Set up Camera Symbolic Link
This is so the video source is always the same for the script to run. Without this the source may be video0 or video2 or video11 etc

Find first video (likely `/dev/video0`)
`sudo v4l2-ctl --device=/dev/videoXXX --all`
`udevadm info --attribute-walk --path=$(udevadm info --query=path --name=/dev/videoXXX)`

Once you find the correct video source, note the `idVendor` and the `idProduct`

`sudo nano /etc/udev/rules.d/83-webcam.rules`

PUT IN RULES
`KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="VENDOR_ID_HERE", ATTRS{idProduct}=="PRODUCT_ID_HERE", SYMLINK+="video-cam"`

Check, validate, and restart system
```
udevadm monitor
udevadm test $(udevadm info --query=path --name=video-cam) 2>&1
sudo udevadm control --reload
udevadm trigger
ls -la /dev/video*
```
`sudo reboot`


### Run Docker Compose

`docker-compose up -d`


