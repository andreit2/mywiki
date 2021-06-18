```
:local PingCount 5;
:local CheckIp1 8.8.8.8;
:local CheckIp8 8.8.4.4;
:local isp1 [/ping $CheckIp1 count=$PingCount interface="WAN1"];
:local isp2 [/ping $CheckIp8 count=$PingCount interface="WAN2"];
:local BackGw [/ip route get [find comment="kontech"] disable];
:if (($isp1=0) && ($isp2=$PingCount) && ($BackGw=true)) do={
/ip route disable [find comment="idea"];
/ip route enable [find comment="kontech"];
:delay 2
:log warning "Set routes to kontech";
/ip firewall connection remove [ find protocol~"tcp" ];
/ip firewall connection remove [ find protocol~"udp" ];
:delay 2
:log warning "Set routes to kontech";
}
:local MainGw [/ip route get [find comment="idea"] disable];
:if (($isp1=$PingCount) && ($MainGw=true)) do={
/ip route enable [find comment="idea"];
/ip route disable [find comment="kontech"];
:delay 2
:log warning "Set routes to idea";
/ip firewall connection remove [ find protocol~"tcp" ];
/ip firewall connection remove [ find protocol~"udp" ];
:delay 2
:log warning "Set routes to idea";
}
```
