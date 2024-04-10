# stun extension for openwrt, which inclides stund and stun-client

## Compile

```
# cd to OpenWrt sdk path
# Clone this repo
git clone https://github.com/TommyLau/stun.git package/network/stun

# Select Network -> stun-client and Network -> stund
make menuconfig

# Compile
make package/network/stun/compile V=s
```

## Usage

```
# you should have at least two routers as server and client
# run in stun server with two interface connected to the Internet
stund -v

# run in stun client to get your NAT type in response
stun-client {server IP} -v
```

## Result

```
Open = Open Internet
Independent Mapping, Independent Filter = Fullcone NAT
Independent Mapping, Address Dependent Filter = Restricted Cone NAT
Independent Mapping, Port Dependent Filter = Port-Restricted Cone NAT
Dependent Mapping = Symmetric NAT
Firewall = Symmetric Firewall
Blocked or could not reach STUN server = UDP Blocked
```

## Test

Use miwifi.com server for a test

```
stun-client stun.miwifi.com
```

## Firewall

Add a "Traffic Rules" in OpenWrt firewall

Name: Stun-Test
Source zone: wan
Destination zone: Device (input)
Action: accept

