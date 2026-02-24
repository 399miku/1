# Diva Controller

Project layout:

- Android app: `app/`
- Windows bridge: `../windows-bridge/`

## Android (current: 0.1.0)

### 0.1.0 update notes

1. `versionName` -> `0.1.0`
2. `versionCode` -> `4`
3. Slider mapping changed:
   - old: `L2/R2` trigger analog
   - new: `LB/RB` shoulder button events
4. Slider multi-press added:
   - two fingers moving opposite directions in slide zone can produce `LB=true` and `RB=true` at the same time

### Protocol (NDJSON)

One JSON per line:

- Button
```json
{"type":"button","name":"TRIANGLE","pressed":true,"t":1700000000000}
```

- Trigger (legacy compatible)
```json
{"type":"trigger","l2":0.0000,"r2":0.7200,"t":1700000000000}
```

### Protocol compatibility

- Android 0.1.0 slider now emits `button` events with `name` = `LB` / `RB`.
- Windows bridge 0.1.0 remains backward compatible with legacy `trigger` frames:
  - still parses `trigger`
  - converts `l2/r2 > 0.01` to shoulder pressed state for fallback compatibility.

### Connect to Windows bridge

- IP: Windows host IP in LAN
- PORT: `28999`

ADB reverse:

```bash
adb reverse tcp:28999 tcp:28999
```

Then Android can use `127.0.0.1:28999`.

## Windows bridge

See `../windows-bridge/README.md`.
