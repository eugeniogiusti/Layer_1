# Cisco 2950 Switch Factory Reset and Console Connection Guide

## Physical Factory Reset
1. Power off the switch
2. Locate the Mode button on front panel (left side of LEDs)
3. Hold Mode button while powering on switch
4. Keep holding Mode button for 15-20 seconds until LED blinks amber
5. Release Mode button
6. Switch will reset to factory defaults

- Useful links:
- https://www.youtube.com/watch?v=L1ep9CDfAaE (factory reset)
- https://www.youtube.com/watch?v=vjaScc6-MbQ (factory reset_2)

## Console Reset Method
```
switch# write erase
switch# delete flash:vlan.dat
switch# reload
```

## Verify Reset
Check these commands to confirm factory reset:
```
show running-config
show vlan
show version
```
- Running-config should show only default settings
- VLAN database should only have VLAN 1
- Interfaces should show "!" indicating no configuration

## Console Cable Connection
1. Hardware Required:
   - RJ45 to DB9 console cable (light blue Cisco cable)
   - If laptop lacks DB9 port: USB to Serial adapter

2. Software Setup:
   - Install terminal emulator (PuTTY, screen, minicom)
   - For Linux using screen:
     ```bash
     sudo apt install screen
     sudo screen /dev/ttyUSB0 9600
     ```
   
3. Connection Settings:
   - Speed: 9600 baud
   - Data bits: 8
   - Stop bits: 1
   - Parity: None
   - Flow control: None

4. Basic Configuration After Reset:
   ```
   enable
   configure terminal
   enable secret <password>
   line vty 0 15
   password <password>
   login
   end
   write memory
   ```

## Save Configuration
To save changes:
```
write memory
```
or
```
copy running-config startup-config
```

## Linux Screen Commands
- Exit screen: Ctrl+A, then type ":quit"
- Detach screen: Ctrl+A, then D
- List screens: screen -ls
- Reattach: screen -r
