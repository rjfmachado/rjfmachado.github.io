---
layout: post
section-type: post
title: Configuring your Hyper-V virtual switch for Network Address Translation
tags: [ 'Hyper-V', 'Networking' ]
category: tech
excerpt_separator: ""
---

This is a reminder for future Ricardo, as it was the 2nd time I searched for the information. After this configuration, Virtual Machines connected to this virtual switch will be able to access the Internet (not only) connection of the host.

````powershell
New-VMSwitch -SwitchName "SwitchName" -SwitchType Internal
New-NetIPAddress -IPAddress <NAT Gateway IP> -PrefixLength <NAT Subnet Prefix Length> -InterfaceIndex <ifIndex>
New-NetNat -Name nat -InternalIPInterfaceAddressPrefix <NAT Gateway IP Network>/<NAT Subnet Prefix Length>
````

Also, the following is a quick and dirty way to get the Hyper-V switch interface index required above.

````powershell
(Get-NetAdapter -InterfaceDescription Hyper-V*).ifIndex
````

Hope this helps.
Ricardo