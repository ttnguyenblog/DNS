
# Script add new DNS

## Example:
```bash
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
```

## Add Record DNS Forward Lookup Zone
```bash
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
```

## Add Record DNS Reverse Lookup Zone
```bash
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
```
## Thêm DNS thứ 3
```bash
$networkAdapters = Get-NetAdapter | Where-Object { $_.Status -eq "Up" }
foreach ($adapter in $networkAdapters) {
    # Lấy thông tin DNS hiện tại của adapter
    $currentDns = (Get-DnsClientServerAddress -InterfaceAlias $adapter.Name).ServerAddresses

    # Kiểm tra nếu DNS thứ 3 chưa có trong danh sách
    if ($currentDns.Count -lt 3) {
        # Thêm DNS thứ 3 vào
        $newDns = $currentDns + "8.8.8.8"  # Thay bằng DNS server bạn muốn thêm
        Set-DnsClientServerAddress -InterfaceAlias $adapter.Name -ServerAddresses $newDns
        Write-Output "DNS server thứ 3 đã được thiết lập cho adapter $($adapter.Name)."
    } else {
        Write-Output "Adapter $($adapter.Name) đã có đủ 3 DNS servers."
    }
}
```
## Xoá hàng loạt DNS

```bash
$ServerFQDN = "ad2012.mangvanphong.com" #Keep the dot (.) at the end
$ServerHostname = "hnx-ad-01"
$IPAddress = "100.64.6.53"

$Zones = Get-DnsServerZone | Where-Object { $_.ZoneType -eq "Primary" } |
Select-Object -ExpandProperty ZoneName

foreach ($Zone in $Zones) {
    Get-DnsServerResourceRecord -ZoneName $Zone | Where-Object { 
        $_.RecordData.IPv4Address -eq $IPAddress -or
        $_.RecordData.NameServer -eq $ServerFQDN -or
        $_.RecordData.DomainName -eq $ServerFQDN -or
        $_.RecordData.HostnameAlias -eq $ServerFQDN -or
        $_.RecordData.MailExchange -eq $ServerFQDN -or
        $_.HostName -eq $ServerHostname
    }
}



$ServerFQDN = "dc01-2019.exoip.local." #Keep the dot (.) at the end
$ServerHostname = "dc01-2019"
$IPAddress = "192.168.1.51"

$Zones = Get-DnsServerZone | Where-Object { $_.ZoneType -eq "Primary" } |
Select-Object -ExpandProperty ZoneName

foreach ($Zone in $Zones) {
    Get-DnsServerResourceRecord -ZoneName $Zone | Where-Object { 
        $_.RecordData.IPv4Address -eq $IPAddress -or
        $_.RecordData.NameServer -eq $ServerFQDN -or
        $_.RecordData.DomainName -eq $ServerFQDN -or
        $_.RecordData.HostnameAlias -eq $ServerFQDN -or
        $_.RecordData.MailExchange -eq $ServerFQDN -or
        $_.HostName -eq $ServerHostname
    } | Remove-DnsServerResourceRecord -ZoneName $Zone -Force -WhatIf
}

```
