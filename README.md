# Five-Port Gigabit Ethernet Switch

A compact five-port 1000BASE-T Ethernet switch PCB built on an integrated switch IC with the required magnetics, connectors, clocks and power rails.

This repository holds the design problem for a compact five-port 1000BASE-T Ethernet switch PCB. The brief fixes the function (five 1000BASE-T ports), the architecture at one level (the switching function is realised in an integrated switch IC, plus the required magnetics and connectors), the presence of management access via either a small MCU or a header, clocks on the board, EEPROM/flash if the chosen device needs it, and all power rails. It also fixes two non-negotiable postures: the board must be small enough that placement of the differential pairs is genuinely constrained, and the switch vendor's reference layout and PHY supply recommendations must be followed. Everything below that - which switch IC, how much it integrates (including whether the PHYs are on-chip), its package, the rail count and voltages, the board input, the clock scheme, connector and magnetics packaging, port protection, board outline, and the stackup that realises the impedance and skew budgets - is left to the design agent and must be decided and documented rather than assumed.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 14 requirements and deliberately leaves
18 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Port count and Ethernet standard | Five ports, 1000BASE-T | brief |
| Switching silicon | An integrated switch IC; the brief names no vendor, device or package, and does not say how much is integrated into it | brief |
| Port front-end scope | The required magnetics and connectors are in scope on this board | brief |
| Management access | Present, via either a small MCU or a header; the brief accepts either | brief |
| Clocking | Clocks required on board; source, frequency, count and distribution not stated | brief |
| Non-volatile configuration storage | EEPROM/flash, conditional - required only if the chosen architecture needs it | brief |
| Power rails | All power rails are in this board's scope; the board input, rail count, voltages and currents are not stated | brief |
| Board size posture | Compact - deliberately tight enough to constrain differential-pair placement; no dimensions given | brief |
| Layout authority | The switch vendor's reference layout and PHY supply recommendations must be followed | brief |
| Likely layer count | 6 | metadata |
| Category, difficulty, brief detail | high-speed-networking; difficulty 5/5; detail 3/5 | metadata |
| Primary stressors | many Ethernet differential pairs; BGA/QFN escape; multiple supplies; magnetics placement | metadata |
| Board outline, dimensions, mounting and connector face | Not fixed by the brief - design agent's choice, constrained only by the compactness posture | open |
| PoE, uplink/SFP, status LEDs, console, enclosure | Not fixed by the brief - the design agent decides whether any of these exist at all | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 26 of 32 |
| Category | high-speed-networking |
| Difficulty | 5 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 6 |
| Primary stressors | many Ethernet differential pairs, BGA/QFN escape, multiple supplies, magnetics placement |

At difficulty 5/5 with a mid-detail (3/5) brief, this board tests whether an agent can carry a high-speed-networking design through the physical problems the metadata names: routing many Ethernet differential pairs in a deliberately tight area, BGA/QFN escape on the switch package, generating the multiple supplies the design turns out to need, and magnetics placement in that same tight area. The brief specifies function and layout authority but almost no numbers, so the test is whether the agent derives rail counts, clocking, impedance targets and stackup from the chosen silicon and the vendor's documentation rather than inventing them. Compliance with a vendor reference layout is an explicit requirement, which makes citation discipline part of what is being measured.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_Gigabit_Ethernet_Switch.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `b28f5cff7f166379930dd38d7c264a32ff1c70ad964a03e870eeecbba56a0d39`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
