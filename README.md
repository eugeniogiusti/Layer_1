# Ethernet Cable Crimping Guide

This guide provides step-by-step instructions for crimping Ethernet cables, including both straight-through and crossover cables. Proper crimping ensures reliable network connections.

---

## Materials Required

- Ethernet cable (Cat5e, Cat6, etc.)
- RJ45 connectors (8P8C plugs)
- Crimping tool
- Cable stripper or knife
- Wire cutter
- Ethernet cable tester (optional, but recommended)

---

## Types of Ethernet Cables

### 1. **Straight-through Cable**

Used to connect:

- Computers to switches/routers.
- Printers to network devices.

![RJ45-Pinout](https://github.com/user-attachments/assets/af6825a0-35cb-4090-a6ba-16604bc6b40f)

### 2. **Crossover Cable**

Used to connect:

- Two computers directly.
- Two switches or hubs without an uplink port.

![EthernetCross-300x217](https://github.com/user-attachments/assets/1ee3e643-1372-4e8a-a88e-a76f4532ebaf)


---

## Wiring Standards

There are two main standards for Ethernet cable wiring:

### **TIA/EIA-568A**

```
Pin 1: White/Green
Pin 2: Green
Pin 3: White/Orange
Pin 4: Blue
Pin 5: White/Blue
Pin 6: Orange
Pin 7: White/Brown
Pin 8: Brown
```

### **TIA/EIA-568B**

```
Pin 1: White/Orange
Pin 2: Orange
Pin 3: White/Green
Pin 4: Blue
Pin 5: White/Blue
Pin 6: Green
Pin 7: White/Brown
Pin 8: Brown
```

### **Choosing the Standard**

- Use the same standard (568A or 568B) on both ends for a straight-through cable.
- Use 568A on one end and 568B on the other for a crossover cable.

---

## Steps for Crimping Ethernet Cables

### 1. **Prepare the Cable**

- Cut the cable to the desired length using wire cutters.
- Strip approximately 1.5 inches (3-4 cm) of the outer jacket using a cable stripper.
- Untwist the wire pairs and straighten them.

### 2. **Arrange the Wires**

- Arrange the wires according to the desired wiring standard (568A or 568B).
- Flatten and align the wires in the correct order.

### 3. **Trim the Wires**

- Trim the wires evenly to about 0.5 inch (1.2 cm) from the jacket.
- Ensure no wire extends beyond the others.

### 4. **Insert the Wires into the RJ45 Connector**

- Hold the RJ45 connector with the clip facing down.
- Insert the wires into the connector, ensuring each wire is fully seated in its slot.
- The outer jacket should fit snugly inside the connector to ensure a secure crimp.

### 5. **Crimp the Connector**

- Place the connector into the crimping tool.
- Squeeze the tool firmly to crimp the connector onto the wires.
- Remove the connector and inspect for proper crimping.

### 6. **Repeat for the Other End**

- Repeat the process for the other end of the cable, using the appropriate wiring standard.

### 7. **Test the Cable**

- Use an Ethernet cable tester to verify continuity and proper wiring.
- Ensure all pins are correctly connected and there are no shorts or miswires.

---

## Troubleshooting Tips

- **Wires not fully seated**: Trim and reinsert the wires, ensuring they are flush with the connector's front.
- **Poor connection**: Check the crimping tool's pressure and ensure the outer jacket is securely crimped.
- **Cable tester fails**: Verify the wiring order and re-crimp if necessary.

---

## Additional Notes

- Use high-quality cables and connectors for optimal performance.
- Avoid over-tightening or damaging the cable jacket during crimping.
- Label cables for easier identification in complex networks.

![images](https://github.com/user-attachments/assets/58d3dbad-f97d-4ecd-b977-b0536260da4d)

- Useful videos: 
- https://www.youtube.com/watch?v=NWhoJp8UQpo
- https://www.youtube.com/watch?v=noRk8jYAbSg


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

4. ## Basic Configuration | Password configuration console line
   ```
   enable
   configure terminal
   line console 0
   password <password>
   login
   end
   write memory
   ```

### Set Enable Password (Privileged EXEC mode)
```
enable
configure terminal
enable secret <password>
end
write memory
```

### Configure hostname
```
enable
configure terminal
hostname <name>
end
write memory
or to save the configuration
copy running-config startup-config
```

### SSH Configuration
```cisco
Switch(config)# hostname switch_name
Switch(config)# ip domain-name local.net
Switch(config)# crypto key generate rsa
Switch(config)# username admin password your_password
Switch(config)# line vty 0 15
Switch(config-line)# transport input ssh
Switch(config-line)# login local
```

### Linux Screen Commands
```
Exit screen: Ctrl+A, then type ":quit"
Detach screen: Ctrl+A, then D
List screens: screen -ls
Reattach: screen -r
```
