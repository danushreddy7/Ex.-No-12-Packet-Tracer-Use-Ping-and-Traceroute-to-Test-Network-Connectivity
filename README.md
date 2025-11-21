# Ex. No: 12 – Packet Tracer: Use Ping and Traceroute to Test Network Connectivity
# Date: 21/11/2025
________________________________________<br>
# Objective
To test and restore IPv4 and IPv6 network connectivity using diagnostic commands (ping and tracert), identify faults, and verify proper routing between end devices in a dual-stack (IPv4 + IPv6) topology.<br>
Tasks:<br>
•	Use ipconfig and ipv6config to collect addressing information.<br>
•	Use ping and tracert to test connectivity.<br>
•	Locate and fix connectivity issues.<br>
•	Verify successful restoration of both IPv4 and IPv6 communication.<br>
________________________________________<br>
# Apparatus / Tools Required
• Cisco Packet Tracer<br>
• 3 Routers (R1, R2, R3 – 2911 or equivalent)<br>
• 4 PCs (PC1–PC4)<br>
• Copper straight-through and serial DCE/DTE cables<br>
________________________________________<br>
# Network Topology Diagram:
<img width="1919" height="1056" alt="506504508-bc2f5902-2b8f-4f68-868c-158978cb12f0" src="https://github.com/user-attachments/assets/1540fe16-927f-49b1-9fbe-de2f7f5f9fa5" />

________________________________________<br>
Addressing Table<br>
Device	Interface	IPv4 Address / Subnet Mask	IPv6 Address / Prefix	Default Gateway<br>
R1	G0/0	10.10.1.97 / 255.255.255.224	2001:db8:1:1::1/64	N/A<br>
R1	S0/0/1	10.10.1.6 / 255.255.255.252	2001:db8:1:2::2/64	N/A<br>
R2	S0/0/0	10.10.1.5 / 255.255.255.252	2001:db8:1:2::1/64	N/A<br>
R2	S0/0/1	10.10.1.9 / 255.255.255.252	2001:db8:1:3::1/64	N/A<br>
R3	G0/0	10.10.1.17 / 255.255.255.240	2001:db8:1:4::1/64	N/A<br>
R3	S0/0/1	10.10.1.10 / 255.255.255.252	2001:db8:1:3::2/64	N/A<br>
PC1	NIC	(DHCP/Manual IPv4)	(Auto IPv6)	R1 G0/0<br>
PC2	NIC	(DHCP/Manual IPv6)	(Auto IPv6)	R1 G0/0<br>
PC3	NIC	(DHCP/Manual IPv4)	(Auto IPv6)	R3 G0/0<br>
PC4	NIC	(DHCP/Manual IPv6)	(Auto IPv6)	R3 G0/0<br>
________________________________________<br>
# Procedure for Students – Use Ping and Traceroute (13.2.7)
Download the Activity File<br>
Ensure the file 13.2.7-packet-tracer---use-ping-and-traceroute-to-test-network-connectivity.pka is saved in an accessible folder (e.g., Downloads or Documents).<br>
________________________________________
# Open Cisco Packet Tracer
Launch Cisco Packet Tracer → Click File → Open...<br>
Select the .pka file and click Open.<br>
________________________________________<br>
# Start the Activity
The pre-configured topology (R1–R3 and PCs PC1–PC4) will load automatically.<br>
Follow the right-hand Instruction Panel for activity steps.<br>
________________________________________
# Part 1: Test and Restore IPv4 Connectivity<br>
# Step 1: Verify IPv4 Configuration<br>
1.	Click PC1, open Command Prompt, and type:<br>
2.	ipconfig /all<br>
Note IPv4 address, mask, and gateway.<br>
3.	Repeat on PC3 and record data in the Addressing Table.<br>
________________________________________<br>
# Step 2: Test and Locate IPv4 Issues
1.	From PC1, ping PC3:<br>
2.	ping <PC3 IPv4 address><br>
Observe failure (expected).<br>
3.	From PC1, trace the route:<br>
4.	tracert <PC3 IPv4 address><br>
Record the last reachable hop.<br>
5.	Repeat the same from PC3 to PC1.<br>
________________________________________<br>
# Step 3: Analyze and Diagnose
•	On R1, run:<br>
•	show ip interface brief<br>
•	show ip route<br>
Identify incorrect interfaces or missing routes.<br>
•	Repeat on R2 and R3.<br>
Compare configurations with documentation to locate the misconfigured interface or subnet.<br>
________________________________________<br>
# Step 4: Implement Fix
Reconfigure the faulty interface or routing entry. Example:<br>
configure terminal<br>
interface s0/0/1<br>
 ip address 10.10.1.6 255.255.255.252<br>
 no shutdown<br>
