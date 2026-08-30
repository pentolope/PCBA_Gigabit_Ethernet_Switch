# Benchmark entry — board 26 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_Gigabit_Ethernet_Switch` |
| Board id | `gigabit_ethernet_switch` |
| Category | high-speed-networking |
| Difficulty | 5 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 6 |
| Primary stressors | many Ethernet differential pairs, BGA/QFN escape, multiple supplies, magnetics placement |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

At difficulty 5/5 with a mid-detail (3/5) brief, this board tests whether an agent can carry a high-speed-networking design through the physical problems the metadata names: routing many Ethernet differential pairs in a deliberately tight area, BGA/QFN escape on the switch package, generating the multiple supplies the design turns out to need, and magnetics placement in that same tight area. The brief specifies function and layout authority but almost no numbers, so the test is whether the agent derives rail counts, clocking, impedance targets and stackup from the chosen silicon and the vendor's documentation rather than inventing them. Compliance with a vendor reference layout is an explicit requirement, which makes citation discipline part of what is being measured.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
