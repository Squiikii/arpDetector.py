# arpDetector.py
"A Python program to heuristically detect an ARP spoofing attack" from the book Ethical Hacking, by Daniel G. Graham.
Detecting an ARP Spoofing Attack
In this section, we’ll write a Python program to heuristically detect an ARP
spoofing attack. We’ll build our own ARP table using a dictionary and then
check to see whether the packet we receive has changed an entry. We’ll as
sume that any packet that changes the state of our table is malicious.

We’ll begin by selecting a library that can both intercept and parse the
packets that pass through our NIC. Scapy is a popular Python package that
allows us to read and send packets. Before you can use Scapy, you’ll need to
install it with pip3. Use the following commands to get both pip3 and Scapy:

kali@kali:~$ sudo apt-get install python3-pip

kali@kali:~$ pip3 install --pre scapy[basic]

Once you’ve installed Scapy, you can import the sniff library, which al
lows us to capture and inspect the packets that pass through our NIC. Copy
and paste the following Python program (arpDetector.py) into Mousepad or
the code editor of your choice. To start Mousepad, run mousepad &.

The sniff() function ∂ in the Scapy library takes several optional pa
rameters. In this implementation, we use the count parameter to indicate the
number of packets to sniff. A count value of 0 means that the library should
continuously sniff packets. We also use the filter parameter, which specifies
the type of packet to capture. Because we’re interested in only ARP pack
ets, we specify a filter value of "arp". The store parameter indicates the num
ber of packets to store. We set the parameter to 0 because we don’t want to
waste memory by storing packets. Lastly, the prn parameter is a functional
pointer that points to the function called whenever a packet is received. It
takes a single parameter, which represents the received packet, as input.

kali@kali:~$ sudo python3 arpDetector.py

As the program is running, open another Kali terminal and execute an
ARP spoofing attack.

Then, quit the attack by pressing CTRLC. This will cause arpspoof to
issue packets that restore the ARP table. When your Python program detects
these packets, you’ll see a message like the following:

Possible ARP attack detected
It is possible that the machine with IP address
192.168.0.67 is pretending to be 192.168.48.67
