<h1>Packet Capture and Analyzer</h1>

<h2>Description</h2>
As a security or network analyst, it’s important to know how to capture and filter network traffic in a Linux environment. It is also vital to know the basic concepts associated with network interfaces. As such, this project consists of performing tasks associated with using tcpdump to capture network traffic from a Linux virtual machine by capturing the data in a packet capture (p-cap) file and then examining the contents of the captured packet data to focus on specific types of traffic.

<br />

<h2>Task 1. Identify network interfaces</h2>

In this task, we will identify the network interfaces that can be used to capture network packet data by using the command "sudo tcpdump -D"(can also use "sudo ifconfig") to identify the interfaces that are available. 

<p align="center">
This command returns output similar to the following: <br/>
<img src="https://imgur.com/IW4taTJ.png"<br />

The Ethernet network interface is identified by the entry with the "eth" prefix.

<h2>Task 2. Inspect the network traffic of a network interface with tcpdump</h2>

In this task, we'll use tcpdump to filter live network packet traffic on the eth0 interface using the command "sudo tcpdump -i eth0 -v -c5"

This command will run tcpdump with the following options:

- <b>-i eth0: Capture data specifically from the eth0 interface.</b>
- <b>-v: Display detailed packet data.</b>
- <b>-c5: Capture 5 packets of data.</b>

<p align="center">
Now, let's take a detailed look at the packet information that this command has returned: <br/>
<img src="https://imgur.com/CjNEc71.png"<br />

<h3>Exploring network packet details</h3>

1. In this example, we’ll identify some of the properties that tcpdump outputs for the packet capture data we’ve just seen. For example, tcpdump reported that it was listening on the eth0 interface, and it provided information on the link type and the capture size in bytes:
<p align="center">
<img src="https://imgur.com/5G1C1S1.png"<br />

2.	On the next line, the first field is the packet's timestamp, followed by the protocol type, IP:
<p align="center">
<img src="https://imgur.com/gsOEwZP.png"<br />

3. The verbose option, -v, has provided more details about the IP packet fields, such as TOS, TTL, offset, flags, internal protocol type (in this case, TCP (6)), and the length of the outer IP packet in bytes:
<p align="center">
<img src="https://imgur.com/6XcgNke.png"<br />

4.	In the next section, the data shows the systems that are communicating with each other. The direction of the arrow (>) indicates the direction of the traffic flow:
<p align="center">
<img src="https://imgur.com/fZ1vqMA.png"<br />

5.	The remaining data filters the header data for the inner TCP packet:
<p align="center">
<img src="https://imgur.com/i7LrFx5.png"<br />

The flags field identifies TCP flags. In this case, the P represents the push flag and the period indicates it's an ACK flag. This means the packet is pushing out data.
The next field is the TCP checksum value, which is used for detecting errors in the data. This section also includes the sequence and acknowledgment numbers, the window size, and the length of the inner TCP packet in bytes.


<h2>Task 3. Capture network traffic with tcpdump</h2>

In this task, we will use tcpdump to save the captured network data to a packet capture file by using a filter and other tcpdump configuration options to save a small sample that contains only web (TCP port 80) network packet data.
1.	Capture packet data into a file called capture.pcap with the following command: sudo "tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &"

This command will run tcpdump in the background with the following options:

- <b>-i eth0: Capture data from the eth0 interface.</b>
- <b>-nn: Do not attempt to resolve IP addresses or ports to names.This is best practice from a security perspective, as the lookup data may not be valid. It also prevents malicious actors from being alerted to an investigation.</b>
- <b>-c9: Capture 9 packets of data and then exit.</b>
- <b>port 80: Filter only port 80 traffic. This is the default HTTP port.</b>
- <b>-w capture.pcap: Save the captured data to the named file.</b>
- <b>&: This is an instruction to the Bash shell to run the command in the background.</b>
- <b>-c9: Capture 9 packets of data and then exit.</b>

2.	Use curl to generate some HTTP (port 80) traffic using the following command: "curl opensource.google.com"

When the curl command is used like this to open a website, it generates some HTTP (TCP port 80) traffic that can be captured.

3.	Verify that packet data has been captured using the following command: "ls -l capture.pcap"

<h2>Task 4. Filter the captured packet data</h2>
In this task, we will use tcpdump to filter data from the packet capture file we saved previously. The tcpdump command will enable us to filter the packet header data from the capture.pcap capture file using the following command: sudo "tcpdump -nn -r capture.pcap -v"

This command will run tcpdump with the following options:

- <b>-nn: Disable port and protocol name lookup.</b>
- <b>-r: Read capture data from the named file.</b>
- <b>-v: Display detailed packet data.</b>

note that we must specify the "-nn" switch again here, as we want to make sure tcpdump does not perform name lookups of either IP addresses or ports, since this can alert threat actors.

<p align="center">
This command returns output similar to the following: <br/>
<img src="https://imgur.com/ZtzIL8i.png"<br />






In this task, network analyst must identify the network interfaces that can be used to capture network packet data by using the command "sudo tcpdump -D"(can also use "sudo ifconfig") to identify the interfaces that are available. 

<p align="center">
This command returns output similar to the following: <br/>
<img src="https://imgur.com/ZtzIL8i.png"<br />

<h2>Stage I: Define business and security objectives</h2>
A shopping application like this will need to process payments. Based on this description, we know certain technologies are required to keep information private and secure and that everything will need to be compliant with PCI-DSS. Accordingly, the DevSecOps team will have the analyze the following requirements: 

- <b>Users can create member profiles internally or by connecting external accounts.</b>
- <b>The app must process financial transactions.</b>
- <b>The app should be in compliance with PCI-DSS.</b>


