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

Lastly, we type the command: no shutdown 
This will activate all of our gigabitethernet ports we are using for our departments. essentially turning them on.  

##

After, we can leave the cli and see that the connection to our switches will begin to turn after some time signified by the blinking green lights.

![(7) connectiontoswitchson](https://github.com/user-attachments/assets/4b5fc442-3ddb-4b4c-ad99-d3f9c7bbf3ab)

##


Step 3:
Going through the list and removing IP addresses.

![python 3](https://github.com/VegaL101/Updating-Files-in-python/assets/166334918/ef708dc7-b1bf-45dc-a355-0ee0aa78e574)

After converting the file from a string to a list we can begin the next part of the algorithm.
I will be using a for loop to go through the ip addresses and find any ip addresses that are on the remove list.

In the loop the key words for, and in are used with elements, and ip_addresses. Elements being the variable for each IP address in  ip_addresses which is the file it's going through. The algorithm then removes any ip addresses using the if conditional statement. If any of the elements from ip_addresses are found in remove_list they will be taken out of the file using the .remove() function. Which is applied to ip_addresses.

STEP 4:
Updating the file.

![python 4](https://github.com/VegaL101/Updating-Files-in-python/assets/166334918/0e1e781e-eeda-47f1-a66f-82c81d0a6642)

To finalize and update the file containing the revised lists of IP addresses we wanna use the .join() function. What this function does is convert all the items we have back into a string. Which is applied to our variable as shown below. We use the string “\n” to let python know to place each element in a new line.

Using the “w” argument with the open() function indicates that I want to open the file and rewrite its contents. Using the the .with() function with our ip_addresses variable as the argument we can apply this to our file object as shown above.This tells python that ip_addresses and its contents will replace the data in the file used with our with statement.

Summary:
I Created this algorithm so that we may remove any ip addresses found in the  remove_list variable from the  “allow_list.txt” file . This algorithm involves opening the file, converting to a string so that it may be read, and then converting it once more into a list stored in the ip_addresses variable. I then used a for loop with a conditional statement that will check and find any ip addresses in the remove_list that are inside the ip_addresses variable. I then applied the .remove()  function to remove any elements from the  remove_list found in ip_addresses. After this was done the final steps were to use the .join() function convert ip_addresses into a string.Finishing this, i used the .write() function to rewrite and update the contents of the  “allow_list.txt” file to the new and revised list.



