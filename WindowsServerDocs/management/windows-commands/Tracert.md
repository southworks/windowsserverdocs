---
title: Tracert
description: "Windows Commands topic for **** -- "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9032a032-2e5e-49d4-9e86-f821600e4ba6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Tracert

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Determines the path taken to a destination by sending Internet Control Message Protocol (ICMP) Echo Request or ICMPv6 messages to the destination with incrementally increasing Time to Live (TTL) field values. The path displayed is the list of near/side router interfaces of the routers in the path between a source host and a destination. The near/side interface is the interface of the router that is closest to the sending host in the path. Used without parameters, tracert displays help.   
## Syntax  
```  
tracert [/d] [/h <MaximumHops>] [/j <HostList>] [/w <Timeout>] [/R] [/S <SrcAddr>] [/4][/6] <TargetName>  
```  
### Parameters  
|Parameter|Description|  
|-------------|---------------|  
|/d|Prevents **tracert** from attempting to resolve the IP addresses of intermediate routers to their names. This can speed up the display of **tracert** results.|  
|/h <MaximumHops>|Specifies the maximum number of hops in the path to search for the target (destination). The default is 30 hops.|  
|/j <HostList>|Specifies that Echo Request messages use the Loose Source Route option in the IP header with the set of intermediate destinations specified in *HostList*. With loose source routing, successive intermediate destinations can be separated by one or multiple routers. The maximum number of addresses or names in the host list is 9. The *HostList* is a series of IP addresses (in dotted decimal notation) separated by spaces. Use this parameter only when tracing IPv4 addresses.|  
|/w <Timeout>|Specifies the amount of time in milliseconds to wait for the ICMP Time Exceeded or Echo Reply message corresponding to a given Echo Request message to be received. If not received within the time-out, an asterisk (*) is displayed. The default time-out is 4000 (4 seconds).|  
|/R|Specifies that the IPv6 Routing extension header be used to send an Echo Request message to the local host, using the destination as an intermediate destination and testing the reverse route.|  
|/S <SrcAddr>|Specifies the source address to use in the Echo Request messages. Use this parameter only when tracing IPv6 addresses.|  
|/4|Specifies that Tracert.exe can use only IPv4 for this trace.|  
|/6|Specifies that Tracert.exe can use only IPv6 for this trace.|  
|<TargetName>|Specifies the destination, identified either by IP address or host name.|  
|/?|Displays Help at the command prompt.|  
## Remarks  
-   This diagnostic tool determines the path taken to a destination by sending ICMP Echo Request messages with varying Time to Live (TTL) values to the destination. Each router along the path is required to decrement the TTL in an IP packet by at least 1 before forwarding it. Effectively, the TTL is a maximum link counter. When the TTL on a packet reaches 0, the router is expected to return an ICMP Time Exceeded message to the source computer. Tracert determines the path by sending the first Echo Request message with a TTL of 1 and incrementing the TTL by 1 on each subsequent transmission until the target responds or the maximum number of hops is reached. The maximum number of hops is 30 by default and can be specified using the **/h** parameter. The path is determined by examining the ICMP Time Exceeded messages returned by intermediate routers and the Echo Reply message returned by the destination. However, some routers do not return Time Exceeded messages for packets with expired TTL values and are invisile to the tracert command. In this case, a row of asterisks (*) is displayed for that hop.  
-   To trace a path and provide network latency and packet loss for each router and link in the path, use the **pathping** command.  
-   This command is available only if the Internet Protocol (TCP/IP) protocol is installed as a component in the properties of a network adapter in Network Connections.  
## <a name="BKMK_Examples"></a>Examples  
To trace the path to the host named corp7.microsoft.com, type:  
```  
tracert corp7.microsoft.com  
```  
To trace the path to the host named corp7.microsoft.com and prevent the resolution of each IP address to its name, type:  
```  
tracert /d corp7.microsoft.com  
```  
To trace the path to the host named corp7.microsoft.com and use the loose source route 10.12.0.1/10.29.3.1/10.1.44.1, type:  
```  
tracert /j 10.12.0.1 10.29.3.1 10.1.44.1 corp7.microsoft.com  
```  
## Additional references  
-   [Command-Line Syntax Key](Command-Line-Syntax-Key.md)  