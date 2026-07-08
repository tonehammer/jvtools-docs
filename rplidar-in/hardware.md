# Hardware & Cabling

## The sensor

RPLidar In was developed against the **Slamtec RPLIDAR A2M12** — a 360°, 16 m range, spinning laser scanner. Other A2-family units should behave the same. The sensor stays completely silent until Houdini commands the motor to spin, so *no lights or sound when you first plug it in is normal*.

## The two cables

RPLIDAR units use two separate leads:

| Cable | Carries | Plug into |
| --- | --- | --- |
| **USB / data** | Data + adapter power, through the USB/UART adapter | Your computer |
| **5V / motor** | Motor power only | Any USB port or USB charger |

Both must be connected for a scan. The motor lead can go to a plain charger — it does not need to be the same machine.

## The USB/UART adapter

The sensor connects through a **Silicon Labs CP210x** USB-to-serial adapter, which enumerates as a COM port on Windows (the driver ships with Windows 11). The adapter has a **baud-rate switch** — it **must be set to 256000** for the A2 family. At the wrong setting the device is completely silent.

## Finding the port

Leave the node's **Port** parameter blank and it auto-detects the CP210x adapter. If auto-detect picks the wrong device (e.g. you have several serial adapters), set the port explicitly — for example `COM3` on Windows.

## Baud rate

The **Baud Rate** parameter defaults to **256000**, which is correct for the A2 family and the only value tested. It exists so you can experiment with other models (A1 uses 115200, S2 uses 1000000), but those are untested. Changing it while Live restarts the stream.

## Only one program at a time

A serial port can only be opened by one process. If Houdini can't open the sensor, make sure no other program holds the port — a separate tester app, another Houdini session in Live mode, or a stale process. Set **Mode → Off** in any session you're not actively using.

## Common wiring problems

* **No Windows chime, nothing new in Device Manager** → cable or port problem, not a driver problem. Try the other USB port and swap the data cable — a dud data cable will stop the device enumerating entirely.
* **Enumerates but no data** → check the adapter baud switch is on 256000.

See [Troubleshooting](troubleshooting.md) for more.
