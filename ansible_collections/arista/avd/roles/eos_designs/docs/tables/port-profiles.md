<!--
  ~ Copyright (c) 2023 Arista Networks, Inc.
  ~ Use of this source code is governed by the Apache License 2.0
  ~ that can be found in the LICENSE file.
  -->
=== "Table"

    | Variable | Type | Required | Default | Value Restrictions | Description |
    | -------- | ---- | -------- | ------- | ------------------ | ----------- |
    | [<samp>port_profiles</samp>](## "port_profiles") | List, items: Dictionary |  |  |  | Optional profiles to share common settings for connected_endpoints and/or network_ports.<br>Keys are the same used under endpoints adapters. Keys defined under endpoints adapters take precedence.<br> |
    | [<samp>&nbsp;&nbsp;-&nbsp;profile</samp>](## "port_profiles.[].profile") | String | Required, Unique |  |  | Port profile name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;parent_profile</samp>](## "port_profiles.[].parent_profile") | String |  |  |  | Parent profile is optional.<br>Port_profiles can refer to another port_profile to inherit settings in up to two levels (adapter->profile->parent_profile). |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;speed</samp>](## "port_profiles.[].speed") | String |  |  |  | Set adapter speed in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br>If not specified speed will be auto.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;description</samp>](## "port_profiles.[].description") | String |  |  |  | By default the description is built leveraging `<peer>_<peer_interface>`.<br>When set this key will overide the default value on the physical ports.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "port_profiles.[].enabled") | Boolean |  | `True` |  | Administrative state, setting to false will set the port to 'shutdown' in the intended configuration.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;mode</samp>](## "port_profiles.[].mode") | String |  |  | Valid Values:<br>- <code>access</code><br>- <code>dot1q-tunnel</code><br>- <code>trunk</code><br>- <code>trunk phone</code> | Interface mode. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;mtu</samp>](## "port_profiles.[].mtu") | Integer |  |  | Min: 68<br>Max: 65535 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;l2_mtu</samp>](## "port_profiles.[].l2_mtu") | Integer |  |  | Min: 68<br>Max: 65535 | "l2_mtu" should only be defined for platforms supporting the "l2 mtu" CLI<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;l2_mru</samp>](## "port_profiles.[].l2_mru") | Integer |  |  | Min: 68<br>Max: 65535 | "l2_mru" should only be defined for platforms supporting the "l2 mru" CLI<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;native_vlan</samp>](## "port_profiles.[].native_vlan") | Integer |  |  | Min: 1<br>Max: 4094 | Native VLAN for a trunk port.<br>If both `native_vlan` and `native_vlan_tag`, `native_vlan_tag` takes precedence.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;native_vlan_tag</samp>](## "port_profiles.[].native_vlan_tag") | Boolean |  | `False` |  | If both `native_vlan` and `native_vlan_tag`, `native_vlan_tag` takes precedence. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;trunk_groups</samp>](## "port_profiles.[].trunk_groups") | List, items: String |  |  |  | Required with `enable_trunk_groups: true`.<br>Trunk Groups are used for limiting VLANs on trunk ports to VLANs with the same Trunk Group.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "port_profiles.[].trunk_groups.[]") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;vlans</samp>](## "port_profiles.[].vlans") | String |  |  |  | Interface VLANs - if not set, the EOS default is that all VLANs are allowed for trunk ports, and VLAN 1 will be used for access ports. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;spanning_tree_portfast</samp>](## "port_profiles.[].spanning_tree_portfast") | String |  |  | Valid Values:<br>- <code>edge</code><br>- <code>network</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;spanning_tree_bpdufilter</samp>](## "port_profiles.[].spanning_tree_bpdufilter") | String |  |  | Valid Values:<br>- <code>enabled</code><br>- <code>disabled</code><br>- <code>True</code><br>- <code>False</code><br>- <code>true</code><br>- <code>false</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;spanning_tree_bpduguard</samp>](## "port_profiles.[].spanning_tree_bpduguard") | String |  |  | Valid Values:<br>- <code>enabled</code><br>- <code>disabled</code><br>- <code>True</code><br>- <code>False</code><br>- <code>true</code><br>- <code>false</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;flowcontrol</samp>](## "port_profiles.[].flowcontrol") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;received</samp>](## "port_profiles.[].flowcontrol.received") | String |  |  | Valid Values:<br>- <code>received</code><br>- <code>send</code><br>- <code>on</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;qos_profile</samp>](## "port_profiles.[].qos_profile") | String |  |  |  | QOS profile name |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;ptp</samp>](## "port_profiles.[].ptp") | Dictionary |  |  |  | The global PTP profile parameters will be applied to all connected endpoints where `ptp` is manually enabled.<br>`ptp role master` is set to ensure control over the PTP topology.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "port_profiles.[].ptp.enabled") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;endpoint_role</samp>](## "port_profiles.[].ptp.endpoint_role") | String |  | `follower` | Valid Values:<br>- <code>bmca</code><br>- <code>default</code><br>- <code>follower</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;profile</samp>](## "port_profiles.[].ptp.profile") | String |  | `aes67-r16-2016` | Valid Values:<br>- <code>aes67</code><br>- <code>aes67-r16-2016</code><br>- <code>smpte2059-2</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;sflow</samp>](## "port_profiles.[].sflow") | Boolean |  |  |  | Configures sFlow on the interface. Overrides `fabric_sflow` setting.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;link_tracking</samp>](## "port_profiles.[].link_tracking") | Dictionary |  |  |  | Configure the downstream interfaces of a respective Link Tracking Group.<br>If `port_channel` is defined in an adapter, then the port-channel interface is configured to be the downstream.<br>Else all the ethernet interfaces will be configured as downstream -> to configure single-active EVPN multihomed networks.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "port_profiles.[].link_tracking.enabled") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name</samp>](## "port_profiles.[].link_tracking.name") | String |  |  |  | Tracking group name.<br>The default group name is taken from fabric variable of the switch, `link_tracking.groups[0].name` with default value being "LT_GROUP1".<br>Optional if default link_tracking settings are configured on the node.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;dot1x</samp>](## "port_profiles.[].dot1x") | Dictionary |  |  |  | 802.1x |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;port_control</samp>](## "port_profiles.[].dot1x.port_control") | String |  |  | Valid Values:<br>- <code>auto</code><br>- <code>force-authorized</code><br>- <code>force-unauthorized</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;port_control_force_authorized_phone</samp>](## "port_profiles.[].dot1x.port_control_force_authorized_phone") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reauthentication</samp>](## "port_profiles.[].dot1x.reauthentication") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pae</samp>](## "port_profiles.[].dot1x.pae") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode</samp>](## "port_profiles.[].dot1x.pae.mode") | String |  |  | Valid Values:<br>- <code>authenticator</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;authentication_failure</samp>](## "port_profiles.[].dot1x.authentication_failure") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;action</samp>](## "port_profiles.[].dot1x.authentication_failure.action") | String |  |  | Valid Values:<br>- <code>allow</code><br>- <code>drop</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;allow_vlan</samp>](## "port_profiles.[].dot1x.authentication_failure.allow_vlan") | Integer |  |  | Min: 1<br>Max: 4094 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;host_mode</samp>](## "port_profiles.[].dot1x.host_mode") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode</samp>](## "port_profiles.[].dot1x.host_mode.mode") | String |  |  | Valid Values:<br>- <code>multi-host</code><br>- <code>single-host</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;multi_host_authenticated</samp>](## "port_profiles.[].dot1x.host_mode.multi_host_authenticated") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mac_based_authentication</samp>](## "port_profiles.[].dot1x.mac_based_authentication") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "port_profiles.[].dot1x.mac_based_authentication.enabled") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;always</samp>](## "port_profiles.[].dot1x.mac_based_authentication.always") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;host_mode_common</samp>](## "port_profiles.[].dot1x.mac_based_authentication.host_mode_common") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;timeout</samp>](## "port_profiles.[].dot1x.timeout") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;idle_host</samp>](## "port_profiles.[].dot1x.timeout.idle_host") | Integer |  |  | Min: 10<br>Max: 65535 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;quiet_period</samp>](## "port_profiles.[].dot1x.timeout.quiet_period") | Integer |  |  | Min: 1<br>Max: 65535 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reauth_period</samp>](## "port_profiles.[].dot1x.timeout.reauth_period") | String |  |  |  | Range 60-4294967295 or "server". |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reauth_timeout_ignore</samp>](## "port_profiles.[].dot1x.timeout.reauth_timeout_ignore") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tx_period</samp>](## "port_profiles.[].dot1x.timeout.tx_period") | Integer |  |  | Min: 1<br>Max: 65535 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reauthorization_request_limit</samp>](## "port_profiles.[].dot1x.reauthorization_request_limit") | Integer |  |  | Min: 1<br>Max: 10 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;poe</samp>](## "port_profiles.[].poe") | Dictionary |  |  |  | Power Over Ethernet settings applied on port. Only configured if platform supports PoE. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;disabled</samp>](## "port_profiles.[].poe.disabled") | Boolean |  | `False` |  | Disable PoE on a POE capable port. PoE is enabled on all ports that support it by default in EOS. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;priority</samp>](## "port_profiles.[].poe.priority") | String |  |  | Valid Values:<br>- <code>critical</code><br>- <code>high</code><br>- <code>medium</code><br>- <code>low</code> | Prioritize a port's power in the event that one of the switch's power supplies loses power |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reboot</samp>](## "port_profiles.[].poe.reboot") | Dictionary |  |  |  | Set the PoE power behavior for a PoE port when the system is rebooted |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;action</samp>](## "port_profiles.[].poe.reboot.action") | String |  |  | Valid Values:<br>- <code>maintain</code><br>- <code>power-off</code> | PoE action for interface |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;link_down</samp>](## "port_profiles.[].poe.link_down") | Dictionary |  |  |  | Set the PoE power behavior for a PoE port when the port goes down |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;action</samp>](## "port_profiles.[].poe.link_down.action") | String |  |  | Valid Values:<br>- <code>maintain</code><br>- <code>power-off</code> | PoE action for interface |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;power_off_delay</samp>](## "port_profiles.[].poe.link_down.power_off_delay") | Integer |  |  | Min: 1<br>Max: 86400 | Number of seconds to delay shutting the power off after a link down event occurs. Default value is 5 seconds in EOS. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shutdown</samp>](## "port_profiles.[].poe.shutdown") | Dictionary |  |  |  | Set the PoE power behavior for a PoE port when the port is admin down |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;action</samp>](## "port_profiles.[].poe.shutdown.action") | String |  |  | Valid Values:<br>- <code>maintain</code><br>- <code>power-off</code> | PoE action for interface |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;limit</samp>](## "port_profiles.[].poe.limit") | Dictionary |  |  |  | Override the hardware-negotiated power limit using either wattage or a power class. Note that if using a power class, AVD will automatically convert the class value to the wattage value corresponding to that power class. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;class</samp>](## "port_profiles.[].poe.limit.class") | Integer |  |  | Min: 0<br>Max: 8 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;watts</samp>](## "port_profiles.[].poe.limit.watts") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fixed</samp>](## "port_profiles.[].poe.limit.fixed") | Boolean |  |  |  | Set to ignore hardware classification |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;negotiation_lldp</samp>](## "port_profiles.[].poe.negotiation_lldp") | Boolean |  |  |  | Disable to prevent port from negotiating power with powered devices over LLDP. Enabled by default in EOS. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;legacy_detect</samp>](## "port_profiles.[].poe.legacy_detect") | Boolean |  |  |  | Allow a subset of legacy devices to work with the PoE switch. Disabled by default in EOS because it can cause false positive detections. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;storm_control</samp>](## "port_profiles.[].storm_control") | Dictionary |  |  |  | Storm control settings applied on port toward the endpoint. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;all</samp>](## "port_profiles.[].storm_control.all") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level</samp>](## "port_profiles.[].storm_control.all.level") | String |  |  |  | Configure maximum storm-control level. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;unit</samp>](## "port_profiles.[].storm_control.all.unit") | String |  | `percent` | Valid Values:<br>- <code>percent</code><br>- <code>pps</code> | Optional variable and is hardware dependent. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;broadcast</samp>](## "port_profiles.[].storm_control.broadcast") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level</samp>](## "port_profiles.[].storm_control.broadcast.level") | String |  |  |  | Configure maximum storm-control level. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;unit</samp>](## "port_profiles.[].storm_control.broadcast.unit") | String |  | `percent` | Valid Values:<br>- <code>percent</code><br>- <code>pps</code> | Optional variable and is hardware dependent. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;multicast</samp>](## "port_profiles.[].storm_control.multicast") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level</samp>](## "port_profiles.[].storm_control.multicast.level") | String |  |  |  | Configure maximum storm-control level. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;unit</samp>](## "port_profiles.[].storm_control.multicast.unit") | String |  | `percent` | Valid Values:<br>- <code>percent</code><br>- <code>pps</code> | Optional variable and is hardware dependent. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;unknown_unicast</samp>](## "port_profiles.[].storm_control.unknown_unicast") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level</samp>](## "port_profiles.[].storm_control.unknown_unicast.level") | String |  |  |  | Configure maximum storm-control level. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;unit</samp>](## "port_profiles.[].storm_control.unknown_unicast.unit") | String |  | `percent` | Valid Values:<br>- <code>percent</code><br>- <code>pps</code> | Optional variable and is hardware dependent. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;monitor_sessions</samp>](## "port_profiles.[].monitor_sessions") | List, items: Dictionary |  |  |  | Used to define switchports as source or destination for monitoring sessions. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "port_profiles.[].monitor_sessions.[].name") | String | Required |  |  | Session name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;role</samp>](## "port_profiles.[].monitor_sessions.[].role") | String |  |  | Valid Values:<br>- <code>source</code><br>- <code>destination</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;source_settings</samp>](## "port_profiles.[].monitor_sessions.[].source_settings") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;direction</samp>](## "port_profiles.[].monitor_sessions.[].source_settings.direction") | String |  |  | Valid Values:<br>- <code>rx</code><br>- <code>tx</code><br>- <code>both</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;access_group</samp>](## "port_profiles.[].monitor_sessions.[].source_settings.access_group") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type</samp>](## "port_profiles.[].monitor_sessions.[].source_settings.access_group.type") | String |  |  | Valid Values:<br>- <code>ip</code><br>- <code>ipv6</code><br>- <code>mac</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name</samp>](## "port_profiles.[].monitor_sessions.[].source_settings.access_group.name") | String |  |  |  | ACL name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;priority</samp>](## "port_profiles.[].monitor_sessions.[].source_settings.access_group.priority") | Integer |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;session_settings</samp>](## "port_profiles.[].monitor_sessions.[].session_settings") | Dictionary |  |  |  | Session settings are defined per session name.<br>Different session_settings for the same session name will be combined/merged.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;encapsulation_gre_metadata_tx</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.encapsulation_gre_metadata_tx") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;header_remove_size</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.header_remove_size") | Integer |  |  |  | Number of bytes to remove from header. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;access_group</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.access_group") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.access_group.type") | String |  |  | Valid Values:<br>- <code>ip</code><br>- <code>ipv6</code><br>- <code>mac</code> |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.access_group.name") | String |  |  |  | ACL name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rate_limit_per_ingress_chip</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.rate_limit_per_ingress_chip") | String |  |  |  | Ratelimit and unit as string.<br>Examples:<br>  "100000 bps"<br>  "100 kbps"<br>  "10 mbps"<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rate_limit_per_egress_chip</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.rate_limit_per_egress_chip") | String |  |  |  | Ratelimit and unit as string.<br>Examples:<br>  "100000 bps"<br>  "100 kbps"<br>  "10 mbps"<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sample</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.sample") | Integer |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;truncate</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.truncate") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.truncate.enabled") | Boolean |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;size</samp>](## "port_profiles.[].monitor_sessions.[].session_settings.truncate.size") | Integer |  |  |  | Size in bytes |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;ethernet_segment</samp>](## "port_profiles.[].ethernet_segment") | Dictionary |  |  |  | Settings for all or single-active EVPN multihoming. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;short_esi</samp>](## "port_profiles.[].ethernet_segment.short_esi") | String | Required |  |  | In format xxxx:xxxx:xxxx or "auto".<br>Define a manual short-esi (be careful using this on profiles) or set the value to "auto" to automatically generate the value.<br>Please see the notes under "EVPN A/A ESI dual and single-attached endpoint scenarios" before setting `short_esi: auto`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;redundancy</samp>](## "port_profiles.[].ethernet_segment.redundancy") | String |  |  | Valid Values:<br>- <code>all-active</code><br>- <code>single-active</code> | If omitted, Port-Channels use the EOS default of all-active.<br>If omitted, Ethernet interfaces are configured as single-active.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;designated_forwarder_algorithm</samp>](## "port_profiles.[].ethernet_segment.designated_forwarder_algorithm") | String |  |  | Valid Values:<br>- <code>auto</code><br>- <code>modulus</code><br>- <code>preference</code> | Configure DF algorithm and preferences.<br>- auto: Use preference-based algorithm and assign preference based on position of device in the 'switches' list,<br>  e.g., assuming a list of three switches, this would assign a preference of 200 to the first switch, 100 to the 2nd, and 0 to the third.<br>- preference: Set preference for each switch manually using designated_forwarder_preferences key.<br>- modulus: Use the default modulus-based algorithm.<br>If omitted, Port-Channels use the EOS default of modulus.<br>If omitted, Ethernet interfaces default to the 'auto' mechanism detailed above.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;designated_forwarder_preferences</samp>](## "port_profiles.[].ethernet_segment.designated_forwarder_preferences") | List, items: String |  |  |  | Manual preference as described above, required only for preference algorithm. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "port_profiles.[].ethernet_segment.designated_forwarder_preferences.[]") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dont_preempt</samp>](## "port_profiles.[].ethernet_segment.dont_preempt") | Boolean |  |  |  | Disable preemption for single-active forwarding when auto/manual DF preference is configured. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;port_channel</samp>](## "port_profiles.[].port_channel") | Dictionary |  |  |  | Used for port-channel adapter. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode</samp>](## "port_profiles.[].port_channel.mode") | String |  |  | Valid Values:<br>- <code>active</code><br>- <code>passive</code><br>- <code>on</code> | Port-Channel Mode. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;channel_id</samp>](## "port_profiles.[].port_channel.channel_id") | Integer |  |  |  | Port-Channel ID.<br>If no channel_id is specified, an id is generated from the first switch port in the port channel.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;description</samp>](## "port_profiles.[].port_channel.description") | String |  |  |  | By default the description is built leveraging `<peer>` name or `adapter.description` when defined.<br>When this key is defined, it will append its content to the physical port description.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "port_profiles.[].port_channel.enabled") | Boolean |  | `True` |  | Port-Channel administrative state.<br>Setting to false will set port to 'shutdown' in intended configuration.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;esi</samp>](## "port_profiles.[].port_channel.esi") <span style="color:red">removed</span> | String |  |  |  | Format xxxx:xxxx:xxxx.<span style="color:red">This key was removed. Support was removed in AVD version 4.0.0. Use <samp>short_esi</samp> instead.</span> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;short_esi</samp>](## "port_profiles.[].port_channel.short_esi") <span style="color:red">deprecated</span> | String |  |  |  | In format xxxx:xxxx:xxxx or "auto".<span style="color:red">This key is deprecated. Support will be removed in AVD version 5.0.0. Use <samp>ethernet_segment.short_esi</samp> instead.</span> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lacp_fallback</samp>](## "port_profiles.[].port_channel.lacp_fallback") | Dictionary |  |  |  | LACP fallback configuration. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode</samp>](## "port_profiles.[].port_channel.lacp_fallback.mode") | String |  |  | Valid Values:<br>- <code>static</code> | Currently only static mode is supported. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;timeout</samp>](## "port_profiles.[].port_channel.lacp_fallback.timeout") | Integer |  |  |  | Timeout in seconds. EOS default is 90 seconds. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lacp_timer</samp>](## "port_profiles.[].port_channel.lacp_timer") | Dictionary |  |  |  | LACP timer configuration. Applies only when Port-channel mode is not "on". |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode</samp>](## "port_profiles.[].port_channel.lacp_timer.mode") | String |  |  | Valid Values:<br>- <code>normal</code><br>- <code>fast</code> | LACP mode for interface members. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;multiplier</samp>](## "port_profiles.[].port_channel.lacp_timer.multiplier") | Integer |  |  |  | Number of LACP BPDUs lost before deeming the peer down. EOS default is 3. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;subinterfaces</samp>](## "port_profiles.[].port_channel.subinterfaces") | List, items: Dictionary |  |  |  | Port-Channel L2 Subinterfaces<br>Subinterfaces are only supported on routed port-channels, which means they cannot be configured on MLAG port-channels.<br>Setting short_esi: auto generates the short_esi automatically using a hash of configuration elements.<br>Please see the notes under "EVPN A/A ESI dual-attached endpoint scenario" before setting short_esi: auto.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;number</samp>](## "port_profiles.[].port_channel.subinterfaces.[].number") | Integer |  |  |  | Subinterface number |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;short_esi</samp>](## "port_profiles.[].port_channel.subinterfaces.[].short_esi") | String |  |  |  | In format xxxx:xxxx:xxxx or "auto"<br>Required for multihomed port-channels with subinterfaces<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;vlan_id</samp>](## "port_profiles.[].port_channel.subinterfaces.[].vlan_id") | Integer |  |  | Min: 1<br>Max: 4094 | VLAN ID to bridge.<br>Default is subinterface number.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;encapsulation_vlan</samp>](## "port_profiles.[].port_channel.subinterfaces.[].encapsulation_vlan") | Dictionary |  |  |  | Client VLAN ID encapsulation.<br>Default is subinterface number.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;client_dot1q</samp>](## "port_profiles.[].port_channel.subinterfaces.[].encapsulation_vlan.client_dot1q") | Integer |  |  | Min: 1<br>Max: 4094 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;raw_eos_cli</samp>](## "port_profiles.[].port_channel.raw_eos_cli") | String |  |  |  | EOS CLI rendered directly on the port-channel interface in the final EOS configuration. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;structured_config</samp>](## "port_profiles.[].port_channel.structured_config") | Dictionary |  |  |  | Custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;raw_eos_cli</samp>](## "port_profiles.[].raw_eos_cli") | String |  |  |  | EOS CLI rendered directly on the ethernet interface in the final EOS configuration. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;structured_config</samp>](## "port_profiles.[].structured_config") | Dictionary |  |  |  | Custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen. |

=== "YAML"

    ```yaml
    # Optional profiles to share common settings for connected_endpoints and/or network_ports.
    # Keys are the same used under endpoints adapters. Keys defined under endpoints adapters take precedence.
    port_profiles:

        # Port profile name.
      - profile: <str; required; unique>

        # Parent profile is optional.
        # Port_profiles can refer to another port_profile to inherit settings in up to two levels (adapter->profile->parent_profile).
        parent_profile: <str>

        # Set adapter speed in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
        # If not specified speed will be auto.
        speed: <str>

        # By default the description is built leveraging `<peer>_<peer_interface>`.
        # When set this key will overide the default value on the physical ports.
        description: <str>

        # Administrative state, setting to false will set the port to 'shutdown' in the intended configuration.
        enabled: <bool; default=True>

        # Interface mode.
        mode: <str; "access" | "dot1q-tunnel" | "trunk" | "trunk phone">
        mtu: <int; 68-65535>

        # "l2_mtu" should only be defined for platforms supporting the "l2 mtu" CLI
        l2_mtu: <int; 68-65535>

        # "l2_mru" should only be defined for platforms supporting the "l2 mru" CLI
        l2_mru: <int; 68-65535>

        # Native VLAN for a trunk port.
        # If both `native_vlan` and `native_vlan_tag`, `native_vlan_tag` takes precedence.
        native_vlan: <int; 1-4094>

        # If both `native_vlan` and `native_vlan_tag`, `native_vlan_tag` takes precedence.
        native_vlan_tag: <bool; default=False>

        # Required with `enable_trunk_groups: true`.
        # Trunk Groups are used for limiting VLANs on trunk ports to VLANs with the same Trunk Group.
        trunk_groups:
          - <str>

        # Interface VLANs - if not set, the EOS default is that all VLANs are allowed for trunk ports, and VLAN 1 will be used for access ports.
        vlans: <str>
        spanning_tree_portfast: <str; "edge" | "network">
        spanning_tree_bpdufilter: <str; "enabled" | "disabled" | "True" | "False" | "true" | "false">
        spanning_tree_bpduguard: <str; "enabled" | "disabled" | "True" | "False" | "true" | "false">
        flowcontrol:
          received: <str; "received" | "send" | "on">

        # QOS profile name
        qos_profile: <str>

        # The global PTP profile parameters will be applied to all connected endpoints where `ptp` is manually enabled.
        # `ptp role master` is set to ensure control over the PTP topology.
        ptp:
          enabled: <bool; default=False>
          endpoint_role: <str; "bmca" | "default" | "follower"; default="follower">
          profile: <str; "aes67" | "aes67-r16-2016" | "smpte2059-2"; default="aes67-r16-2016">

        # Configures sFlow on the interface. Overrides `fabric_sflow` setting.
        sflow: <bool>

        # Configure the downstream interfaces of a respective Link Tracking Group.
        # If `port_channel` is defined in an adapter, then the port-channel interface is configured to be the downstream.
        # Else all the ethernet interfaces will be configured as downstream -> to configure single-active EVPN multihomed networks.
        link_tracking:
          enabled: <bool>

          # Tracking group name.
          # The default group name is taken from fabric variable of the switch, `link_tracking.groups[0].name` with default value being "LT_GROUP1".
          # Optional if default link_tracking settings are configured on the node.
          name: <str>

        # 802.1x
        dot1x:
          port_control: <str; "auto" | "force-authorized" | "force-unauthorized">
          port_control_force_authorized_phone: <bool>
          reauthentication: <bool>
          pae:
            mode: <str; "authenticator">
          authentication_failure:
            action: <str; "allow" | "drop">
            allow_vlan: <int; 1-4094>
          host_mode:
            mode: <str; "multi-host" | "single-host">
            multi_host_authenticated: <bool>
          mac_based_authentication:
            enabled: <bool>
            always: <bool>
            host_mode_common: <bool>
          timeout:
            idle_host: <int; 10-65535>
            quiet_period: <int; 1-65535>

            # Range 60-4294967295 or "server".
            reauth_period: <str>
            reauth_timeout_ignore: <bool>
            tx_period: <int; 1-65535>
          reauthorization_request_limit: <int; 1-10>

        # Power Over Ethernet settings applied on port. Only configured if platform supports PoE.
        poe:

          # Disable PoE on a POE capable port. PoE is enabled on all ports that support it by default in EOS.
          disabled: <bool; default=False>

          # Prioritize a port's power in the event that one of the switch's power supplies loses power
          priority: <str; "critical" | "high" | "medium" | "low">

          # Set the PoE power behavior for a PoE port when the system is rebooted
          reboot:

            # PoE action for interface
            action: <str; "maintain" | "power-off">

          # Set the PoE power behavior for a PoE port when the port goes down
          link_down:

            # PoE action for interface
            action: <str; "maintain" | "power-off">

            # Number of seconds to delay shutting the power off after a link down event occurs. Default value is 5 seconds in EOS.
            power_off_delay: <int; 1-86400>

          # Set the PoE power behavior for a PoE port when the port is admin down
          shutdown:

            # PoE action for interface
            action: <str; "maintain" | "power-off">

          # Override the hardware-negotiated power limit using either wattage or a power class. Note that if using a power class, AVD will automatically convert the class value to the wattage value corresponding to that power class.
          limit:
            class: <int; 0-8>
            watts: <str>

            # Set to ignore hardware classification
            fixed: <bool>

          # Disable to prevent port from negotiating power with powered devices over LLDP. Enabled by default in EOS.
          negotiation_lldp: <bool>

          # Allow a subset of legacy devices to work with the PoE switch. Disabled by default in EOS because it can cause false positive detections.
          legacy_detect: <bool>

        # Storm control settings applied on port toward the endpoint.
        storm_control:
          all:

            # Configure maximum storm-control level.
            level: <str>

            # Optional variable and is hardware dependent.
            unit: <str; "percent" | "pps"; default="percent">
          broadcast:

            # Configure maximum storm-control level.
            level: <str>

            # Optional variable and is hardware dependent.
            unit: <str; "percent" | "pps"; default="percent">
          multicast:

            # Configure maximum storm-control level.
            level: <str>

            # Optional variable and is hardware dependent.
            unit: <str; "percent" | "pps"; default="percent">
          unknown_unicast:

            # Configure maximum storm-control level.
            level: <str>

            # Optional variable and is hardware dependent.
            unit: <str; "percent" | "pps"; default="percent">

        # Used to define switchports as source or destination for monitoring sessions.
        monitor_sessions:

            # Session name.
          - name: <str; required>
            role: <str; "source" | "destination">
            source_settings:
              direction: <str; "rx" | "tx" | "both">
              access_group:
                type: <str; "ip" | "ipv6" | "mac">

                # ACL name.
                name: <str>
                priority: <int>

            # Session settings are defined per session name.
            # Different session_settings for the same session name will be combined/merged.
            session_settings:
              encapsulation_gre_metadata_tx: <bool>

              # Number of bytes to remove from header.
              header_remove_size: <int>
              access_group:
                type: <str; "ip" | "ipv6" | "mac">

                # ACL name.
                name: <str>

              # Ratelimit and unit as string.
              # Examples:
              #   "100000 bps"
              #   "100 kbps"
              #   "10 mbps"
              rate_limit_per_ingress_chip: <str>

              # Ratelimit and unit as string.
              # Examples:
              #   "100000 bps"
              #   "100 kbps"
              #   "10 mbps"
              rate_limit_per_egress_chip: <str>
              sample: <int>
              truncate:
                enabled: <bool>

                # Size in bytes
                size: <int>

        # Settings for all or single-active EVPN multihoming.
        ethernet_segment:

          # In format xxxx:xxxx:xxxx or "auto".
          # Define a manual short-esi (be careful using this on profiles) or set the value to "auto" to automatically generate the value.
          # Please see the notes under "EVPN A/A ESI dual and single-attached endpoint scenarios" before setting `short_esi: auto`.
          short_esi: <str; required>

          # If omitted, Port-Channels use the EOS default of all-active.
          # If omitted, Ethernet interfaces are configured as single-active.
          redundancy: <str; "all-active" | "single-active">

          # Configure DF algorithm and preferences.
          # - auto: Use preference-based algorithm and assign preference based on position of device in the 'switches' list,
          #   e.g., assuming a list of three switches, this would assign a preference of 200 to the first switch, 100 to the 2nd, and 0 to the third.
          # - preference: Set preference for each switch manually using designated_forwarder_preferences key.
          # - modulus: Use the default modulus-based algorithm.
          # If omitted, Port-Channels use the EOS default of modulus.
          # If omitted, Ethernet interfaces default to the 'auto' mechanism detailed above.
          designated_forwarder_algorithm: <str; "auto" | "modulus" | "preference">

          # Manual preference as described above, required only for preference algorithm.
          designated_forwarder_preferences:
            - <str>

          # Disable preemption for single-active forwarding when auto/manual DF preference is configured.
          dont_preempt: <bool>

        # Used for port-channel adapter.
        port_channel:

          # Port-Channel Mode.
          mode: <str; "active" | "passive" | "on">

          # Port-Channel ID.
          # If no channel_id is specified, an id is generated from the first switch port in the port channel.
          channel_id: <int>

          # By default the description is built leveraging `<peer>` name or `adapter.description` when defined.
          # When this key is defined, it will append its content to the physical port description.
          description: <str>

          # Port-Channel administrative state.
          # Setting to false will set port to 'shutdown' in intended configuration.
          enabled: <bool; default=True>

          # In format xxxx:xxxx:xxxx or "auto".
          # This key is deprecated.
          # Support will be removed in AVD version 5.0.0.
          # Use <samp>ethernet_segment.short_esi</samp> instead.
          short_esi: <str>

          # LACP fallback configuration.
          lacp_fallback:

            # Currently only static mode is supported.
            mode: <str; "static">

            # Timeout in seconds. EOS default is 90 seconds.
            timeout: <int>

          # LACP timer configuration. Applies only when Port-channel mode is not "on".
          lacp_timer:

            # LACP mode for interface members.
            mode: <str; "normal" | "fast">

            # Number of LACP BPDUs lost before deeming the peer down. EOS default is 3.
            multiplier: <int>

          # Port-Channel L2 Subinterfaces
          # Subinterfaces are only supported on routed port-channels, which means they cannot be configured on MLAG port-channels.
          # Setting short_esi: auto generates the short_esi automatically using a hash of configuration elements.
          # Please see the notes under "EVPN A/A ESI dual-attached endpoint scenario" before setting short_esi: auto.
          subinterfaces:

              # Subinterface number
            - number: <int>

              # In format xxxx:xxxx:xxxx or "auto"
              # Required for multihomed port-channels with subinterfaces
              short_esi: <str>

              # VLAN ID to bridge.
              # Default is subinterface number.
              vlan_id: <int; 1-4094>

              # Client VLAN ID encapsulation.
              # Default is subinterface number.
              encapsulation_vlan:
                client_dot1q: <int; 1-4094>

          # EOS CLI rendered directly on the port-channel interface in the final EOS configuration.
          raw_eos_cli: <str>

          # Custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen.
          structured_config: <dict>

        # EOS CLI rendered directly on the ethernet interface in the final EOS configuration.
        raw_eos_cli: <str>

        # Custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen.
        structured_config: <dict>
    ```
