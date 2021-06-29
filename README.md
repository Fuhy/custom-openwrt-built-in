# custom-openwrt-built-in
Some useful files for quickly set up v2ray on a self built OpenWrt image.

It's only some shell scripts and config files here. If you want to use the files, you need to built your OpenWrt image with the necessary module like openwrt-v2ray, git and git-http, curl, etc.

```shell
.
├── etc
│   ├── init.d
│   │   ├── tproxyrule    # init.d script to automatic enable transparent proxy
│   │   └── v2ray         # init.d script to automatic start v2ray when reboot
│   └── uci-defaults
│       ├── enable_dhcp_on_first_boot   # enable dhcp/wifi so you can connect the device when the first boot
│       ├── enable_ip_forward        # require if you want it to be the gateway
│       └── set_zsh_as_default_shell  # remenber to include zsh into the image
├── root  # /root is ~/ directory, set up some useful script here.
│   ├── export_v2ray_env_var.sh
│   └── install_oh_my_zsh.sh
└── usr
    └── local
        ├── bin
        │   ├── flush_iptable_tproxy     # called by init.d/tproxyrule
        │   └── restore_iptable_tproxy   # called by init.d/tproxyrule
        ├── etc
        │   └── v2ray # require V2RAY_LOCATION_CONFIG=/usr/local/share/v2ray
        │       └── config.json
        └── share
            └── v2ray # require V2RAY_LOCATION_ASSET=/usr/local/share/v2ray
                ├── geoip.dat
                └── geosite.dat
```

`geoid.dat` and `geosite.dat` is downloaded from [Loyalsoldier](https://github.com/Loyalsoldier)/**[v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)**. Need to update it frequently.

`config.json` and related iptable setup scripts is used for set to transparent proxy. Basically according to the guide: [新 V2Ray 白话文指南 - 透明代理](https://guide.v2fly.org/app/tproxy.html)

I used the v2ray-core from the project [kuoruan](https://github.com/kuoruan)/**[openwrt-v2ray](https://github.com/kuoruan/openwrt-v2ray)**. The author has also developed the LuCI for it [luci-app-v2ray](https://github.com/kuoruan/luci-app-v2ray).
