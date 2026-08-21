# Changelog

## 1.1.16-sn12p550.1

- Forked from `5at0ri/homebridge-tcl-home` `v1.1.16`.
- Added tested support notes for TCL SN12P550 / P09F4CSW1K.
- Adjusted HomeKit Cool handling for TCL `workMode: 1`.
- Kept HomeKit Auto exposed for SN12P550 alternate mode behavior.
- Removed Sleep Mode from the HomeKit accessory surface.
- Changed target temperature writes to use `targetTemperature`.
- Reads reported target temperature from `targetCelsiusDegree`, with fallback to `targetTemperature`.
- Made fan speed control update only TCL `windSpeed`, without changing power or operating mode.
- Kept MIT license and original attribution.
