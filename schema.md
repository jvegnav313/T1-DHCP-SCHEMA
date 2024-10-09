sequenceDiagram

    participant Server1
    participant Client
    participant Server2

note over Client: Begins initialization
    Client->>Server1 : DHCPDISCOVER
    Client->>Server2 : DHCPDISCOVER

    Note over Server2 : Determines configuration

    Server2->>Client : DHCPOFFER (Lease 8 hours)
    Note over Client : Collects Replies

    note over Server1: Determines configuration    
    Server1->>Client : DHCPOFFER (Lease 8 hours)





    Note over Client : Selects configuration

    Client->> Server1 : DHCPREQUEST
    Client->> Server2 : DHCPREQUEST
    
    Note over Server1 : Conmits configuration
    Server1 ->> Client: DHCPACK (IP Assigned)
    note over Client : Connects for 1 Hour
    note over Server1:  Server 1 goes down
    note over Server1, Client: 3 minute outage

    Client->>Server1 : DHCPDISCOVER
    Client->>Server2 : DHCPDISCOVER

    Note over Server2 : Determines configuration

    Server2->>Client : DHCPOFFER (Lease 8 hours)
    Note over Client : Collects Replies
    Client->>Server2: DHCPREQUEST
    note over Server2: Connmits configuration
    Server2->>Client: DHCPACK (IP Assigned)
    note over Client: Stay 12 hours
    note over Client: Disconnects 1 hour
    Client->> Server2: DHCPREQUEST (IP Renewal)
    Server2->> Client: DHCPACK (Lease renewal)

    note over Client: Stay 5 hours
    
    note over Client: Disconnect.