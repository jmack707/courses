
Configure GSLB Sync on BIG-IP 5 and BIG-IP6
    DNS >> Setting GSLB General
       - Synchronize: "checked"
       - Group Name: acme

Create Listeners on BIG-IP 5 and BIG-IP6

    DNS >> Delivery >> Listeners >> Listeners List >> +
       - Set Name:                dns1.acme.com (BIG-IP 5)     dns2.acme.com (BIG-IP 6)
       - Set IP address:          10.1.10.99 (BIG-IP 5)        10.1.10.199 (BIG-IP 6)
       - Set VLAN and Tunnels:    external

Create Two Datacenters only on BIG-IP 5
    DNS >> GSLB >> Data Centers >> Data Center List >> +
       - Set Name:       DC1    
       - Set Name:       DC2

Create GTM Servers
    DNS >> GSLB >> Servers >> Server List
       - Set Name: gtm.dc1
       - Set Data Center: DC1

          -  BIG-IP System Device
           -    Name: bigip5.f5lab.local
           -    Address: 10.1.20.11
           -    Click: Add

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

Install Device Certificates
    Click Putty for bigip5
    Enter: bigip_add
        Password: admin

ADD BIGIP6(GTM2) to BIGIIP5(GTM1)
    Click Putty for BIGIP6
    Enter: gtm_add admin@10.1.20.11
        Password: admin

Create GTM Pool
    DNS >> GSLB >> Pools >> Pool List >> +
        Name: app1.gtm.pl
        Type: A
        Virtual Server:
            GSLB/A1/dc1.app1.https.vs
            GSLB/A1/dc2.app1.https.vs

        Name: app2.gtm.pl
        Type: A
        Virtual Server:
            GSLB/A1/dc1.app2.https.vs
            GSLB/A1/dc2.app2.https.vs

Create Wide IPs
    DNS >> GSLB >> Wide IPs >> Wide IP List>> +
        Name: app1.gslb.acme.com
        type: A
        Pool: app1.gtm.pl

        Name: app2.gslb.acme.com
        type: A
        Pool: app2.gtm.pl



DNS Sync https://support.f5.com/csp/article/K13734
