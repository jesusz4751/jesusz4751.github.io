---
layout: post
title: Cisco Packet Tracer - Network Configuration Walkthrough
description: Configure a network consisting of 2 LANs connected via a router. (This is part of Calbright's Network+ course and corresponds with Lab 2)
image: assets/images/posts/image_1784131523913.png
---

# Lab Objectives

- Complete the network documentation.
- Perform basic device configurations on a router and a switch.
- Verify connectivity and troubleshoot any issues.

In this lab, we are presented with two LANs that are interconnected via a single router. Our network manager wants us to demonstrate our technical skills by configuring the network devices to establish connectivity between all devices.

The first thing we are given is a partially filled Addressing Table. The last column for Default Gateway is incomplete, but everything else has been given to us. Because of this, the first logical step is to configure each of the networking devices we have with the given information.

<img src="/assets/images/posts/image_1784131868470.png" width="auto" alt="image_1784131868470.png">
## Step 1: Configure the Router
Our first step in this scenario is to configure our router with the information we have been given. An image from the current network layout is shown below. Our goal is to configure the two interfaces, G0/0 and G0/1, so that the router recognizes them and is able to move traffic between them.

<img src="/assets/images/posts/image_1784132037220.png" width="auto" alt="image_1784132037220.png">

Our first step is to log on to the router and enable privileged mode. Since this is a newly configured router, it has no credentials and can be accessed without any password. Press enter to activate the CLI and type "en" (short for enable) to enter privileged EXEC mode. You will know you're in privileged mode when you see a # at the end of the line. Type in "conf t" (short for configure terminal) to enter configuration mode from the terminal. You should see the following screen:

<img src="/assets/images/posts/image_1784132319487.png" width="auto" alt="image_1784132319487.png">

The first thing we want to do is give our router an appropriate name. This way, we will know from the command line which device we are configuring. Type in "hostname College" to change the name of the router to College. You should see that the name in the beginning of the line changed from "Router" to "College"! This means that everything's working correctly.

<img src="/assets/images/posts/image_1784132505052.png" width="auto" alt="image_1784132505052.png">

Next, we want to set a password to both the basic CLI and privileged mode. Type in "line con 0", "password cisco", "login". Line con 0 will allow you to configure port 0 in the router, which is the console line. Password will set the password to cisco, and login ensures that the router verifies the password on each login. Next type "exit" to return to the previous line.

<img src="/assets/images/posts/image_1784132796751.png" width="auto" alt="image_1784132796751.png">

Now we want to create an encrypted password for our privileged mode. We do this by typing in "enable secret class". Class becomes our password to access privileged mode, and secret encrypts it in the running-config file. To encrypt all passwords that aren't encrypted by default (such as our basic login password), type "service password-encryption".

<img src="/assets/images/posts/image_1784132965661.png" width="auto" alt="image_1784132965661.png">

A final good security practice is to display a banner on login. This is a way to let others know that only authorized users should access the CLI of the router. To do this, type in 'banner motd "Only authorized users allowed!"'. This will display the message upon initial login.

<img src="/assets/images/posts/image_1784133202882.png" width="auto" alt="image_1784133202882.png">

Before we move on to configuring the interfaces, let's check to see if our current configurations worked. Type in "end" to exit configuration mode and "exit" to log out of the router. When you reactivate the router, you should see the banner and a prompt for password on login. If you see this, that means you did everything correctly! Log back into configuration mode using "en" and "conf t".

<img src="/assets/images/posts/image_1784133391319.png" width="auto" alt="image_1784133391319.png">

Now we will work on configuring each of the interfaces. Going back to our Addressing Table, we see that we have two interfaces to configure, each with an IPv4 address, IPv6 address, and a link-local address.

<img src="/assets/images/posts/image_1784133557569.png" width="auto" alt="image_1784133557569.png">

To start, switch to the GigabitEthernet 0/0 interface by typing "interface GigabitEthernet 0/0". This will allow you to configure settings specifically on this interface. Start by giving the interface a description so we know what it's for. Type in "description LAN connection to Class-A".

<img src="/assets/images/posts/image_1784134338982.png" width="auto" alt="image_1784134338982.png">

Then, we want to configure the IPv4, IPv6, and link local address. To configure the IPv4 address and subnet mask, type "ip address 128.107.20.1 255.255.255.0". To configure the IPv6 address, type "ipv6 address 2001:DB8:A::1/64". To configure the link local address, type "ipv6 address FE80::1 link-local". Finally, we want to ensure that the interface is enabled by typing "no shutdown".

<img src="/assets/images/posts/image_1784134267996.png" width="auto" alt="image_1784134267996.png">

Now do the same thing for the other interface, GigabitEthernet 0/1. Configure the IPv4, IPv6, and link local address according to the Addressing Table, then enable it using "no shutdown".

<img src="/assets/images/posts/image_1784134620730.png" width="auto" alt="image_1784134620730.png">

We have two more things to configure before moving on. First, we want to ensure that we're able to route IPv6 unicast packets via the router. We do this by typing "ipv6 unicast-routing". We also want to configure a password for our VTY line. This is a virtual line for remote management, such as SSH. We do this by entering "line vty 0", "password cisco", "login".

<img src="/assets/images/posts/image_1784135096526.png" width="auto" alt="image_1784135096526.png">

We finished configuring our router! Our last step is to copy our running configuration to the device's startup configuration. This way our router will remember our configuration when it reboots. exit configuration mode and type "copy run sta" (short for copy running-config startup-config), then press enter. This will save your changes for future use on the router.

<img src="/assets/images/posts/image_1784135233832.png" width="auto" alt="image_1784135233832.png">

If we go back to our network, we see that the two lines connected to the router are green. That means everything is working properly and traffic can pass through the router. Congratulations! Now it's time to configure the Class-B switch.

<img src="/assets/images/posts/image_1784135293729.png" width="auto" alt="image_1784135293729.png">
## Step 2: Configure the Switch
Configuration for the switch will be essentially the same as the router. This lab locks the switch labeled Class-A, so the only switch we will be configuring is Class-B. Log onto the switch and enter administrative mode. Since it's the first time it's been opened, there isn't a password. In configuration mode, change the name to Class-B, give the switch an appropriate banner, enable passwords for the CLI and privileged mode, and encrypt passwords. The commands are the same as on the router.

<img src="/assets/images/posts/image_1784218479675.png" width="auto" alt="image_1784218479675.png">

Next, we will configure VLAN 1, which is the default VLAN on the switch. We will access it using the "interface VLAN 1" command, and then configure it using the same commands we used to configure other interfaces on the router. We will add a description, define the ip address and subnet mask, and activate it.

<img src="/assets/images/posts/image_1784218710113.png" width="auto" alt="image_1784218710113.png">

Finally, copy the running config to the startup config so the switch will remember its configurations when it resets.

<img src="/assets/images/posts/image_1784218786314.png" width="auto" alt="image_1784218786314.png">

Congratulations! We finished configuring both our router and switch, and now packets can traverse the network. The final step is to configure each of the end devices and test the connectivity between them.

## Step 3: Configure Hosts and Test Connectivity

Now, we need to log onto each computer individually and ensure that each of the IP configurations are set up correctly. Log onto any computer, switch to the desktop tab, and select IP Configuration. It will be on the top left of the window.

<img src="/assets/images/posts/image_1784219034315.png" width="auto" alt="image_1784219034315.png">

Once inside, we notice a couple things are wrong or missing. The IPv4 address on this computer is set to 128.107.20.30, while on our Addressing Table it says it should be 128.107.30.30 instead. Additionally, the IPv6 address and Default Gateway are missing from the configuration.

<img src="/assets/images/posts/image_1784219186847.png" width="auto" alt="image_1784219186847.png">

If we look back at our Addressing Table, we notice that the IPv4 and IPv6 addresses are available to us, but the last column for Default Gateway is missing. This is something that we will have to determine.

<img src="/assets/images/posts/image_1784219383895.png" width="auto" alt="image_1784219383895.png">

To find these values, we have to think about where our computer is connected to. If we look at the interfaces on our router, we will notice that there are two GigabitEthernet ports, 0/0 and 0/1.

<img src="/assets/images/posts/image_1784219649146.png" width="auto" alt="image_1784219649146.png">

Looking at the IP Address of both, we notice that one corresponds with the 128.107.20 network, and the other with the 128.107.30 network. If we look at our entire network, we will notice that the computer we're configuring, Student-4, is in the 128.107.30 network. Because of this, the switch it sends traffic through is connected through the GigabitEthernet 0/1 port. This means the IP address on the 0/1 interface, 128.107.30.1, is the default gateway for all computers on this subnet. Conversely, the two computers on the other subnet, Student-1 and Student-2, are connected to the 0/0 interface and have a respective default gateway of 128.107.20.1

<img src="/assets/images/posts/image_1784219725987.png" width="auto" alt="image_1784219725987.png">

Now go back and configure all of the missing information on Student-4. It should look like this once it's complete.

<img src="/assets/images/posts/image_1784220665993.png" width="auto" alt="image_1784220665993.png">

Now, go through the other 3 computers and do the same thing, checking the Addressing Table to correct the information on each of the IP configurations.

Once you complete this, it's time to check to see if you can send traffic to both computers within the same subnet and computers on a different one. Open Student-4, and enter the command prompt from the desktop tab. You should be presented with a black screen waiting for input.

<img src="/assets/images/posts/image_1784221027713.png" width="auto" alt="image_1784221027713.png">

First, we will test connectivity between computers on the same subnet. Ping Student-3 by typing "ping 128.107.30.25". If everything was set up correctly, we should see a reply from the computer.

<img src="/assets/images/posts/image_1784221055877.png" width="auto" alt="image_1784221055877.png">

Next, we will try to test connectivity between different subnets by pinging Student-1. Type in "ping 128.107.20.25", and if everything is set up correctly we should get a reply from the other computer.

<img src="/assets/images/posts/image_1784221204495.png" width="auto" alt="image_1784221204495.png">

Congratulations! You've configured an entire network from scratch, setting up a new router and a switch alongside enabling connectivity between different computers.
