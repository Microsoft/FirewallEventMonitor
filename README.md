Note: FirewallEventMonitor is now archived.

# Firewall Event Monitor

Firewall Event Monitor listens for Events generated by the Microsoft Windows Hyper-V Virtual Filter Protocol (VFP) extension. These Events are generated whenever a Software Defined Networking (SDN) Firewall Rule is applied to traffic going through a Hyper-V Virtual Switch.

Events captured can be filtered by:
1. The IP Address of the traffic source and destination.
2. The Id (GUID) of the FirewallRule that allowing or blocking the traffic.

## Running Firewall Event Monitor

FirewallEventMonitor.exe
    
    -TimeLimit <seconds> : Stop after running for the specified time.
    
    -EventThrottle <count> : Throttle events captured per second. Default: 10,000 Events per second.
    
    -Output <output1,output2,...> : Comma-delimited list of desired output.
        Console : Print to console.
        File : Write to file on disk.
    
    -Directory <path> : Location of log file (if -Output generates one). Default: current directory.
    
    -IP <address1,address2,...> : Fitler for the comma-delimited list of addresses.
        Note: Events without the specified IP address(es) in either source or destination are ignored.
        
    -Rule <guid1,guid2,...> : Fitler for the comma-delimited list of Rule Ids.
        Note: Events without the specified Rule Ids are ignored.
        Note: Must be valid Guids. XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX or "{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"
    
## Example Output

    [20170907 224228] Inbound Allow rule status = 0x0
      port {id = 4, portName = 07312833-61E0-4D4E-BB4C-BFC46E86D345, portFriendlyName = NULL}
      flow {src = 192.168.100.21, dst = 192.168.100.22, protocol = ICMPv4, icmp type = V4EchoRequest}
      rule {id = 43cff06e-a520-4ad3-9fd9-1894f4a3489b, layer = FW_CONTROLLER_LAYER_ID, group = FW_GROUP_IPv4_IN_ID, gftFlags = 0}

## Examples

* Filter by IP Addresses

    ```
    FirewallEventMonitor.exe -IP 192.168.0.22,192.168.0.23
    ```
    
* Filter by Rule Id

    ```
    FirewallEventMonitor.exe -Rule 391e5f07-0039-42dc-9734-abb5d633aadd,38222F79-1C3B-41F2-83B3-9FE0337AD548
    ```

* Log Events to a file in C:\temp

    ```
    FirewallEventMonitor.exe -Output Console,File -Directory C:\temp
    ```
    

## Testing

Tests are built using the Visual Studio Unit Test Framework.

## Branches

- Releases are made to the [master][] branch.

[master]: https://github.com/Microsoft/FirewallEventMonitor/tree/master

---

This project has adopted the [Microsoft Open Source Code of Conduct][]. For more
information see the [Code of Conduct FAQ][] or contact
[opencode@microsoft.com][] with any additional questions or comments.

[Microsoft Open Source Code of Conduct]: https://opensource.microsoft.com/codeofconduct/
[Code of Conduct FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[opencode@microsoft.com]: mailto:opencode@microsoft.com
