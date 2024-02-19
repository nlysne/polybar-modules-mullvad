# [Polybar](https://polybar.github.io/) Modules for [Mullvad VPN](https://mullvad.net/)

| 💬 | A collection of other useful polybar modules maintained by the community can be found [here](https://github.com/polybar/polybar-scripts). |
|---|--------------------------------------|

These polybar modules use the [Mullvad CLI](https://mullvad.net/help/how-use-mullvad-cli/) `mullvad` to display details about the VPN connection and the established tunnel and allow to control certain settings from the module without having to open the Mullvad GUI. This version simplifies the text output to neatly report the status without extended information that may not be necessary (such as the exact tunnel location). It relies on characters typically included in [Nerd fonts](https://www.nerdfonts.com/), a family of extended character sets useful for many other polybar configurations.

![Example for 'disconnected.'](https://github.com/nlysne/polybar-modules-mullvad/tree/main/assets/screenshots/disconn.png?raw=true)
*An example of the module when Mullvad is disconnected, placed to the right of the WiFi module.*

![Example for 'connected.'](https://github.com/nlysne/polybar-modules-mullvad/tree/main/assets/screenshots/conn.png?raw=true)
*An example when Mullvad is connected.*

For a blocked connection, the tunnel protocol has to be toggled, as wireguard is not available for all locations.
For an unknown tunnel status, the polybar module will display the error message.

![Example for 'blocked.'](https://github.com/nlysne/polybar-modules-mullvad/tree/main/assets/screenshots/blocked.png?raw=true)

## Connection module

This polybar module displays the connection status (and potential errors) and allows for establishing a VPN connection, disconnecting and reconnecting with a simple click.

With the module configuration shown below, left-click toggles the connection state and right-click triggers a reconnect.

```ini
[module/vpn-mullvad-status]
type = custom/script
exec = ~/.config/polybar/scripts/vpn-mullvad.sh --status
click-left = ~/.config/polybar/scripts/vpn-mullvad.sh --toggle
click-right = ~/.config/polybar/scripts/vpn-mullvad.sh --reconnect
interval = 1
```

## Tunnel module

In a second polybar module, some tunnel details like the location of the VPN server currently connected to, as well as the used tunnel protocol can be viewed and changed.

The location is just the country shortcode if only the country was set (e.g. `at`) and city and country shortcodes if city was set (e.g. `vie-at`).

With the module configuration shown below, scrolling cycles through available server locations by country and left-click toggles the tunnel protocol (WireGuard, OpenVPN).

By default the status shown are the tunnel details (`--tunnel-details`), but it can be configured to only show the location (`--location`) or only the protocol (`--protocol`).

```ini
[module/vpn-mullvad-tunnel]
type = custom/script
exec = ~/.config/polybar/scripts/vpn-mullvad.sh --tunnel-details
click-left = ~/.config/polybar/scripts/vpn-mullvad.sh --toggle-protocol
scroll-up = ~/.config/polybar/scripts/vpn-mullvad.sh --previous
scroll-down = ~/.config/polybar/scripts/vpn-mullvad.sh --next
interval = 1
```
