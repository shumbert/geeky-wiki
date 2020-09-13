# Configuration
## TCP sequence numbers
By default wireshark replaces TCP sequence numbers with relative ones (starting at 1) for easier analysis. To display the original sequence numbers go to Edit > Preferences > Protocols > TCP and uncheck TCP relative numbers.

## Directories
Go to Help > About wireshark then select the Folders tab to see all plugin, configuration, ... directories used by wireshark.

## Configuration profiles
Use configuration profiles to save the following settings:
- preferences
- capture filters
- display filters
- coloring rules
- disabled protocols
- forced decodes
- recent settings, such as pane sizes, view menu settings, and column widths
- protocol-specific tables, such as SNMP users and custom HTTP headers

Access through Edit > Configuration profiles or profile manager at the bottom-right end of the screen. Profiles are stored under ~/.config/wireshark/profiles, you can back them up or copy them to another machine.

# Finding packets
Open the find toolbar using Ctrl+F or Edit > Find packet. You can choose between:
- display filters
- hex value (for instance 00ff)
- string
- regular expression

# Marking packets
Mark a packet by right-clicking a packet and selecting Mark packet, or by pressing Ctrl+M.

To jump forward/backward between marked packets press Shift+Ctrl+N and Shift+Ctrl+B.

# Timing
You can mark a packet as time reference so that all subsequent time calculations are done starting at that packet. Right-click the packet and select "Set time reference" or press Ctrl+T.

If you merge network captures taken from different machines with various time soures packets might not be properly synced. Before merging you can shift timestamp by going to Edit > Time Shift.

# Display filters
You can save display filters by either:
- entering your display filter, then click the ribbon on the left side and select Save this filter
- go to Capture > Capture filters

You can apply saved filters by clicking the ribbon on the left side of the display filters toolbar.

You can also create a filter button by clicking the + sign in the display filters toolbar or going Edit > Preferences > Filter buttons.

# Name resolution
You can create a custom hosts file for name resolution.

Create the file under ~/.config/wireshark/<profile>/hosts:
```
10.0.0.42 alice
10.0.0.43 bob
```

Then go to Edit > Preferences > Name resolution and modify the following options:
- check "Resolve network (IP) addresses"
- uncheck "Use an external network name resolver"
- check "Only use the profile hosts file"

# Dissectors
Wireshark generally successfully guesses which dissector to use for a given packet. If wireshark is off-track however (for instance if a non-standard port is used) you can manually override it.

Either right-click a packet and select Decode as, or go to Analyze > Decode as. Then select the field, its value and which dissector you want to apply.

You can view the dissectors source code [here](https://github.com/wireshark/wireshark/tree/master/epan/dissectors).

# SSL
In the past it was possible to decrypt SSL traffic if you had the RSA private key. But as prefect forward secrecy is becoming more common it is not the case anymore. You can still decrypt traffic if you set up your browser to log the SSL pre-master secret keys.

First set up an environment variable SSLKEYLOGFILE:
```
export SSLKEYLOGFILE=/path/to/ssl/log/file
```

Then start up your browser (make sure SSLKEYLOGFILE is actually part of the environment variables seen by your browser).

Then in wireshark:
- go to Edit > Preferences > Protocols > SSL
- choose the ssl keys log file in (Pre)-Master-Secret log filename

Then capture traffic, wireshark will be able to decrypt traffic.

# Statistics
Here is some useful statistics about your traffic.

## Packet lengths
Go to Statistics > Packet Length

## Protocol Hierarchy
Go to Statistics > Protocol Hierarchy to list a hierarchy of the protocols found in the capture.

## Graphing
### IO graph
Go to Statistics > IO Graph to graph network throughput. You can superpose several visualisations (lines, bars, stacked bars, ...) and use display filters to apply them to subsets of the overall traffic.

For instance you can use several stacked bars, each with their own display filter, to show relative proportion of different classes of traffic.

### Round-trip time
Go to Statistics > TCP Stream Graphs > Round Trip Time Graph.

**Note:** the graph is unidirectional, you can click on the switch direction to see the opposite side.

### Flow graphing
Show a column-based view of connections between hosts.

# Expert information
Dissectors define expert info which alerts you about various states regarding packets and connections. Expert Info is displayed on a packet per packet basis in the packet list, you can see it all by going to Analyze > Expert Information.
