![Wifidog icon](http://dev.wifidog.org/chrome/site/wifidog.png)
# Wifidog Auth Server [![MIT License][license-svg]][license-url]
	This is auth server for wifidog, it can use with wifidog gateway.
# HTTP interface of the wifidog auth server.
## Ping
### Request URL 
	http://$auth_server:$port/ping?gw_id=$gw_id&sys_uptime=$sys_uptime&sys_memfree=$sys_memfree&sys_load=$sys_load&wifidog_uptime=$wifidog_uptime
|Url Param | Param Description |wifidog version|
|------|-----|----|
|gw_id| wifi-dog gateway id|v1|
|sys_uptime|start up time of system|v1|
|sys_memfree|system memory free percent|v1|
|sys_load| system loadage|v1|
|wifidog_uptime|running time of wifi-dog gateway|v1|
|dev_id| device id| v2|
|cpu_usage|cpu usage percent value:0-100|v2|
|nf_conntrack_num| number of connection session| v2|
|out_rate|out rate of WAN interface,unit: bps| v2|
|in_rate|in rate of WAN interface,unit: bps| v2|
|online_devices| number of online device(auth device and unauth device)|v2|

**Note:** response is 'Pong ' with rules appended. rules is consist of host/network rule, ip white list, mac black list, mac white list and domain white list.

## Login
### Request URL 
	http://auth_server:port/login?gw_id=$gw_id&gw_address=$gw_address&gw_port=$gw_port&url=$url
|Url Param | Param Description |wifidog version|
|------|-----|----|
|gw_id| wifi-dog gateway id|v1|
|gw_address|wifidog gateway address for redirect|v1|
|gw_port|wifidog gatewat port for redirect|v1|
|url|url accessed of user-endpoint|v1|
|dev_id| device id| v2|
|mac|user-endpoint mac address|v2|

**Note**: After login success the url will be redirect to 'http://$gw_address:$gw_port/wifidog/auth?token=$token&url=$url' with HTTP code 302


## Auth
### Request URL 
	http://auth_server:port/auth?ip=$ip&mac=$mac&token=$tokrn&incoming=$incoming&outgoing=$outgoing&stage=$stage
|Url Param | Param Description |wifidog version|
|------|-----|----|
|ip| user-endpoint ip address|v1|
|mac|user-endpoint mac address|v1|
|token|token is created by interface 'login'|v1|
|incoming|download Octets|v1|
|outgoing|upload Octets|v1|
|stage|stage of auth. value is 'login' or 'counters'|v1|
|dev_id|device id|v2|
|uprate|up rate of user-endpoint, unit: bps|v2|
|downrate|down rate of user-endpoint, unit: bps|v2|
|gw_id| wifi-dog gateway id|v2|
|client_name|client name of user|v2|

**Note:** response should be 'Auth: 1' when param of stage is 'login'.
	'Auth: 0' for 'counters' and incoming is out of normal value.

## Portal
### Request URL 
	http://auth_server:port/portal?gw_id=$gw_id
|Url Param | Param Description |wifidog version|
|------|-----|----|
|gw_id| wifidog gateway id|v1|
|dev_id|device id|v2|

**Note**: this request will be redirect to fixed URL config or AD page for AD impression with HTTP code 302

## Auth flow
![auth flow icon](https://github.com/gityf/wifidog-auth-server/blob/master/doc/FlowDiagram.png)
## Wifidogr-gateway login to wifidog-auth-server and AAA-Radius server.
![auth flow icon](https://github.com/gityf/wifidog-auth-server/blob/master/doc/wifidog-gateway-auth-radius.png)




[license-url]: https://github.com/deuill/go-php/blob/master/LICENSE
[license-svg]: https://img.shields.io/badge/license-MIT-blue.svg
