# Exorde-CLI-Docker-Guide

### The short and fast installation guide. Execute the commands sequentially. One by one:

1
```
apt update
```
2
```
apt install git
```
3
```
apt install apt-transport-https ca-certificates software-properties-common curl
```
4
```
curl -f -s -S -L https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
5
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```
6
```
apt update
```
7
```
cd /root
```
8
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```
9
```
sudo systemctl status docker
```
10
```
git clone https://github.com/exorde-labs/ExordeModuleCLI.git
```
11
```
cd ./ExordeModuleCLI
```
12
```
docker build -t exorde-cli .
```
13
```
docker run -d exorde-cli -m YOUR_MAIN_ETH_ADDRESS -l 2
```
For example:
```
docker run -d exorde-cli -m 0x16f177263988fF6fc8999013BD9bCB70F39b42d3 -l 2
```

### NOTES

Done! Your module is running in the container in the background. Now you can close the CLI terminal, and the module will continue to work.

To run another copy of the module, simply repeat the same command:
```
docker run -d exorde-cli -m YOUR_MAIN_ADDRESS -l 2
```
How many times will you enter this command, how many modules will you run.

Don't forget that containers can sometimes stop. And they need to be restarted. First, we need to find out <container_id>
To do this, enter a command that will display all our containers:
```
docker ps -a
```
Copy your <container_id> and enter the command to restart the container:
```
docker restart <container_id>
```
For example:
```
docker restart 1f77bd5b1111
```
Also, with the same command, you need to restart the module when a new version is released.

To display the processes taking place in a container that is open in the background, you need to enter the command:

```
docker logs --follow  <container_id>
```
For example:
```
docker logs --follow  1f77bd5b1111
```

Other commands that may be useful to you:

Stop a module:

```
docker stop <container_id>
```

Delete a module:

```
docker rm <container_id>
```

Remember that in order for your modules to work properly, it is necessary that they do not overload your system. Therefore, open such a number of modules that will work optimally for your technical characteristics

View general server statistics (for example, to check the system load):

```
top
```
[OFFICIAL INSTRUCTION FROM THE EXORDE LABS TEAM](https://github.com/exorde-labs/ExordeModuleCLI/tree/feat/docker)
OFFICIAL INSTRUCTION FROM THE EXORDE LABS TEAM => http://google.com/](

Remember that you need to constantly monitor the updates that are published in [Discord Exorde](https://discord.gg/ExordeLabs) in the #testnet channel
