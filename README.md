# Practice-Cisco-Packet-tracer
My first network being built

Project 1: Setting up a LAN between 4 computers
Purpose is to learn how to configure computers on a basic network

1st hookup 4 computers to two switches and one router
Use a coopper straight and use gigabit internet to connect the switch and the router

To turn the arrows from red to green configure the router port

using the router command line interface (how to configure g0/0) {
	enter "No" for intial configure dialouge  
	Now we are in the user execution mode	
	>> type "enable">> to get into the privillage mode
	next >> type "configure terminal" >> Now we are in global configuartion mode
	Next configure interface >> type "interface g0/0">>
	Next >> type "ip address 192.168.1.1 then type the submask of " 255.255.255.0">>
	Next > type "  no shutdown "

}
Next type "Exit" to enter global interface
Go back to global terminal
configure g0/1 {
	>> type "interface g0/1">> have to configure for two different networks
	>> type "ip address 192.168.2.1" then type the submask og " 255.255.255.0"
	>> then type "No shutdown "
}
Close terminal and check for green arrows if not double check steps

Next configure PC0

Click PC/desktop/ip configuration
	{
	>>type ip address "192.168.1.10"
	default gateway of corresponding router " 192.168.1.1
}
Next configure PC1 
{
	>>type ip address "192.168.1.11"
	default gateway of corresponding router " 192.168.1.1
}

Next configure PC2 
{
	>>type ip address "192.168.2.10"
	default gateway of corresponding router " 192.168.2.1
}
	
Next configure PC3 
{
	>>type ip address "192.168.2.11"
	default gateway of corresponding router " 192.168.2.1
}

Router ip address g0/0 -192.168.1.1
Router ip address g0/1 -192.168.2.1

PC 0 ip address is- 192.168.1.10 (gateway to g0/0)
pc 1 ip address is- 192.168.1.11 (gateway to g0/0)
pc 2 ip address is - 192.168.2.10 (gateway to g0/1)
pc 3 ip address is -  192.168.2.11 (gateway to g0/1)
	
Next part setting up VLAN 
Purpose: To segment networks by splitting the switch into isolated networks
Open router 0 command line
Access the configure terminal ip address and erase the single ip address assigned to it 
{
enable the router/then type configure terminal/
>> type " interface g0/0" >> type " no ip address"
}

Next to slice the g0/0 port into two virtual sub interfaces and to be the separate gateways for the two vlans 
in the same commandline type {
>> type "interface g0/0.10" 
then>> type encapsulation dot1Q 10
then type ip address 192.168.1.1 255.255.255.0
exit
}
Next create and configure a Vlan 20 sub interface
Go back to router config # then you have to create a second virtual gateway for PC1 new network
{  >>type in “ interface g0/0.20”
Then type >> “encapsulation dot 1Q 20”
Then type >> “ip address 192.168.3.1 255.255.255.0”
Then type exit
}
 Summary of this key step is that there was one physical cord connecting the router, so I split it virtually into the two gateways of (g0/0.10 and g0/0.20). These handle two different networks for one single cable at the same time.
Side note encapsulation gave the router instructions on how to read the tag. It tells the router if a packet has this number on it send it through.

Next configure switches check to make sure the pcs are plugged into the right internet cables by hovering over the green triangles after turning on preferences and always show port labels.
Next step is setting up the VLANS on the switch
We have to tell the switch that the VLAN’s exist {
Click switch and open up command line 
>> type “enable” >> “configure terminal”>> type “vlan 10”>> type “name Net1” >> type “vlan 20”>> type “name “NET3” >> type “exit”
}
Next is to assign the access ports from the PCs
Enter this in the switch/configure command line. This puts PC- into Vlan 10 {
Type “ interface f0/1” >> type “switchport mode access” >> type “switchport access vlan 10”>> type “exit”


This puts PC1 into VLAN 20 {
>>Type “Interface f0/2” >> type “ switchport mode access”>> type “switchport access vlan 20”>> type “exit”
}
This next step sets up the Trunk port. This gives them a way to send both of them up to the router. We turn the port connect to a router to a trunk.
Enter this into switch configuration{
>>type “interface g0/1>> type “switchport mode trunk>> type “exit”
}
Issues that I ran into I got 100% packet loss after trying to ping each other computer
Fixed it by fixing the ip address of PC1
Open pc1 command line and type “ping 192.168.3.1 





