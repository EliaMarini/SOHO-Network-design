<h1>SOHO Network design</h1>
<br />

<h1>Scenario</h1>
<br />
<p>A company is intending to open a branch office and you are assigned to design the network for the branch. The branch office is 
intended to operate separate from the head office networ.
Being a small network, the company has the following requirements during implementation:
<ul>
  <li>One router and one switch to be used</li>
  <li>3 departments (Admin/IT, Finance/HR, Customer service/Reception)</li>
  <li>Each department is required to be in different VLANS</li>
  <li>Host devices in the network are required to obtain IPv4 address automatically</li>
  <li>Devices in all the departments are required to communicate with each other</li>
</ul>

Assume the ISP gave out a base network of 192.168.1.0, you as the young network engineer who has been hired,
design and implement a network considering the above requirements.
</p>
<br />

<h1>Network architecture</h1>

<br />
<img width="1292" height="654" alt="NetworkDesign" src="https://github.com/user-attachments/assets/57715ce9-3d77-41ec-bc4d-fa9a73465842" />

<br />
<p>This is the network design with the required network devices and a subnet for each department</p>
<br />

<h1>Subnetting</h1>

<br />
<p>The base network is 192.168.1.0 with a default /24 subnet mask. 3 subnets are needed so i applied a /26 subnet mask. Each subnets contains 62 usable ip addresses.
  
1st subnet
<ul>
<li>Network ID 192.168.1.0</li>
<li>First usable ip 192.168.1.1</li>
<li>Last usable ip 192.168.1.62</li>
<li>Broadcast address 192.168.1.63</li>
</ul>

2nd subnet

<ul>
<li>Network ID 192.168.1.64</li>
<li>First usable ip 192.168.1.65</li>
<li>Last usable ip 192.168.1.126</li>
<li>Broadcast address 192.168.1.127</li>
</ul>

3rd subnet

<ul>
<li>Network ID 192.168.1.128</li>
<li>First usable ip 192.168.1.129</li>
<li>Last usable ip 192.168.1.190</li>
<li>Broadcast address 192.168.1.191</li>
</ul>

</p>

<br />

<h1>VLANs setup</h1>

<br />
<p>A VLAN for each department is required. These are the VLANs that i created:
<ul>
  <li>VLAN 10 for Admin/IT</li>
  <li>VLAN 20 for Finance/HR</li>
  <li>VLAN 30 for Customer support/Reception</li>
</ul>
<br />
<img width="502" height="158" alt="Vlan_config1" src="https://github.com/user-attachments/assets/e34e0af4-07ab-4433-8a68-5c33edc14520" />
<br />
Then i assigned to each switch interface the proper VLAN.
<br />
<img width="866" height="193" alt="Vlan_config2" src="https://github.com/user-attachments/assets/bb4ca0ad-7ea2-467d-a9fe-7b254a766c6d" />
<br />
<img width="635" height="303" alt="Vlan_config3" src="https://github.com/user-attachments/assets/be62f6dd-96af-4e2e-8b8e-3e35a70eba38" />
<br />
I created the trunk interface on the switch that will be connected to the router
<br />
<img width="441" height="118" alt="Vlan_config4" src="https://github.com/user-attachments/assets/69bad3a1-7b03-4cc8-ab81-3b315447db01" />
<br />
Using the "show running-config" command i checked the VLANs configuration
<br />
<img width="391" height="650" alt="showrunningconfig" src="https://github.com/user-attachments/assets/79cdbb35-d495-476a-9c9a-678292f60ad3" />

</p>
<br />

<h1>Inter VLAN rounting</h1>
<br />
<p>The next step is to activate the inter vlan routing by creating sub-interfaces on the router
<br />
<img width="736" height="506" alt="intervlanrouting" src="https://github.com/user-attachments/assets/4e6e43ae-dc67-4a95-a910-3b45a068c1e3" />
<br />

For each vlan these are going to be the default gateways:
<ul>
  <li>VLAN 10 192.168.1.1</li>
  <li>VLAN 20 192.168.65</li>
  <li>VLAN 30 192.168.129</li>
</ul>
</p>
<br />

<h1>DHCP service</h1>
<br />
<p>Hosts needs to obtain automatically IP configuration, to do so i configured the DHCP service on the router
<br />
  <img width="466" height="339" alt="serverdhcp" src="https://github.com/user-attachments/assets/05f6b38d-03cb-4260-bb54-2d03da81cad0" />
<br />
 Then i configured each host to use the DHCP service
<br />
  <img width="1085" height="561" alt="HostFinalConfig" src="https://github.com/user-attachments/assets/89f7cfe4-2212-4712-bb31-ce65819b1e79" />
<br />
</p>

<h1>Wireless configuration</h1>
<br />
<p>Lastly each department must have a wireless network. The following images show the configurations of the access point and of the wireless laptop in the customer service/reception department
<br />
<img width="1100" height="495" alt="access point config" src="https://github.com/user-attachments/assets/264f04e2-4966-40a4-b193-5f8d9237db0b" />
<br />
<img width="1094" height="525" alt="wirelessdevconfig" src="https://github.com/user-attachments/assets/21d4b232-431f-461c-b120-2411a20fb705" />

</p>
<br />

<h1>Connectivity test</h1>
<br />
<p>By using the ping command i tested the comunication between devices in different subents. These are the configurations of each device and the following results.
<br />
  <img width="1093" height="278" alt="Connectivitytest1" src="https://github.com/user-attachments/assets/c3d6956f-f7a8-4646-8c23-982a8a3dbe47" />
  <br />
  <img width="1104" height="274" alt="Connectivitytest2" src="https://github.com/user-attachments/assets/8ad163ce-6157-491f-ae58-53490adb8afb" />
  <br />
  <img width="1094" height="281" alt="Connectivitytest3" src="https://github.com/user-attachments/assets/3252b6e0-d1c1-431e-be3a-bb48f28f2282" />
  <br />
  <img width="485" height="356" alt="ping" src="https://github.com/user-attachments/assets/331fbe44-2e00-404f-adf4-a0870f99c1ae" />


</p>
