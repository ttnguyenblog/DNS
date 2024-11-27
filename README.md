# DNS
Script add new DNS

##Example:

platform-api.apic-mgm01.nor.tpb.com             192.168.0.91
consumer-api.apic-mgm01.nor.tpb.com             192.168.0.91
cloud-admin-ui.apic-mgm01.nor.tpb.com           192.168.0.91
api-manager-ui.apic-mgm01.nor.tpb.com           192.168.0.91
analytics-ingestion.apic-ana01.nor.tpb.com      192.168.0.92
analytics-client.apic-ana01.nor.tpb.com         192.168.0.92
portal-admin.apic-por01.nor.tpb.com             192.168.0.93
portal.apic-por01.nor.tpb.com                   192.168.0.93
apic-cli01.nor.tpb.com                          192.168.0.90
apic-mgm01.nor.tpb.com                          192.168.0.91
apic-ana01.nor.tpb.com                          192.168.0.92
apic-por01.nor.tpb.com                          192.168.0.93


##Add Record DNS Forward Lookup Zone
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "platform-api.apic-mgm01" -IPv4Address "192.168.0.91"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "consumer-api.apic-mgm01" -IPv4Address "192.168.0.91"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "cloud-admin-ui.apic-mgm01" -IPv4Address "192.168.0.91"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "api-manager-ui.apic-mgm01" -IPv4Address "192.168.0.91"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "analytics-ingestion.apic-ana01" -IPv4Address "192.168.0.92"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "analytics-client.apic-ana01" -IPv4Address "192.168.0.92"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "portal-admin.apic-por01" -IPv4Address "192.168.0.93"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "portal.apic-por01" -IPv4Address "192.168.0.93"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "apic-cli01" -IPv4Address "192.168.0.90"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "apic-mgm01" -IPv4Address "192.168.0.91"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "apic-ana01" -IPv4Address "192.168.0.92"
Add-DnsServerResourceRecordA -ZoneName "nor.tpb.com" -Name "apic-por01" -IPv4Address "192.168.0.93"


##Add Record DNS Reverse Lookup Zone
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "91" -PtrDomainName "platform-api.apic-mgm01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "91" -PtrDomainName "consumer-api.apic-mgm01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "91" -PtrDomainName "cloud-admin-ui.apic-mgm01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "91" -PtrDomainName "api-manager-ui.apic-mgm01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "92" -PtrDomainName "analytics-ingestion.apic-ana01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "92" -PtrDomainName "analytics-client.apic-ana01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "93" -PtrDomainName "portal-admin.apic-por01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "93" -PtrDomainName "portal.apic-por01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "91" -PtrDomainName "apic-mgm01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "92" -PtrDomainName "apic-ana01.nor.tpb.com"
Add-DnsServerResourceRecordPtr -ZoneName "0.168.192.in-addr.arpa" -Name "93" -PtrDomainName "apic-por01.nor.tpb.com"
