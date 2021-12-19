## How to install the file system on a mothership

1. Clone the git repository
2. Install docker compose
3. Create environment variable files (from template)



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