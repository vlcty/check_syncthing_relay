check_syncthing_relay
=====================

check_syncthing_relay is a plugin for your monitoring environment which uses plugins developed according to the Nagios Developer Guidelines. So if you are running Nagios or (better) Icinga/Icinga 2 it should be easy to implement it.

The plugin fetches the Syncthing relay server status page and analyzes the returned JSON. This plugin is able to check if the relay is up but the main focus lies on gathering performance data.

Usage
-----
Let's say your Syncthing relay server runs on the IP 51.254.126.115 and its status page is available via port 22070 (that's the default port). The call would look like the following:

```
:~$ perl check_syncthing_relay --address 51.254.126.115
```

If 22070 is not your default port you can of course specify it. The call then looks like this:

```
:~$ perl check_syncthing_relay --address 51.254.126.115 --port 12345
```

If the plugin can fetch the status page and is able to analyze the content then the ouput will look similar like this:

```
OK - Connections: 963 Active sessions: 197 Traffic: 741.74 GByte
Average bandwidth used:
10s -> 20.28 MBit/s
1m -> 16.20 MBit/s
5m -> 13.45 MBit/s
15m -> 13.86 MBit/s
30m -> 13.22 MBit/s
60m -> 11.01 MBit/s|connections=963 active_sessions=197 traffic=741742194821 avg_bandwidth_10s=20276 avg_bandwidth_1m=16195 avg_bandwidth_5m=13447 avg_bandwidth_15m=13856 avg_bandwidth_30m=13225 avg_bandwidth_60m=11011
```

The values are calculated since the Syncthing relay server was started.

Used units in the display and performance data string
-----------------------------------------------------------

The units in the display string are converted from Bytes and KBit to more human readable formats if necessary. However the units used in the performance data string are always the same:
- traffic is given in bytes
- avg_bandwidth_XXX are given in KBit/s

Integration into Icinga 2
-------------------------

Use the following CheckCommand definition:
