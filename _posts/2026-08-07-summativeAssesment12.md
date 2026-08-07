---
layout: post
title: Cisco Packet Tracer - Network Cabling Walkthrough
description: Configure a network and connect all devices to the local service provider. (This is part of Calbright's Network+ course and corresponds with Lab 9)
image: assets/images/posts/image_1786120740385.png
---
# Lab Objectives
Our goal with this lab is to connect all of the end devices on the network by using the appropriate cabling for each device. We will have to also make some modifications to the switches in order for them to connect to each other and end devices.
## Step 1: Configure the switches and routers
The first thing we need to do is ensure that all the switches and routers are ready to be connected to their end devices. We immediately notice that there is no corresponding switch to connect to PCs 1, 2, and 3. However, we don't have enough money to go and buy another switch. Because of this, we have to find a way to connect the devices directly to the East router.

Click on the East router to bring up the physical interface. We notice that there aren't any interfaces that can be used to connect to the end devices, but there is an empty modular slot on the left. Going through the modules, we see there's one called HWIC-4ESW that provides 4 switching ports. This would be enough for us to connect to the PCs that don't have any switch to connect to. To connect the module, turn off the router, drag over the module to the cisco router to plug it in, and then turn the router back on.

<img src="/assets/images/posts/image_1786121485604.png" width="auto" alt="image_1786121485604.png">

Looking back at our network diagram, we notice that there is going to be a connection between switch 2 and switch 3 that has to be a Gigabit optical connection. This is because Switch 2 will be connected to the Access Point on the bottom, and that needs high speeds to work correctly. Opening the physical interface of the switch, we see there is one slot to add a module. Going through the modules, there is just one that provides us the Gigabit Ethernet optical connection, and this is the 1FGE module. Once again, you connect it by turning off the device, dragging over the module, and turning the device back on.

<img src="/assets/images/posts/image_1786121773669.png" width="auto" alt="image_1786121773669.png">

Now that we have set up our routers and switches, we can start connecting all of our devices.

## Part 2: Connect devices
We are given the following diagram showing what device should be connected where, and what cable to use. I'll be walking through each connection individually and why they are connected that way.

<img src="/assets/images/posts/image_1786122026523.png" width="auto" alt="image_1786122026523.png">

The first and simplest step is to connect the PCs to their corresponding router or switch. A copper straight-through cable is used to connect two different types of devices, such as a router and a PC. To connect two devices, first select the appropriate cable on the bottom right menu. The, click on the device you want to connect. A menu will appear with all the available ports. In this case, select the FastEthernet0 port on the PC. This is the ethernet connection that will then connect to the switch for internet connectivity. Repeat this process for all PCs and their corresponding switch. Remember that we entered a module into the East router, so it functions as a switch to the nearby PCs.

<img src="/assets/images/posts/image_1786122155868.png" width="auto" alt="image_1786122155868.png">

Next, we will be connecting each of the switches to each other and ultimately to the router. Remember that we configured a optical fiber module on switch 2 to create a Gigabit Ethernet connection to switch 3. Using the fiber optic cable, connect both switches via the GigabitEthernet5/1 port. This will allow a Gigabit Ethernet connection between both devices on the network.

<img src="/assets/images/posts/image_1786122504546.png" width="auto" alt="image_1786122504546.png">

To connect switch 1 and switch 4 to the East router, use a copper straight through cable to connect via the Gigabit Ethernet 0/1 port. Since routers and switches are different devices, they use a copper straight through cable.

<img src="/assets/images/posts/image_1786122663644.png" width="auto" alt="image_1786122663644.png">

To connect switch 4 with switch 3, use a copper cross over cable. Since they are the same type of device, a straight through cable wouldn't be appropriate, and a copper cross over cable is a better option.

<img src="/assets/images/posts/image_1786122746110.png" width="auto" alt="image_1786122746110.png">

Connect switch 2 to the Access point with a copper straight through cable, and a serial cable to connect the East router with the West router. This will complete the wired connections in the network and should provide connectivity for all PCs.

<img src="/assets/images/posts/image_1786122862871.png" width="auto" alt="image_1786122862871.png">

The only thing we have to do now is connect the two wireless devices on the bottom. The first one we will configure is the Laptop. Click on the laptop, go to the config tab, and select the Wireless0 interface. In it we see many different options for configuring our Wi-Fi settings, but the only one that matters for now is the On switch on the top right. Select that, and you should see that the device automatically connects to the access point.

<img src="/assets/images/posts/image_1786122939425.png" width="auto" alt="image_1786122939425.png">

<img src="/assets/images/posts/image_1786123037766.png" width="auto" alt="image_1786123037766.png">

Now we will go through a similar process for the TabletPC, except we will connect it directly to the cell tower via 4G. Select the tablet, go to the config tab, and select the 3G/4G Cell1 interface. Once again, select the On switch on the top right to turn on the 4G connection. It should automatically connect to the cell tower.

<img src="/assets/images/posts/image_1786123062372.png" width="auto" alt="image_1786123062372.png">

At this point, all of our devices should be connected. If you did everything correctly, the network should look like this:

<img src="/assets/images/posts/image_1786123211600.png" width="auto" alt="image_1786123211600.png">

Congratulations! You've set up an entire network with the appropriate connections and given each end device connectivity to the internet.