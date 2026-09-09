network:
	version: 2
	renderer: networkd
	ethernets:
		YOUR_OWN_INTERFACE:
			dhcp4: no
			addresses:
				- YOUR_DESIRED_STATIC_IP_ADDRESS
			routes:
				- to: default
				  via: YOUR_ROUTER_PANEL_IP
			nameservers:
				addresses:
					- 127.0.0.1
					- 1.1.1.1