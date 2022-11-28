# Exorde Testnet CLI + Docker Guide

> ⚠️ Remember that you need to constantly monitor the updates that are published in our [Discord](https://discord.gg/ExordeLabs) channel #testnet. If an update comes out but you ignore it, you might just be wasting your resources (time; computing power; funds if you use a rented vps, etc.).
> 
> This guide will be updated and supplemented.


## ⭕ SYSTEM REQUIREMENTS

**CPU:** 2 cores

**RAM:** 4 Gb

**SSD:** 1 Gb


## ⭕ ACTUAL MODULE VERSION: 1.3.4a 1


## ⭕ Quick and easy installation guide. Follow the commands one by one:

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
docker run -d --restart unless-stopped --pull always --name <CONTAINER_NAME> rg.fr-par.scw.cloud/exorde-labs/exorde-cli -m <YOUR_MAIN_ETH_ADDRESS> -l <LEVEL OF LOGGING>
```
> **Variables:**
> - <CONTAINER NAME> - think of any name for your container, for example: **exorde-cli_1**
> - <YOUR_MAIN_ETH_ADDRESS> - The OTC address of your Ethereum (ETH) Mainnet wallet. (For example, from MetaMask).
> - <LEVEL OF LOGGING> - is spelled with one of five digits from 0 to 4 and means:
>      
>        = 0 - no logs
>  
>        = 1 - general logs
>  
>        = 2 - validation logs
>  
>        = 3 - validation + scraping logs
>  
>        = 4 - detailed validation + scraping logs (e.g. for troubleshooting)
>  
> Optimally use: 2

Thus, an example of a ready-made command to start one module (container) looks like this:
```
docker run -d --restart unless-stopped --pull always --name exorde-cli_1 rg.fr-par.scw.cloud/exorde-labs/exorde-cli -m 0x16f177263988fF6fc8999013BD9bCB70F39b42d3 -l 2
```

## ⭕ ### NOTES

Finished! Your module is running in the container in the background. Now you can leave everything as it is, close the CLI terminal, and the module will continue to run. But remember that you need to monitor the updates in Discord and the performance of each module separately!

To run an extra copy of the module, just repeat the same command, but with a different <CONTAINER NAME>:
```
docker run -d --restart unless-stopped --pull always --name <CONTAINER_NAME_2> rg.fr-par.scw.cloud/exorde-labs/exorde-cli -m <YOUR_MAIN_ETH_ADDRESS> -l <LEVEL OF LOGGING>
```
For example:
```
docker run -d --restart unless-stopped --pull always --name exorde-cli_2 rg.fr-par.scw.cloud/exorde-labs/exorde-cli -m 0x16f177263988fF6fc8999013BD9bCB70F39b42d3 -l 2
```
How many times you enter this command with different names, the number of modules you will run.

## ⭕ CONTROL N1. CONTAINER STATUS

Keep in mind that containers = modules can sometimes stop working.

Check the number of running modules and their status (+ find out <container_id> of each module):

```
docker ps -a
```

If the status of the container is "Up to..." - module is now active.

If the status of the container is "Exited" - this module is not working now.

![image](https://user-images.githubusercontent.com/97410466/203429617-c52b747f-570b-4dc7-b08d-8f628279506a.png)
Need to make a restart:
```
docker restart <container_id>
```
Or
```
docker restart <CONTAINER_NAME>
```
For example:
```
docker restart 1f77bd5b1111
```
Or
```
docker restart exorde-cli
```
To restart all containers = modules at once, use the command
```
docker restart $(docker ps -a -q)
```

## ⭕ CONTROL N2. SYSTEM LOAD.
For modules to work efficiently, you need to ensure that they do not overload your system. Therefore, run as many modules as will work optimally for your specifications. Accordingly, if you find that the system is working to its limits, stop and remove unnecessary modules.

View the overall statistics of your server (like Task Manager for Windows):
```
top
```

To delete a container(s), you must first stop it(s) (except for the option to use the "force" delete command).  

Stop container = module:
```
docker stop <container_id>
```
Or
```
docker stop <CONTAINER_NAME>
```
Stop all containers = modules:
```
docker stop $(docker ps -a -q)
```
Remove container = module:
```
docker rm <container_id>
```
Or
```
docker rm <CONTAINER_NAME>
```
Delete all containers:
```
docker rm $(docker ps -a -q)
```
"Force" deletion of container = module (without stopping first):
```
docker rm <container_id> --force
```
Or
```
docker rm <CONTAINER_NAME> --force
```
"Force" deletion of all containers = modules (without stopping first):
```
docker rm $(docker ps -a -q) --force
```

## ⭕ CONTROL N3. CHECKING LOGS
Check processes = logs = logs occurring in a container open in the background with the following command:
```
docker logs --follow <container_id>
```
or
```
docker logs --follow <CONTAINER_NAME>
```
For example:
```
docker logs --follow 1f77bd5b1111
```
Or
```
docker logs --follow exorde-cli
```
Processes = logs = logs can only be viewed for each container = module separately.

They will display:
- current version

![image](https://user-images.githubusercontent.com/97410466/203429108-55d479a2-9318-4088-9cfb-1cedf265aa43.png)
- processes in progress (e.g. validation, voting, etc.)
- reputation (REP) and rewards (a system message with your stats automatically appears every 10 minutes)

![image](https://user-images.githubusercontent.com/97410466/203428442-d0c91be6-957d-42ea-af9a-8b68b1f6bb11.png)
- bugs if something goes wrong

![image](https://user-images.githubusercontent.com/97410466/203428958-ce0e5724-204a-4321-bda9-f50932f9c17f.png)

In case the current version is up to date, processes are happening, REP increases over time - your module is working properly.


## ⭕ CONTROL N4. VERSION VALIDITY
IF YOU FIND A NEW VERSION OF THE MODULE (ON THE #testnet CHANNEL IN OUR Discord), THE MOST RELIABLE WAY TO REINSTALL THE MODULE VERSION IS TO COMPLETELY REMOVE AND REINSTALL THE MODULE. To do this, run the following commands in turn:

```
docker rm <container_id> --force
```

```
docker run -d --restart unless-stopped --pull always --name <CONTAINER NAME> rg.fr-par.scw.cloud/exorde-labs/exorde-cli -m <YOUR_MAIN_ETH_ADDRESS> -l 2
```

This will restart a single module. If you want to start more than one module again, just repeat the last command by changing <CONTAINER_NAME>.

> The numbering of CONTROL #1 - CONTROL #4 does not imply that the first place is the most significant control. The control must be comprehensive and include all of the above four points and you must always have the current version of the module, otherwise the rest is meaningless.

⭕ [OFFICIAL DOCUMENTATION FROM EXORDE LABS TEAM](https://docs.exorde.network/)

⭕ [OFFICIAL GITHUB MANUAL FROM THE EXORDE LABS TEAM](https://github.com/exorde-labs/ExordeModuleCLI)
