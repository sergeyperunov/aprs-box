# Direwolf

Direwolf can be found at [https://github.com/wb2osz/direwolf](https://github.com/wb2osz/direwolf). This box is based on Direwolf 1.2.

## Compiling Direwolf

Direwolf is surprisingly easy to compile: if you followed the instructions in [Software](software.md), then it is a matter of cloning the Direwolf repository on your Beaglebone, then follow the standard instructions for Linux:

```
git clone https://www.github.com/wb2osz/direwolf
cd direwolf
git checkout 1.2
make
sudo make install
make install-conf
```

## Configuring Direwolf

You should then install the configuration for Direwolf in ```/etc/direwolf/direwolf.conf``` . This file, along with all other configuration files is located in the github repository of the project. [/etc/direwolf/direwolf.conf](https://github.com/elafargue/aprs-box/blob/master/config/etc/direwolf/direwolf.conf).

You will need to set the "MYCALL" variable to your actual call sign before launching Direwolf, of course!

Also depending on how you are connecting to your radio, you can/should update the ```PTT``` and ```DCD``` lines to reflect the GPIOs you are using.

Last: by default, direwolf.conf is configured to listen only. Configure the "PBEACON" and/or "OBEACON" lines to enable beaconing if you want to.

## Configuring Direwolf logs

For a box that is running 24/7, you should make sure direwolf's log output is properly handled. This is done through the syslog and logrotate facilities:

- [/etc/logrotate.d/direwolf](https://github.com/elafargue/aprs-box/blob/master/config/etc/logrotate.d/direwolf)
- [/etc/rsyslog.d/direwolf.conf](https://github.com/elafargue/aprs-box/blob/master/config/etc/rsyslog.d/direwolf.conf)

This way, all direwolf log output will be directed to ```/var/log/direwolf.log``` and be automatically rotated every day.

## Automatically starting Direwolf

Then next step is to make sure Direwolf automatically starts when the box boots:

- [/etc/init.d/direwolf](https://github.com/elafargue/aprs-box/blob/master/config/etc/init.d/direwolf)

This script needs to be linked to runlevel 2:

```
cd /etc/rc2.d/
ln -s ../init.d/direwolf S001direwolf
```

so that Direwolf starts.

At this stage, you can reboot your Beaglebone to check that Direwolf does start properly:

```
ps aux | grep direwolf
tail -f /var/log/direwolf.log
```

... you can then move on to installing [Polaric Server](polaric.md)