
Create Listeners 

    DNS >> Delivery >> Listeners >> Listeners List >> +
        Set Name:                dns1.acme.com (BIGIP A)     dns2.acme.com (BIGIP B)
        Set IP address:          10.1.10.99 (BIGIP A)        10.1.10.199 (BIGIP B)
        Set VLAN and Tunnels:    external

Create Datacenters
    DNS >> GSLB >> Data Centers >> Data Center List >> +
        Set Name:       DC1     DC2

Create GTM Servers
    DNS >> GSLB >> Servers >> Server List
        Set Name: gtm.dc1
        Set Data Center: DC1

            BIG-IP System Device
                Name: bigip5.f5lab.local
                Address: 10.1.20.11
                Click: Add

        Set Health Monitor: bigip


        Set Name: gtm.dc2
        Set Data Center: DC2

            BIG-IP System Device
                Name: bigip6.f5lab.local
                Address: 10.1.20.12
                Click: Add

        Set Health Monitor: bigip

Create LTM Servers        
    DNS >> GSLB >> Servers >> Server List
        Set Name: ltm.dc1
        Set Data Center: DC1

            BIG-IP System Device
                Name: bigip1.f5lab.local
                Address: 10.1.20.4
                Click: Add

        Set Health Monitor: bigip
        Set Virtual Server Discovery: Enable


        Set Name: ltm.dc2
        Set Data Center: DC2

            BIG-IP System Device
                Name: bigip2.f5lab.local
                Address: 10.1.20.5
                Click: Add

        Set Health Monitor: bigip5
        Set Virtual Server Discovery: Enable