end<br>
copy running-config startup-config<br>
________________________________________<br>
# Step 5: Verify IPv4 Restoration
From PC1:<br>
ping <PC3 IPv4 address><br>
From PC3:<br>
ping <PC1 IPv4 address><br>
Both pings should now succeed.<br>
________________________________________
# Part 2: Test and Restore IPv6 Connectivity
# Step 1: Verify IPv6 Configuration
On PC2 and PC4, use:<br>
ipv6config /all<br>
Record IPv6 address, prefix, and gateway.<br>
________________________________________
# Step 2: Test and Trace IPv6 Connectivity
1.	From PC2, ping PC4:<br>
2.	ping 2001:db8:1:4::a<br>
Expected: Failure initially.<br>
3.	Trace route:<br>
4.	tracert 2001:db8:1:4::a<br>
Record last reachable IPv6 address.<br>
________________________________________
# Step 3: Diagnose and Correct IPv6 Faults
•	On routers, use:<br>
•	show ipv6 interface brief<br>
•	show ipv6 route<br>
Verify that interfaces are up and prefixes match documentation.<br>
•	Identify and correct errors (e.g., missing IPv6 address, shutdown interface).<br>
________________________________________
# Step 4: Implement and Verify IPv6 Restoration
1.	Correct any configuration errors using CLI.<br>
2.	Confirm end-to-end IPv6 connectivity with ping and tracert.<br>
________________________________________
# Verification and Testing Summary
Command	Purpose<br>
ipconfig /all	View IPv4 details<br>
ipv6config /all	View IPv6 details<br>
ping	Test reachability<br>
tracert	Trace route hops<br>
show ip interface brief	Verify IPv4 interface status<br>
show ipv6 interface brief	Verify IPv6 interface status<br>
________________________________________
# Output:
• Command outputs (ipconfig, ipv6config, ping, tracert) for PCs.<br>
• PC-1 and PC-3<br>
<img width="1915" height="1199" alt="506504670-83dba5a6-4583-406a-bc4e-1011c3ec96ff" src="https://github.com/user-attachments/assets/2cc0de88-aaed-4c4d-8851-f336100d7c51" /><br>
<img width="1915" height="1199" alt="506504670-83dba5a6-4583-406a-bc4e-1011c3ec96ff" src="https://github.com/user-attachments/assets/0030d48d-e25c-4e09-a487-f295b6fd38fc" /><br>

• PC-2 and PC-4<br>
<img width="1919" height="1199" alt="506528501-4bebf9fa-38e0-4764-954c-63c50aad2b8d" src="https://github.com/user-attachments/assets/948c3799-9795-4a5f-bbf1-ffc3f331cec9" /><br>
<img width="1919" height="1199" alt="506528501-4bebf9fa-38e0-4764-954c-63c50aad2b8d" src="https://github.com/user-attachments/assets/46bdf192-9b08-4813-a022-0dc6b483fef9" /><br>

• Router interface and routing tables.<br>
• R1<br>
<img width="1911" height="1055" alt="506504956-c3dfe0ca-c58c-4b10-a4d2-33977c566b8a" src="https://github.com/user-attachments/assets/6240ae73-df4c-415b-8c31-f00754d0ca2e" />

• R2<br>
<img width="1919" height="1043" alt="506505060-f67e5e25-8093-41fc-ae7b-4b1641925fd9" src="https://github.com/user-attachments/assets/d1e4b409-c12e-4162-bde1-0abf46191183" />

•R3<br>
<img width="1919" height="1058" alt="506505218-ada5eaf1-f379-44a4-9832-29eb2ef7a7b5" src="https://github.com/user-attachments/assets/55ddbca6-1a0e-444b-915f-b737f220713c" />

• Successful ping results after fixes.<br>
• PC-1 and PC-3<br>
<img width="1915" height="1199" alt="506504670-83dba5a6-4583-406a-bc4e-1011c3ec96ff" src="https://github.com/user-attachments/assets/7cd24588-a195-4db6-b76f-b49730bb7bbf" /><br>

<img width="1915" height="1199" alt="506504670-83dba5a6-4583-406a-bc4e-1011c3ec96ff" src="https://github.com/user-attachments/assets/264dc192-435d-45be-a260-c7bc058a4152" />

•PC-2 and PC-4:
<img width="1919" height="1199" alt="506527284-6a8d7f59-530e-456d-935c-00babc79b3b5" src="https://github.com/user-attachments/assets/d404ba9a-3081-4be4-899f-d815d180f6dd" /><br>

<img width="1919" height="1199" alt="506527284-6a8d7f59-530e-456d-935c-00babc79b3b5" src="https://github.com/user-attachments/assets/57651dd6-3af5-441a-a910-ff5cb5c740b8" />

• Activity Result<br>
<img width="1888" height="986" alt="image" src="https://github.com/user-attachments/assets/a5c98656-ebd6-4764-b284-04f313653b41" />


________________________________________<br>
# Result
IPv4 and IPv6 connectivity issues were diagnosed and resolved using ping and tracert commands. Routers and PCs achieved full dual-stack communication after correcting configuration errors, confirming network restoration and routing accuracy.<br>

