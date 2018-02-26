# exemple_linux_daemon

Create a new script file at /etc/init/myphpworker.conf. Here is an example:
################################################################
# Info
description "My PHP Worker"
author      "Jonathan"

# Events
start on startup
stop on shutdown

# Automatically respawn
respawn
respawn limit 20 5

# Run the script!
# Note, in this example, if your PHP script returns
# the string "ERROR", the daemon will stop itself.
script
    [ $(exec /usr/bin/php -f /path/to/your/script.php) = 'ERROR' ] && ( stop; exit 1; )
end script


#############################################################
Starting & stopping your daemon:
sudo service myphpworker start
sudo service myphpworker stop

Check if your daemon is running:
sudo service myphpworker status
