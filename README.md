# wpcm450-openocd

Create your openocd.cfg in your project directory.

Run `openocd`, run `telnet localhost 4444` and execute the command `soft_reset_hold; exit`.
Restart `openocd`, run `./gdb.sh`.

## openocd.cfg

```
transport select jtag
reset_config srst_only
adapter speed 1000

source [find target/wpcm450.cfg]
```

## gdb.sh

```
#!/bin/sh
elf="monitor.elf"

gdb -ex "target extended-remote localhost:3333" \
	-ex "#monitor reset init" \
	-ex "load ${elf}" \
	-ex "continue" \
	"${elf}"
```

## Connections

### JTAG

```
J_IBMC_JTAG
2                                                     20
() () () () () () () () () () () () () () () () () () ()
[] () () () () () () () () () () () () () () () () () ()
```

pin | function
----|----------------
1   | VTref (3.3V)
2   | VCC (3.3V)
3   | TRST (Used)
4   | GND (Used)
5   | TDI (Used)
6   | NC
7   | TMS/SWDIO
8   | NC
9   | TCK/SWCLK
10  | NC
11  | NC
12  | NC
13  | TDO/SWO
14  | NC
15  | RESET
16  | NC
17  | NC
18  | NC
19  | NC
20  | NC

### RPI

JTAG pin      | RPI pin
--------------|----------------
1 (VCC)       | NC
2 (VCC)       | NC
3 (TRST)      | 26 (GPIO7)
4 (GND)       | 20 (GROUND)
5 (TDI)       | 19 (GPIO10)
6 (NC)        | NC
7 (TMS/SWDIO) | 28 (GPIO8)
8 (NC)        | NC
9 (TCK/SWCLK) | 23 (GPIO11)
10 (NC)       | NC
11 (RTCLK)    | NC
12 (NC)       | NC
13 (TDO/SWO)  | 21 (GPIO9)
14 (NC)       | NC
15 (RESET)    | 18 (GPIO24)
16 (NC)       | NC
17 (NC)       | NC
18 (NC)       | NC
19 (NC)       | NC
20 (NC)       | NC