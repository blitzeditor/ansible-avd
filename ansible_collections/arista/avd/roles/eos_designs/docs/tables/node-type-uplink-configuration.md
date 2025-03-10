<!--
  ~ Copyright (c) 2023 Arista Networks, Inc.
  ~ Use of this source code is governed by the Apache License 2.0
  ~ that can be found in the LICENSE file.
  -->
=== "Table"

    | Variable | Type | Required | Default | Value Restrictions | Description |
    | -------- | ---- | -------- | ------- | ------------------ | ----------- |
    | [<samp>&lt;node_type_keys.key&gt;</samp>](## "<node_type_keys.key>") | Dictionary |  |  |  |  |
    | [<samp>&nbsp;&nbsp;defaults</samp>](## "<node_type_keys.key>.defaults") | Dictionary |  |  |  | Define variables for all nodes of this type. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;link_tracking</samp>](## "<node_type_keys.key>.defaults.link_tracking") | Dictionary |  |  |  | This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.<br>Useful in EVPN multhoming designs.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "<node_type_keys.key>.defaults.link_tracking.enabled") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;groups</samp>](## "<node_type_keys.key>.defaults.link_tracking.groups") | List, items: Dictionary |  | `[{'name': 'LT_GROUP1'}]` |  | Link Tracking Groups.<br>By default a single group named "LT_GROUP1" is defined with default values.<br>Any groups defined under "groups" will replace the default.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "<node_type_keys.key>.defaults.link_tracking.groups.[].name") | String |  |  |  | Tracking group name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;recovery_delay</samp>](## "<node_type_keys.key>.defaults.link_tracking.groups.[].recovery_delay") | Integer |  |  | Min: 0<br>Max: 3600 | default -> platform_settings_mlag_reload_delay -> 300. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;links_minimum</samp>](## "<node_type_keys.key>.defaults.link_tracking.groups.[].links_minimum") | Integer |  |  | Min: 1<br>Max: 100000 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_ipv4_pool</samp>](## "<node_type_keys.key>.defaults.uplink_ipv4_pool") | String |  |  | Format: ipv4_cidr | IPv4 subnet to use to connect to uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_interfaces</samp>](## "<node_type_keys.key>.defaults.uplink_interfaces") | List, items: String |  |  |  | Local uplink interfaces<br>Each list item supports range syntax that can be expanded into a list of interfaces.<br>If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.<br>Please note that default_interfaces are not defined by default, you should define these yourself.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.defaults.uplink_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interfaces</samp>](## "<node_type_keys.key>.defaults.uplink_switch_interfaces") | List, items: String |  |  |  | Interfaces located on uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.defaults.uplink_switch_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_switches</samp>](## "<node_type_keys.key>.defaults.uplink_switches") | List, items: String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.defaults.uplink_switches.[]") | String | Required |  |  | Hostname of uplink switch.<br>If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.<br>e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_interface_speed</samp>](## "<node_type_keys.key>.defaults.uplink_interface_speed") | String |  |  |  | Set point-to-Point interface speed and will apply to uplink interfaces on both ends.<br>(Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interface_speed</samp>](## "<node_type_keys.key>.defaults.uplink_switch_interface_speed") | String |  |  |  | Set point-to-Point interface speed for the uplink switch interface only.<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;max_uplink_switches</samp>](## "<node_type_keys.key>.defaults.max_uplink_switches") | Integer |  |  |  | Maximum number of uplink switches.<br>Changing this value may change IP Addressing on uplinks.<br>Can be used to reserve IP space for future expansions.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;max_parallel_uplinks</samp>](## "<node_type_keys.key>.defaults.max_parallel_uplinks") | Integer |  |  |  | Number of parallel links towards uplink switches.<br>Changing this value may change interface naming on uplinks (and corresponding downlinks).<br>Can be used to reserve interfaces for future parallel uplinks.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_bfd</samp>](## "<node_type_keys.key>.defaults.uplink_bfd") | Boolean |  | `False` |  | Enable bfd on uplink interfaces. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_native_vlan</samp>](## "<node_type_keys.key>.defaults.uplink_native_vlan") | Integer |  |  | Min: 1<br>Max: 4094 | Only applicable to switches with layer-2 port-channel uplinks.<br>A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.<br>By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_ptp</samp>](## "<node_type_keys.key>.defaults.uplink_ptp") | Dictionary |  |  |  | Enable PTP on all infrastructure links. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enable</samp>](## "<node_type_keys.key>.defaults.uplink_ptp.enable") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_macsec</samp>](## "<node_type_keys.key>.defaults.uplink_macsec") | Dictionary |  |  |  | Enable MacSec on all uplinks. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;profile</samp>](## "<node_type_keys.key>.defaults.uplink_macsec.profile") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;uplink_structured_config</samp>](## "<node_type_keys.key>.defaults.uplink_structured_config") | Dictionary |  |  |  | Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".<br>When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.<br>When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.<br>"uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.<br>Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;short_esi</samp>](## "<node_type_keys.key>.defaults.short_esi") | String |  |  |  | short_esi only valid for l2leaf devices using port-channel uplink.<br>Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.<br>< 0000:0000:0000 | auto >.<br> |
    | [<samp>&nbsp;&nbsp;node_groups</samp>](## "<node_type_keys.key>.node_groups") | List, items: Dictionary |  |  |  | Define variables related to all nodes part of this group. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;group</samp>](## "<node_type_keys.key>.node_groups.[].group") | String | Required, Unique |  |  | The Node Group Name is used for MLAG domain unless set with 'mlag_domain_id'.<br>The Node Group Name is also used for peer description on downstream switches' uplinks.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nodes</samp>](## "<node_type_keys.key>.node_groups.[].nodes") | List, items: Dictionary |  |  |  | Define variables per node. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].name") | String | Required, Unique |  |  | The Node Name is used as "hostname". |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;link_tracking</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].link_tracking") | Dictionary |  |  |  | This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.<br>Useful in EVPN multhoming designs.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].link_tracking.enabled") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;groups</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].link_tracking.groups") | List, items: Dictionary |  | `[{'name': 'LT_GROUP1'}]` |  | Link Tracking Groups.<br>By default a single group named "LT_GROUP1" is defined with default values.<br>Any groups defined under "groups" will replace the default.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].link_tracking.groups.[].name") | String |  |  |  | Tracking group name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;recovery_delay</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].link_tracking.groups.[].recovery_delay") | Integer |  |  | Min: 0<br>Max: 3600 | default -> platform_settings_mlag_reload_delay -> 300. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;links_minimum</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].link_tracking.groups.[].links_minimum") | Integer |  |  | Min: 1<br>Max: 100000 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_ipv4_pool</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_ipv4_pool") | String |  |  | Format: ipv4_cidr | IPv4 subnet to use to connect to uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_interfaces</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_interfaces") | List, items: String |  |  |  | Local uplink interfaces<br>Each list item supports range syntax that can be expanded into a list of interfaces.<br>If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.<br>Please note that default_interfaces are not defined by default, you should define these yourself.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interfaces</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_switch_interfaces") | List, items: String |  |  |  | Interfaces located on uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_switch_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switches</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_switches") | List, items: String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_switches.[]") | String | Required |  |  | Hostname of uplink switch.<br>If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.<br>e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_interface_speed</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_interface_speed") | String |  |  |  | Set point-to-Point interface speed and will apply to uplink interfaces on both ends.<br>(Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interface_speed</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_switch_interface_speed") | String |  |  |  | Set point-to-Point interface speed for the uplink switch interface only.<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;max_uplink_switches</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].max_uplink_switches") | Integer |  |  |  | Maximum number of uplink switches.<br>Changing this value may change IP Addressing on uplinks.<br>Can be used to reserve IP space for future expansions.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;max_parallel_uplinks</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].max_parallel_uplinks") | Integer |  |  |  | Number of parallel links towards uplink switches.<br>Changing this value may change interface naming on uplinks (and corresponding downlinks).<br>Can be used to reserve interfaces for future parallel uplinks.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_bfd</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_bfd") | Boolean |  | `False` |  | Enable bfd on uplink interfaces. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_native_vlan</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_native_vlan") | Integer |  |  | Min: 1<br>Max: 4094 | Only applicable to switches with layer-2 port-channel uplinks.<br>A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.<br>By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_ptp</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_ptp") | Dictionary |  |  |  | Enable PTP on all infrastructure links. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enable</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_ptp.enable") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_macsec</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_macsec") | Dictionary |  |  |  | Enable MacSec on all uplinks. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;profile</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_macsec.profile") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_structured_config</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].uplink_structured_config") | Dictionary |  |  |  | Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".<br>When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.<br>When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.<br>"uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.<br>Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;short_esi</samp>](## "<node_type_keys.key>.node_groups.[].nodes.[].short_esi") | String |  |  |  | short_esi only valid for l2leaf devices using port-channel uplink.<br>Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.<br>< 0000:0000:0000 | auto >.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;link_tracking</samp>](## "<node_type_keys.key>.node_groups.[].link_tracking") | Dictionary |  |  |  | This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.<br>Useful in EVPN multhoming designs.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "<node_type_keys.key>.node_groups.[].link_tracking.enabled") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;groups</samp>](## "<node_type_keys.key>.node_groups.[].link_tracking.groups") | List, items: Dictionary |  | `[{'name': 'LT_GROUP1'}]` |  | Link Tracking Groups.<br>By default a single group named "LT_GROUP1" is defined with default values.<br>Any groups defined under "groups" will replace the default.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "<node_type_keys.key>.node_groups.[].link_tracking.groups.[].name") | String |  |  |  | Tracking group name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;recovery_delay</samp>](## "<node_type_keys.key>.node_groups.[].link_tracking.groups.[].recovery_delay") | Integer |  |  | Min: 0<br>Max: 3600 | default -> platform_settings_mlag_reload_delay -> 300. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;links_minimum</samp>](## "<node_type_keys.key>.node_groups.[].link_tracking.groups.[].links_minimum") | Integer |  |  | Min: 1<br>Max: 100000 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_ipv4_pool</samp>](## "<node_type_keys.key>.node_groups.[].uplink_ipv4_pool") | String |  |  | Format: ipv4_cidr | IPv4 subnet to use to connect to uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_interfaces</samp>](## "<node_type_keys.key>.node_groups.[].uplink_interfaces") | List, items: String |  |  |  | Local uplink interfaces<br>Each list item supports range syntax that can be expanded into a list of interfaces.<br>If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.<br>Please note that default_interfaces are not defined by default, you should define these yourself.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.node_groups.[].uplink_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interfaces</samp>](## "<node_type_keys.key>.node_groups.[].uplink_switch_interfaces") | List, items: String |  |  |  | Interfaces located on uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.node_groups.[].uplink_switch_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switches</samp>](## "<node_type_keys.key>.node_groups.[].uplink_switches") | List, items: String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.node_groups.[].uplink_switches.[]") | String | Required |  |  | Hostname of uplink switch.<br>If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.<br>e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_interface_speed</samp>](## "<node_type_keys.key>.node_groups.[].uplink_interface_speed") | String |  |  |  | Set point-to-Point interface speed and will apply to uplink interfaces on both ends.<br>(Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interface_speed</samp>](## "<node_type_keys.key>.node_groups.[].uplink_switch_interface_speed") | String |  |  |  | Set point-to-Point interface speed for the uplink switch interface only.<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;max_uplink_switches</samp>](## "<node_type_keys.key>.node_groups.[].max_uplink_switches") | Integer |  |  |  | Maximum number of uplink switches.<br>Changing this value may change IP Addressing on uplinks.<br>Can be used to reserve IP space for future expansions.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;max_parallel_uplinks</samp>](## "<node_type_keys.key>.node_groups.[].max_parallel_uplinks") | Integer |  |  |  | Number of parallel links towards uplink switches.<br>Changing this value may change interface naming on uplinks (and corresponding downlinks).<br>Can be used to reserve interfaces for future parallel uplinks.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_bfd</samp>](## "<node_type_keys.key>.node_groups.[].uplink_bfd") | Boolean |  | `False` |  | Enable bfd on uplink interfaces. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_native_vlan</samp>](## "<node_type_keys.key>.node_groups.[].uplink_native_vlan") | Integer |  |  | Min: 1<br>Max: 4094 | Only applicable to switches with layer-2 port-channel uplinks.<br>A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.<br>By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_ptp</samp>](## "<node_type_keys.key>.node_groups.[].uplink_ptp") | Dictionary |  |  |  | Enable PTP on all infrastructure links. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enable</samp>](## "<node_type_keys.key>.node_groups.[].uplink_ptp.enable") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_macsec</samp>](## "<node_type_keys.key>.node_groups.[].uplink_macsec") | Dictionary |  |  |  | Enable MacSec on all uplinks. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;profile</samp>](## "<node_type_keys.key>.node_groups.[].uplink_macsec.profile") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_structured_config</samp>](## "<node_type_keys.key>.node_groups.[].uplink_structured_config") | Dictionary |  |  |  | Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".<br>When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.<br>When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.<br>"uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.<br>Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;short_esi</samp>](## "<node_type_keys.key>.node_groups.[].short_esi") | String |  |  |  | short_esi only valid for l2leaf devices using port-channel uplink.<br>Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.<br>< 0000:0000:0000 | auto >.<br> |
    | [<samp>&nbsp;&nbsp;nodes</samp>](## "<node_type_keys.key>.nodes") | List, items: Dictionary |  |  |  | Define variables per node. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "<node_type_keys.key>.nodes.[].name") | String | Required, Unique |  |  | The Node Name is used as "hostname". |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;link_tracking</samp>](## "<node_type_keys.key>.nodes.[].link_tracking") | Dictionary |  |  |  | This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.<br>Useful in EVPN multhoming designs.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enabled</samp>](## "<node_type_keys.key>.nodes.[].link_tracking.enabled") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;groups</samp>](## "<node_type_keys.key>.nodes.[].link_tracking.groups") | List, items: Dictionary |  | `[{'name': 'LT_GROUP1'}]` |  | Link Tracking Groups.<br>By default a single group named "LT_GROUP1" is defined with default values.<br>Any groups defined under "groups" will replace the default.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;name</samp>](## "<node_type_keys.key>.nodes.[].link_tracking.groups.[].name") | String |  |  |  | Tracking group name. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;recovery_delay</samp>](## "<node_type_keys.key>.nodes.[].link_tracking.groups.[].recovery_delay") | Integer |  |  | Min: 0<br>Max: 3600 | default -> platform_settings_mlag_reload_delay -> 300. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;links_minimum</samp>](## "<node_type_keys.key>.nodes.[].link_tracking.groups.[].links_minimum") | Integer |  |  | Min: 1<br>Max: 100000 |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_ipv4_pool</samp>](## "<node_type_keys.key>.nodes.[].uplink_ipv4_pool") | String |  |  | Format: ipv4_cidr | IPv4 subnet to use to connect to uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_interfaces</samp>](## "<node_type_keys.key>.nodes.[].uplink_interfaces") | List, items: String |  |  |  | Local uplink interfaces<br>Each list item supports range syntax that can be expanded into a list of interfaces.<br>If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.<br>Please note that default_interfaces are not defined by default, you should define these yourself.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.nodes.[].uplink_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interfaces</samp>](## "<node_type_keys.key>.nodes.[].uplink_switch_interfaces") | List, items: String |  |  |  | Interfaces located on uplink switches. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.nodes.[].uplink_switch_interfaces.[]") | String |  |  | Pattern: Ethernet[\d/]+ |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switches</samp>](## "<node_type_keys.key>.nodes.[].uplink_switches") | List, items: String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&lt;str&gt;</samp>](## "<node_type_keys.key>.nodes.[].uplink_switches.[]") | String | Required |  |  | Hostname of uplink switch.<br>If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.<br>e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_interface_speed</samp>](## "<node_type_keys.key>.nodes.[].uplink_interface_speed") | String |  |  |  | Set point-to-Point interface speed and will apply to uplink interfaces on both ends.<br>(Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_switch_interface_speed</samp>](## "<node_type_keys.key>.nodes.[].uplink_switch_interface_speed") | String |  |  |  | Set point-to-Point interface speed for the uplink switch interface only.<br>Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;max_uplink_switches</samp>](## "<node_type_keys.key>.nodes.[].max_uplink_switches") | Integer |  |  |  | Maximum number of uplink switches.<br>Changing this value may change IP Addressing on uplinks.<br>Can be used to reserve IP space for future expansions.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;max_parallel_uplinks</samp>](## "<node_type_keys.key>.nodes.[].max_parallel_uplinks") | Integer |  |  |  | Number of parallel links towards uplink switches.<br>Changing this value may change interface naming on uplinks (and corresponding downlinks).<br>Can be used to reserve interfaces for future parallel uplinks.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_bfd</samp>](## "<node_type_keys.key>.nodes.[].uplink_bfd") | Boolean |  | `False` |  | Enable bfd on uplink interfaces. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_native_vlan</samp>](## "<node_type_keys.key>.nodes.[].uplink_native_vlan") | Integer |  |  | Min: 1<br>Max: 4094 | Only applicable to switches with layer-2 port-channel uplinks.<br>A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.<br>By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_ptp</samp>](## "<node_type_keys.key>.nodes.[].uplink_ptp") | Dictionary |  |  |  | Enable PTP on all infrastructure links. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;enable</samp>](## "<node_type_keys.key>.nodes.[].uplink_ptp.enable") | Boolean |  | `False` |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_macsec</samp>](## "<node_type_keys.key>.nodes.[].uplink_macsec") | Dictionary |  |  |  | Enable MacSec on all uplinks. |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;profile</samp>](## "<node_type_keys.key>.nodes.[].uplink_macsec.profile") | String |  |  |  |  |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;uplink_structured_config</samp>](## "<node_type_keys.key>.nodes.[].uplink_structured_config") | Dictionary |  |  |  | Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".<br>When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.<br>When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.<br>"uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.<br>Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.<br> |
    | [<samp>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;short_esi</samp>](## "<node_type_keys.key>.nodes.[].short_esi") | String |  |  |  | short_esi only valid for l2leaf devices using port-channel uplink.<br>Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.<br>< 0000:0000:0000 | auto >.<br> |

=== "YAML"

    ```yaml
    <node_type_keys.key>:

      # Define variables for all nodes of this type.
      defaults:

        # This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.
        # Useful in EVPN multhoming designs.
        link_tracking:
          enabled: <bool; default=False>

          # Link Tracking Groups.
          # By default a single group named "LT_GROUP1" is defined with default values.
          # Any groups defined under "groups" will replace the default.
          groups: # default=[{'name': 'LT_GROUP1'}]

              # Tracking group name.
            - name: <str>

              # default -> platform_settings_mlag_reload_delay -> 300.
              recovery_delay: <int; 0-3600>
              links_minimum: <int; 1-100000>

        # IPv4 subnet to use to connect to uplink switches.
        uplink_ipv4_pool: <str>

        # Local uplink interfaces
        # Each list item supports range syntax that can be expanded into a list of interfaces.
        # If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.
        # Please note that default_interfaces are not defined by default, you should define these yourself.
        uplink_interfaces:
          - <str>

        # Interfaces located on uplink switches.
        uplink_switch_interfaces:
          - <str>
        uplink_switches:

            # Hostname of uplink switch.
            # If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.
            # e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].
          - <str; required>

        # Set point-to-Point interface speed and will apply to uplink interfaces on both ends.
        # (Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).
        # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
        uplink_interface_speed: <str>

        # Set point-to-Point interface speed for the uplink switch interface only.
        # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
        uplink_switch_interface_speed: <str>

        # Maximum number of uplink switches.
        # Changing this value may change IP Addressing on uplinks.
        # Can be used to reserve IP space for future expansions.
        max_uplink_switches: <int>

        # Number of parallel links towards uplink switches.
        # Changing this value may change interface naming on uplinks (and corresponding downlinks).
        # Can be used to reserve interfaces for future parallel uplinks.
        max_parallel_uplinks: <int>

        # Enable bfd on uplink interfaces.
        uplink_bfd: <bool; default=False>

        # Only applicable to switches with layer-2 port-channel uplinks.
        # A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.
        # By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.
        uplink_native_vlan: <int; 1-4094>

        # Enable PTP on all infrastructure links.
        uplink_ptp:
          enable: <bool; default=False>

        # Enable MacSec on all uplinks.
        uplink_macsec:
          profile: <str>

        # Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".
        # When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.
        # When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.
        # "uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.
        # Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.
        uplink_structured_config: <dict>

        # short_esi only valid for l2leaf devices using port-channel uplink.
        # Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.
        # < 0000:0000:0000 | auto >.
        short_esi: <str>

      # Define variables related to all nodes part of this group.
      node_groups:

          # The Node Group Name is used for MLAG domain unless set with 'mlag_domain_id'.
          # The Node Group Name is also used for peer description on downstream switches' uplinks.
        - group: <str; required; unique>

          # Define variables per node.
          nodes:

              # The Node Name is used as "hostname".
            - name: <str; required; unique>

              # This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.
              # Useful in EVPN multhoming designs.
              link_tracking:
                enabled: <bool; default=False>

                # Link Tracking Groups.
                # By default a single group named "LT_GROUP1" is defined with default values.
                # Any groups defined under "groups" will replace the default.
                groups: # default=[{'name': 'LT_GROUP1'}]

                    # Tracking group name.
                  - name: <str>

                    # default -> platform_settings_mlag_reload_delay -> 300.
                    recovery_delay: <int; 0-3600>
                    links_minimum: <int; 1-100000>

              # IPv4 subnet to use to connect to uplink switches.
              uplink_ipv4_pool: <str>

              # Local uplink interfaces
              # Each list item supports range syntax that can be expanded into a list of interfaces.
              # If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.
              # Please note that default_interfaces are not defined by default, you should define these yourself.
              uplink_interfaces:
                - <str>

              # Interfaces located on uplink switches.
              uplink_switch_interfaces:
                - <str>
              uplink_switches:

                  # Hostname of uplink switch.
                  # If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.
                  # e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].
                - <str; required>

              # Set point-to-Point interface speed and will apply to uplink interfaces on both ends.
              # (Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).
              # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
              uplink_interface_speed: <str>

              # Set point-to-Point interface speed for the uplink switch interface only.
              # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
              uplink_switch_interface_speed: <str>

              # Maximum number of uplink switches.
              # Changing this value may change IP Addressing on uplinks.
              # Can be used to reserve IP space for future expansions.
              max_uplink_switches: <int>

              # Number of parallel links towards uplink switches.
              # Changing this value may change interface naming on uplinks (and corresponding downlinks).
              # Can be used to reserve interfaces for future parallel uplinks.
              max_parallel_uplinks: <int>

              # Enable bfd on uplink interfaces.
              uplink_bfd: <bool; default=False>

              # Only applicable to switches with layer-2 port-channel uplinks.
              # A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.
              # By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.
              uplink_native_vlan: <int; 1-4094>

              # Enable PTP on all infrastructure links.
              uplink_ptp:
                enable: <bool; default=False>

              # Enable MacSec on all uplinks.
              uplink_macsec:
                profile: <str>

              # Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".
              # When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.
              # When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.
              # "uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.
              # Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.
              uplink_structured_config: <dict>

              # short_esi only valid for l2leaf devices using port-channel uplink.
              # Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.
              # < 0000:0000:0000 | auto >.
              short_esi: <str>

          # This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.
          # Useful in EVPN multhoming designs.
          link_tracking:
            enabled: <bool; default=False>

            # Link Tracking Groups.
            # By default a single group named "LT_GROUP1" is defined with default values.
            # Any groups defined under "groups" will replace the default.
            groups: # default=[{'name': 'LT_GROUP1'}]

                # Tracking group name.
              - name: <str>

                # default -> platform_settings_mlag_reload_delay -> 300.
                recovery_delay: <int; 0-3600>
                links_minimum: <int; 1-100000>

          # IPv4 subnet to use to connect to uplink switches.
          uplink_ipv4_pool: <str>

          # Local uplink interfaces
          # Each list item supports range syntax that can be expanded into a list of interfaces.
          # If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.
          # Please note that default_interfaces are not defined by default, you should define these yourself.
          uplink_interfaces:
            - <str>

          # Interfaces located on uplink switches.
          uplink_switch_interfaces:
            - <str>
          uplink_switches:

              # Hostname of uplink switch.
              # If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.
              # e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].
            - <str; required>

          # Set point-to-Point interface speed and will apply to uplink interfaces on both ends.
          # (Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).
          # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
          uplink_interface_speed: <str>

          # Set point-to-Point interface speed for the uplink switch interface only.
          # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
          uplink_switch_interface_speed: <str>

          # Maximum number of uplink switches.
          # Changing this value may change IP Addressing on uplinks.
          # Can be used to reserve IP space for future expansions.
          max_uplink_switches: <int>

          # Number of parallel links towards uplink switches.
          # Changing this value may change interface naming on uplinks (and corresponding downlinks).
          # Can be used to reserve interfaces for future parallel uplinks.
          max_parallel_uplinks: <int>

          # Enable bfd on uplink interfaces.
          uplink_bfd: <bool; default=False>

          # Only applicable to switches with layer-2 port-channel uplinks.
          # A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.
          # By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.
          uplink_native_vlan: <int; 1-4094>

          # Enable PTP on all infrastructure links.
          uplink_ptp:
            enable: <bool; default=False>

          # Enable MacSec on all uplinks.
          uplink_macsec:
            profile: <str>

          # Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".
          # When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.
          # When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.
          # "uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.
          # Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.
          uplink_structured_config: <dict>

          # short_esi only valid for l2leaf devices using port-channel uplink.
          # Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.
          # < 0000:0000:0000 | auto >.
          short_esi: <str>

      # Define variables per node.
      nodes:

          # The Node Name is used as "hostname".
        - name: <str; required; unique>

          # This configures the Link Tracking Group on a switch as well as adds the p2p-uplinks of the switch as the upstream interfaces.
          # Useful in EVPN multhoming designs.
          link_tracking:
            enabled: <bool; default=False>

            # Link Tracking Groups.
            # By default a single group named "LT_GROUP1" is defined with default values.
            # Any groups defined under "groups" will replace the default.
            groups: # default=[{'name': 'LT_GROUP1'}]

                # Tracking group name.
              - name: <str>

                # default -> platform_settings_mlag_reload_delay -> 300.
                recovery_delay: <int; 0-3600>
                links_minimum: <int; 1-100000>

          # IPv4 subnet to use to connect to uplink switches.
          uplink_ipv4_pool: <str>

          # Local uplink interfaces
          # Each list item supports range syntax that can be expanded into a list of interfaces.
          # If uplink_interfaces is not defined, platform-specific defaults (defined under default_interfaces) will be used instead.
          # Please note that default_interfaces are not defined by default, you should define these yourself.
          uplink_interfaces:
            - <str>

          # Interfaces located on uplink switches.
          uplink_switch_interfaces:
            - <str>
          uplink_switches:

              # Hostname of uplink switch.
              # If parallel uplinks are in use, update max_parallel_uplinks below and specify each uplink switch multiple times.
              # e.g. uplink_switches: [ 'DC1-SPINE1', 'DC1-SPINE1', 'DC1-SPINE2', 'DC1-SPINE2' ].
            - <str; required>

          # Set point-to-Point interface speed and will apply to uplink interfaces on both ends.
          # (Uplink switch interface speed can be overridden with `uplink_switch_interface_speed`).
          # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
          uplink_interface_speed: <str>

          # Set point-to-Point interface speed for the uplink switch interface only.
          # Speed should be set in the format `<interface_speed>` or `forced <interface_speed>` or `auto <interface_speed>`.
          uplink_switch_interface_speed: <str>

          # Maximum number of uplink switches.
          # Changing this value may change IP Addressing on uplinks.
          # Can be used to reserve IP space for future expansions.
          max_uplink_switches: <int>

          # Number of parallel links towards uplink switches.
          # Changing this value may change interface naming on uplinks (and corresponding downlinks).
          # Can be used to reserve interfaces for future parallel uplinks.
          max_parallel_uplinks: <int>

          # Enable bfd on uplink interfaces.
          uplink_bfd: <bool; default=False>

          # Only applicable to switches with layer-2 port-channel uplinks.
          # A suspended (disabled) vlan will be created in both ends of the link unless the vlan is defined under network services.
          # By default the uplink will not have a native_vlan configured, so EOS defaults to vlan 1.
          uplink_native_vlan: <int; 1-4094>

          # Enable PTP on all infrastructure links.
          uplink_ptp:
            enable: <bool; default=False>

          # Enable MacSec on all uplinks.
          uplink_macsec:
            profile: <str>

          # Custom structured config applied to "uplink_interfaces", and "uplink_switch_interfaces".
          # When uplink_type == "p2p", custom structured config added under ethernet_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the ethernet interface level.
          # When uplink_type == "port-channel", custom structured config added under port_channel_interfaces.[name=<interface>] for eos_cli_config_gen overrides the settings on the port-channel interface level.
          # "uplink_structured_config" is applied after "structured_config", so it can override "structured_config" defined on node-level.
          # Note! The content of this dictionary is _not_ validated by the schema, since it can be either ethernet_interfaces or port_channel_interfaces.
          uplink_structured_config: <dict>

          # short_esi only valid for l2leaf devices using port-channel uplink.
          # Setting short_esi to "auto" generates the short_esi automatically using a hash of configuration elements.
          # < 0000:0000:0000 | auto >.
          short_esi: <str>
    ```
