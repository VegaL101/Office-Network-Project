# Office-Network-Project

## Objective

In this Project i will be going over how i created a simple office network using Cisco packet tracer to simulate A real life office network setting. In this project we will have 3 departments. A acounting, IT, and operations department with their own respective subnet. Each with 2 PC's and a printer. 

### Skills Learned

- Network Design  
- IP addressing and subnetting
- router configuration
- Networking Testing 

## Steps

Step 1:
Creating the network layout

Firstly, We will be using the network address 192.168.1.0 for our office in this project. Now we add our main router. On the bottom left we can click on network devices > routers > 2911 router  which is the model router we are using for this project. We Then add our 3 switches which we name accounting Dept, IT Dept, and Operations Dept. Go to network devices > 
switches > 2960 which will be the switch model we will be using.

 Switches are good for segmentation and improve network performance by isolating devices and eliminating collisions. Our layout is shown below.

![(1)routers and switches](https://github.com/user-attachments/assets/b95c3dab-2078-4c67-9383-20f9fae192b1)

##

We then add 2 PC'S and 1 printer for each department. We go to End devices > End devices > PC and then End devices > End devices > Printer. We then name them and align them as shown below.

![(2)PCSandPrinters](https://github.com/user-attachments/assets/24a0bfdf-d4bc-4958-8b71-56bcf8f0ba51)

##

Next, we make our connections from the router to the switches. as shown below. To do this we go to the bottom left and click on connections > connections > copper straight-through which is the cable we are using. Once the connector is selected we click on our router and use port "gigabitethernet 0/0" and drag the connnection to the accounting switch's port "gigabitethernet 0/1". We do the same for the Rest of the departments. We connect "gigabitethernet 0/1" from our router to IT's switch at "gigabitethernet 0/1". For operations we connection "gigabitethernet 0/2" to Operations gigabitethernet 0/1.

![(3)connections to switches](https://github.com/user-attachments/assets/5ffdabf8-2528-4c93-8b9d-28d7220c1bac)

##

Now, we make our connections from our switches to our endpoint devices in each department. We use Fastethernet ports 1-3 from thw switch to connect to our 2 PC's and printer Fastethernet port 0 or port 0 on our devices. We do this for all devices in their respective departments.

![(4) connections](https://github.com/user-attachments/assets/59070f5e-1394-4a9e-8599-903877dc7174)

##

Next, I added some quick bubbles to help organize the departments.

![(5) added bubbles](https://github.com/user-attachments/assets/85e3d882-1514-4483-9949-85ec525b96c9)

##


Step 2:
Enabling the router and creating our subnets

I stated earlier that for this project we are using the network address 192.168.1.0 and we will use this address and create three subnets. Our IP address is a 32bit address with a 255.255.255.0 /24bit subnet mask. A Ip address is broken into 4 octets. The first 3 octets 192.168.1 are the network identifier and last octet .0 is the host identifier. To get our subnets we calculate the formula below.

![formula](https://github.com/user-attachments/assets/2786cf0f-905d-4401-babc-294100ac4906)

N=1 bit that we would borrow from the part of the address. so when we ca;culate 2 to the power of 1 our answer is 2 subnets. so instead lets try borrowing 2 bit and calculating it which would give us 4 subnets which gives us one extra subnet than we need. After borrowing these 2 bits our new subnet mask is 255.255.255.192 or /26 bits (24 original network portion bits + 2 borrowed bits from the host portion). 

##

Now to we have our 4 subnets we need to find out how many usable IP addresses we have per subnet. To do so we calculate 2(borrowed bits) to power of 6 (bits left from host portion) which comes out to be 64 but we subtract 2 which leaves us 62. so in each subnet we have 62 Usable ip addresses for devices as well as one ip address for the network address and one 
other for the broadcast address per subnet. so all together it should similar to this:

Subnet 1 (Accounting):<br>
Network: 192.168.1.0/26 <br>
Usable IP range: 192.168.1.1 - 192.168.1.62<br>
Broadcast: 192.168.1.63<br>

Subnet 2(IT):<br>
Network: 192.168.1.64/26<br>
Usable IP range: 192.168.1.65 - 192.168.1.126<br>
Broadcast: 192.168.1.127<br>

Subnet 3(Operation):<br>
Network: 192.168.1.128/26<br>
Usable IP range: 192.168.1.129 - 192.168.1.190<br>
Broadcast: 192.168.1.191<br>

Subnet 4(Extra):<br>
Network: 192.168.1.192/26<br>
Usable IP range: 192.168.1.193 - 192.168.1.254<br>
Broadcast: 192.168.1.255<br>

##

Now we have our subnets so we can continue to enable and configure our router. We select our router to see the device and what it looks. we wannna zoom in and actually power on the router first before we can do anything.

![(5 5) turn the power on](https://github.com/user-attachments/assets/ccc2e979-bbcb-4623-94e0-571ab4f2935f)

##

Next, in the command line interface (CLI on the top left tab) is where configure our router.

![(6)routerCLI](https://github.com/user-attachments/assets/e9ca9fa2-1067-43eb-b526-fc4d3c958f59)

##

Firstly, we type in the command: en <br>
To enable our router.

We then type: config t<br>
Which allows you to enter a configuration mode to make changes

Then enter in: int range gig0/0-2 <br>
this lets us enter the configuration for our interfaces. 

Next, we type the command: no shutdown<br>
This will activate all of our gigabitethernet ports we are using for our departments. essentially turning them on.  

Lastly to save our changes we type:<br>
do wr


![(6 5) router cli](https://github.com/user-attachments/assets/70c2b1f3-8e09-4783-9066-0941492a98f8)

##

After, we can leave the cli and see that the connection to our switches will begin to turn after some time signified by the blinking green lights.

![(7) connectiontoswitchson](https://github.com/user-attachments/assets/4b5fc442-3ddb-4b4c-ad99-d3f9c7bbf3ab)

##

We now move onto adding our subnets. We come back to the CLI of our router to add our accounting subnet. we type:<br>
>en<br>
>configure terminal (config t is short for configure terminal)<br>
>interface gigabitethernet 0/0 (int is short for interface)<br>
>ip address 192.168.1.1 255.255.255.192(we assign this first usable IP in the subnet for the interface)<br>
>no shutdown
>exit

![(8) subnet for accounting](https://github.com/user-attachments/assets/e472c4b5-a6cf-4eab-91a2-e1ef224f6d18)

##

We now moving onto the IT subnet. we type:<br>
>configure terminal<br>
>interface gigabitethernet 0/01<br>
>ip address 192.168.1.65 255.255.255.192(we assign this first usable IP in the subnet for the interface)<br>
>no shutdown
>exit

![(9)IT subnet](https://github.com/user-attachments/assets/f61b209d-9193-4b00-adc8-59ece7679cff)

##

Lastly, the Operations subnet. we type:<br>
>configure terminal<br>
>interface gigabitethernet 0/01<br>
>ip address 192.168.1.129 255.255.255.192(we assign this first usable IP in the subnet for the interface)<br>
>no shutdown
>exit
>do wr (to save our changes)

![(10)operationsubnet](https://github.com/user-attachments/assets/80ba1e60-cac8-49e4-92b1-d2aedb1960db)

##

In order to check if everything was done correctly we type:
>en
>show ip interface brief


![(11) check  if subnets are set up properly](https://github.com/user-attachments/assets/5d123f24-4c47-49a0-a86a-df6942c6a0b4)

Here we can see the status of our interfaces 

##

Step 3:
configuring our end devices and testing

Now that we have set up our subnets we then go ahead and start setting up our PC's and printers. First, we'll be setting up accountings devices.<br>
For the first PC we click it, head over to the desktop tab and then to IP configuration.<br>

Here i choose static ip and give it one of the usable ipv4 addresss fromm the first subnet and give it the subnet mask 255.255.255.192 going forward we will be using the same subnet mask for all end devices <br>
if done correctly it should look similar to my image below.

![(11 5) gettopcipconfig](https://github.com/user-attachments/assets/3bccd8a7-dbfd-40a3-ab59-91375655f35f)

##
To test our configuration we can exit ip configuration and go to command prompt using the same PC and ping our accounting interface by entering the commmand: ping 192.168.1.1 <br>
this ping should send out 4 packets and receive 4 as a reply if everything has been done correctly so far.

![(12) accPCping](https://github.com/user-attachments/assets/44fee780-b78e-4b3c-ad84-159a36236d83)

We do the same thing for our second PC in the accounting dept using the next available IP address.

##

Next, we continue to configure the printer. We click on it and go to the config tab to add our next ip address and our subnet mask. 

![(13)printer settings](https://github.com/user-attachments/assets/233ea023-ecba-4581-b0a2-1967ae6efdfe)

##

After doing so we can ping the printer to test it. we come back to our pc in the same deparment and ping the ip address we gave our printer.

![(12 5)accprinterping](https://github.com/user-attachments/assets/d091bab7-8213-4c8e-b981-e5fb11225518)

##

Next, we move onto the It department our usabele ip ranges for this department are: 192.168.1.65 - 192.168.1.126 excluding 192.268.1.65 since we are already using this ip for our IT interface.
we configure our IP settings again on our PC 

![(14)itpcip](https://github.com/user-attachments/assets/343c1442-66fe-42d4-a2b1-10dbbfffe8ad)

##

We then ping our IT interface to test it.

![(15)ITpcping](https://github.com/user-attachments/assets/761c0e67-bac3-4b9b-9095-104d511ba31f)

##

We then go to our IT printer configure the settings.

![(16)ITprinter settings](https://github.com/user-attachments/assets/8ff83733-439e-494e-b1c9-17b0601b3217)

##

And then ping it to test it.

![(15 5)ITprinterping](https://github.com/user-attachments/assets/a6ca96e0-2f5f-4550-92a5-58cf836bb8e7)

##

Lastly we do all these steps again with the Operations department. We uses the ranges 192.168.1.129 - 192.168.1.190 excluding 192.168.1.129 (interface ip address) and then ping all the devices in the department. Like below.

Operations interface ping.

![(18)operationpcping](https://github.com/user-attachments/assets/1ced522e-4350-4bd9-954f-44f2a917dfac)

Operations printer ping.

![(18 5)operationprinterping](https://github.com/user-attachments/assets/97eff731-c9f0-4f84-a07a-7adabf8db871)

##

Now we have configured the ip addresses for all the end devices. The end devices are able to communicate with each other in their respective department. But what if we wanted a PC from one department to communicate with a PC in another department.<br>
In order for us to do this we need to configure our gateways it helps us connects with different networks.

For accounting we go to all our end devices IP configurations and in our default gateway we type in '192.168.1.1' you might notice that the ip address is the same as our accountings interface IP and thats because our devices will be using that interface as a gateway to connnect to other networks. 
![(19)accounting gateway](https://github.com/user-attachments/assets/590a3639-2ef3-4d7c-8a0d-796bec1a6a25)

This is the gateway we use for our IT end devices.

![(20)ITgateway](https://github.com/user-attachments/assets/ce583c17-e3cd-4af3-ad4b-53d7fb430ce1)

And this is our gateway for our Operations end devices.

![(21) operation gateway](https://github.com/user-attachments/assets/99abf831-594a-47cd-926e-db4926e4f5e0)

##

Now, to test what we have configured everything properly we can ping into a end device in our IT department and then our Operations department.

Here we ping to IT successfully.

![(22) pingto IT](https://github.com/user-attachments/assets/5718d314-4c89-4145-8712-60d9b9b6b274)

And, Here we ping to Operations successfully. 

![(23)PIng to operations](https://github.com/user-attachments/assets/61800c9e-ddaf-45d8-8d72-fc3d6341fed9)

##

###Summary

In this project, you’ll gain hands-on experience with key networking concepts such as subnetting, IP address management, and routing. By dividing a larger network into smaller subnets, you'll practice efficient address allocation and configure network devices accordingly. Setting up the router to enable communication between these subnets will reinforce your understanding of routing principles and inter-network communication.



