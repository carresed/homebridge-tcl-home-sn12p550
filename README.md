# Homebridge TCL Home SN12P550

Homebridge plugin for TCL Home air conditioners, forked and adapted for the TCL SN12P550 / P09F4CSW1K.

This fork is based on the original [homebridge-tcl-home](https://github.com/5at0ri/homebridge-tcl-home) project by [5at0ri](https://github.com/5at0ri). The original project is licensed under the MIT License; this fork keeps the same license and copyright notice.

## Supported Device

Tested on:

- TCL SN12P550 / P09F4CSW1K

Other TCL Home app connected air conditioners may work, but this fork documents only the behavior tested on the model above.

## SN12P550 Behavior

Confirmed working on the tested unit:

- HomeKit On/Off controls `powerSwitch`
- HomeKit Cool maps to TCL `workMode: 1`
- HomeKit Off sends `powerSwitch: 0`
- TCL `workMode: 1` maps back to HomeKit Cool
- TCL `workMode: 0` maps back to HomeKit Auto
- TCL `workMode: 2` maps back to HomeKit Auto and is treated as Dry on this model
- HomeKit target temperature writes using `targetTemperature`
- TCL shadow/reporting target temperature is read from `targetCelsiusDegree`, with fallback to `targetTemperature`
- Current temperature reporting works
- Fan control and fan speed work without changing the TCL operating mode
- Sleep Mode is intentionally removed from HomeKit

Note: the currently tested local code sends HomeKit Auto as `workMode: 0`. If your unit requires Auto to send `workMode: 2`, verify that on the device before changing this mapping.

## HomeKit Controls

### Thermostat

- Off: powers the AC off
- Cool: turns the AC on in TCL cooling mode
- Auto: exposed intentionally for the SN12P550 alternate mode behavior
- Target temperature: 18-30 C

### AC Fan

Fan speed is exposed separately and only changes `windSpeed`. It does not power the AC on/off and does not change `workMode`.

Approximate mapping:

| HomeKit Speed | TCL `windSpeed` |
| --- | --- |
| 0% | 0 |
| 1-16% | 2 |
| 17-33% | 3 |
| 34-50% | 4 |
| 51-66% | 5 |
| 67-100% | 6 |

## Installation

Until this fork is published to npm, install it from GitHub after creating the repository:

```bash
npm install -g git+https://github.com/YOUR_GITHUB_USERNAME/homebridge-tcl-home-sn12p550.git
```

If you publish it to npm later:

```bash
npm install -g homebridge-tcl-home-sn12p550
```

## Configuration

```json
{
  "platforms": [
    {
      "platform": "TclHome",
      "name": "TCL Home",
      "username": "your.email@example.com",
      "password": "your_tcl_password",
      "debugMode": false
    }
  ]
}
```

| Option | Required | Default | Description |
| --- | --- | --- | --- |
| `username` | Yes | - | TCL Home app email address |
| `password` | Yes | - | TCL Home app password |
| `debugMode` | No | `false` | Enable detailed Homebridge logs |

## Development

```bash
npm install
node --check index.js
```

## Credits

Original project: [5at0ri/homebridge-tcl-home](https://github.com/5at0ri/homebridge-tcl-home).

The original plugin also credits [nemesa/ha-tcl-home-unofficial-integration](https://github.com/nemesa/ha-tcl-home-unofficial-integration) for TCL Home API documentation and authentication flow analysis.

## License

MIT License. See [LICENSE](LICENSE).

This fork preserves the original MIT license and attribution.
