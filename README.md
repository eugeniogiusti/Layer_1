# Cisco 2950 Switch Factory Reset and Console Connection Guide

## Physical Factory Reset
1. Power off the switch
2. Locate the Mode button on front panel (left side of LEDs)
3. Waiting boot system
4. Keep holding Mode button for 15-20 seconds until LED blinks amber
5. Release Mode button
6. Switch will reset to factory defaults

![image](https://github.com/user-attachments/assets/fed3670a-d522-455f-99b5-c88cb9b5e897)

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
![image](https://github.com/user-attachments/assets/e941da62-f990-4ddf-a958-a178f82d4f12)

![image](https://github.com/user-attachments/assets/d56716ca-8a3a-4634-9e86-c6a92f1a81d3)

![image](https://github.com/user-attachments/assets/f4a2c8e8-9ead-43f3-b7f9-7a5813ce42eb)


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
     ![image](https://github.com/user-attachments/assets/4a447941-b8d7-472a-866d-a05d50d8d3e1)

     ![image](https://github.com/user-attachments/assets/713e66d4-35a5-487b-8201-3622b8cf1612)

     ![image](https://github.com/user-attachments/assets/bb89a4bb-305f-4d2e-93bd-402c295fdb1e)


   
3. Connection Settings:
   - Speed: 9600 baud
   - Data bits: 8
   - Stop bits: 1
   - Parity: None
   - Flow control: None

4. Basic Configuration After Reset | Password configuration console line
   ```
   enable
   configure terminal
   line console 0
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
