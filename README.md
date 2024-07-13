# esp-power-saver
Automated supply control for battery powered devices


## Purpose
This device can restart a powered-down battery-powered device such as a Raspberry Pi.

## Assumption

Power-cycling, i.e. disconnecting the battery supply and reconnecting it, will cause the system to restart/reboot.

This is true for all Raspberry Pi computers, other devices might require some configuration.

## Typical uses




## Typical configurations

In most cases the ESP-Power-Saver will run from the same power supply, usually a 5V LiPo power-bank, as used to power the Raspberry Pi.

The Pi enters power-saving state by issuing ```sudo poweroff```

The power-saver will restart the Pi at a pre-determined time, or after a pre-determined delay.

## Scheduling

Raspberry Pi computers, other than the new RPi 5, do not have real-time-clock (RTC) hardware.  To determine the current time and date, the computer uses its Internet connection or and attached device to get the current time from an Internet Time Server.

### Internet access

Where Internet access is available this will be the usual source of current time, and will be checked whenever the system reboot.  Note that if no connection can be made Raspberry Pi computers typically set their time from the date-stamp of the last file to be modified on the SD card.

### Real-time-clock (RTC)

A lower power module that keeps accurate time using a crystal oscillator.  Once set should keep good time for many months. Cost, approx £5.

### 2G/4G or GNSS

Where Internet access is not available, but accurate time is required a cellular modem or satellite navigation receiver can be used to obtain the time. Cost, approx £25.

### Duty-cycle scheduling

In cases where there is no accurate time source, typically where there is no Internet access and no RTC, ESP-Power-Saver can be configured to run i duty-cycle mode, for example 2 minutes on, followed by 30 minutes off.  This might be used for data logging, or time-lapse photography.


## Shutdown method

### RPi poweroff

Issuing the command 'sudo poweroff' will stop all running processes, log out all users, and place the Pi in a halted state.  This will use significantly less power than when running the operating system alone.  See XXX for power usage figures.

### Power disconnect

Ideally power should only be disconnected after the *poweroff* command has completed and the device is in the halted state.

### Watchdog disconnect or power-cycle

The ESP-Power-Saver watchdog checks for Raspberry Pi system activity and if there is none it will automatically disconnect power.  If configured to automatically restart the Raspberry Pi the power disconnect is immediately followed by a power reconnect.

