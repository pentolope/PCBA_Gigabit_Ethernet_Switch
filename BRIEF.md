# PCBA_Gigabit_Ethernet_Switch — Five-Port Gigabit Ethernet Switch

**Benchmark ID:** 26  
**Difficulty:** 5/5  
**Brief detail:** 3/5  
**Category:** high-speed-networking  
**Likely layer count:** 6  
**Primary stressors:** many Ethernet differential pairs, BGA/QFN escape, multiple supplies, magnetics placement

## Design brief

Create a compact five-port 1000BASE-T Ethernet switch PCB using an integrated switch IC plus the required magnetics/connectors. Include management access through a small MCU or header, clocks, EEPROM/flash if needed, and all power rails. Aim for a board size that forces careful placement rather than giving the differential pairs unlimited space. Follow the switch vendor's reference layout and PHY supply recommendations.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
