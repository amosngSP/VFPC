# VFPC Plugin (Modified with Transition, FLAS)

This version of the plugin has been modified to add in checks for FLAS, Transitions in SIDs separated by x (XOBAV2DxNIXIV), and general improvements to the parsing of the JSON file to accept string inputs on top of arrays.

Part of the code has been copied from vatsimhk's HKCP repository, but slightly modified for areas where transitions are in the SID.
 
VFPC (Vatsim Flugplan-RFL checker) is a plugin for EuroScope that checks defined departure restrictions on filed flight plans. It adds a Tag Item type for the Departure List, which displays the result of the check.

![Departure List](https://i.imgur.com/wJRsdJq.png)

## Features:
- Tag item VFPC: Shows check-result as green 'OK!' or red 'FPL!' ('SID' = No valid SID found, 'ENG' = Failed Engine type restriction, 'E/O' = Failed even/odd Flightlevel, 'MIN' = Failed minimum Flight Level, 'MAX' = Failed maximum Flightlevel)
- Tag function 'Check FP': Explains the check-result in chat output
- Chat command '.vfpc reload': reload the Sid.json config
- Chat command '.vfpc check': checks currently selected AC and outputs result
- Restrictions customizable in Sid.json config
- Checks Even/Odd Flightlevel restriction
- Checks Minimum & Maximum Flightlevel restriction
- Check condition 'route must contain airway' available
- Check condition 'destination must be' available
- Check condition 'aircraft type must be' available (? - unknown, P - piston, T - turboprop/turboshaft, J - jet, E - electric)

## How to use:
- Load up the plugin
- Add Tag Item type & function to Departure List
- Extend the 'Sid.json' config file
![Departure List2](https://i.imgur.com/kQrtVfN.png)


### How to define configurations
The 'Sid.json'-File is using the JSON file format. Each airport is an object containing the "icao" and a sub-object "sids", which contains all definitions & restrictions. Inside this sub-object are all available SIDs defined by the first route waypoint (i.e. "AMLUH" for AMLUH1B, AMLUH9C, AMLUH9D & AMLUH9G).
Each SID can contain multiple objects with defined options based on restrictions. The plugin will stop at the first matching one from top-to-bottom, so the most restrictive objects should always be on top.

Available restrictions:
- "destinations" - Array of strings OR string. The object only applies to FPL with one of the given destination ICAOs. Partials are possible, ex. "ED"
- "engine" - Either string or array of strings. The object only applies to AC with one of the given Engine Types. Options are "P" (piston), "T" (turboprop/turboshaft), "J" (jet) and "E" (electric), as defined by Euroscope
- "navigation" - A string which contains the equipment codes which defines all allowed capabilities for the SID
- "airways" - Array of strings OR string. The object only applies to FPL if route contains any of the given airways

Available options:
- "direction" - String. The FPL must have this E/O option as final flightlevel. Available: "EVEN/ODD/ANY")
- "min_fl" - Integer. The FPL must have this flightlevel as minimum
- "max_fl" - Integer. The FPL must have this flightlevel as maximum
- "allowed_fls" - Array of strings. Contains all the allowed flight levels for the route (Used for FLAS)
- "FLAS" - A remark column for when allowed_fls is used. Basically contains the same thing as allowed_fls but in string.

Examples can be found in the given Sid.json file. (TO BE UPDATED)
