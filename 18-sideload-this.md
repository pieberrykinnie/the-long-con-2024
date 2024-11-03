# Sideload this!

Presented by Mike

- Bluetooth products are shit

## Reverse engineering

- Decomppile Android APKs
- Sniff traffic from the apps from an Android device
- How do you capture Bluetooth traffic off of an Android phone?
- `extcap`:
    - WireShark/TShark support extcap
    - Way of adding external capture and log sources
    - Like `remote-sshdump` or `ciscodump`
- The simple example, capturing wifi
    - Wireshark -> Extcap -> Androiddump -> tcpdump
- Can drag and drop bugreport.zip to Wireshark

## Quick guide on BNE

- What are we seeing
    - Attribute handle new-value notifications
    - Two PDUs, one with 20 bytes, one with 16
    - ff550100...
- I don't know what I'm doing so
    - JADX was the tool I grabbed
    - Opened up the APK
    - Only got 2000 warnings
    - Got some shockingly readable code
- Can figure out the byte frames and how they parse

## Lessons learned

- I hate Java
- Wireshark is always the saviour
- BLE is weird and very opaque and obtuse
