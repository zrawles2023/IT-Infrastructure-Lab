
#Create the scripting file on the IT Server
sudo nano /usr/local/bin/ping-check.sh

#File Contents

#!/bin/bash

#Hosts to Check

HOSTS=("client-01.internal.lan" "client-02.internal.lan" "ns1.internal.lan")
LOGFILE="/var/log/ping-check.log"
TIMESTAMP=$(date '+%Y-%m-%d %H:%M:%S')

echo "=== Ping Check @ $TIMESTAMP ===" >> "$LOGFILE"

for HOST in "${HOSTS[@]}"; do
    if ping -c 2 -W 2 "$HOST" > /dev/null; then
        echo " $HOST is reachable" | tee -a "$LOGFILE"
    else
        echo " $HOST is NOT reachable" | tee -a "$LOGFILE"
    fi
done

echo "" >> "$LOGFILE"

#Make file executable
sudo chmod +x /usr/local/bin/ping-check.sh

#Test it
sudo /usr/local/bin/ping-check.sh

#Log output
cat /var/log/ping-check.log



-----------------------------------------------------------------
This script performs a basic reachability check for specified hosts using the ping command. It logs the results with timestamps to /var/log/ping-check.log and prints them to the terminal in real time. It's useful for quickly verifying network connectivity to critical systems in a small internal lab environment.
