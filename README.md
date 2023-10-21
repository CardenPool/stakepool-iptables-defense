# Cardano Stakepool iptables Defense Script
The *DDoS-defense.sh* script configures and deploys iptables rules designed to safeguard a Cardano stakepool from a range of DDoS attack vectors, ensuring rule persistence across reboots

## Installation
### 1. Download the script to your local drive:
### 2. Customize the script 


### 3. Schedule the cronjob
Every iptable added by command line is not boot proof and will be forget at reboot time. To make the defense rules loading at boot time, we have to schedule its loading with crontab.
Since this script uses *iptables* command that requires administrative priviledges to operate, we have to run the script with root priviledges. To achieve this, we have to edit the *root cronjob list* (containing tasks run with root priviledges) makeng use of the command:
```console
sudo contab -e
```
This will open the *contab text editor interface* where we have to add the call to our script. Please replace **<YOUR-PATH>** with the right path of your local file and add the call at the end of the list.
```bash
#Apply DDoS iptables rules. NOTE: can't use iptables-persistant since we're using UFW (conflict!)
@reboot sleep 20; /<YOUR-PATH>/DDoS-defense.sh
```
PressCTRL+o to save and update the contab list, then CTRL+x to come back to te terminal. The call run the script at every boot, 20 seconds after boot time to ensure UFW and other services are up and running. You're done!
