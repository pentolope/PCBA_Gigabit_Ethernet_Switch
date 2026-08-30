# Requirements — Five-Port Gigabit Ethernet Switch

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `b28f5cff7f166379930dd38d7c264a32ff1c70ad964a03e870eeecbba56a0d39`.

## Fixed by the brief

### REQ-01 — The board is an Ethernet switch with five 1000BASE-T ports.

Brief text:

> five-port 1000BASE-T Ethernet switch PCB using an integrated switch IC

### REQ-02 — The switching function is realised in an integrated switch IC rather than a discrete implementation; the brief does not say how much that IC integrates, including whether the port PHYs are on-chip.

Brief text:

> using an integrated switch IC plus the required magnetics/connectors

### REQ-03 — The magnetics and port connectors required by the ports are part of this board's scope.

Brief text:

> Create a compact five-port 1000BASE-T Ethernet switch PCB using an integrated switch IC plus the required magnetics/connectors.

### REQ-04 — The board must be compact.

Brief text:

> Create a compact five-port 1000BASE-T Ethernet switch PCB using an integrated switch IC plus the required magnetics/connectors.

### REQ-05 — Management access must be provided, either through a small MCU on the board or through a header.

Brief text:

> Include management access through a small MCU or header

### REQ-06 — Clocks must be provided on the board.

Brief text:

> Include management access through a small MCU or header, clocks, EEPROM/flash if needed

### REQ-07 — EEPROM/flash must be included if the chosen architecture needs it; the brief makes this conditional rather than unconditional.

Brief text:

> Include management access through a small MCU or header, clocks, EEPROM/flash if needed, and all power rails.

### REQ-08 — All the power rails the design needs must be included on this board; the brief states no board input, rail count, voltages or currents, and does not say which rails are generated on-board versus supplied to it.

Brief text:

> Include management access through a small MCU or header, clocks, EEPROM/flash if needed, and all power rails.

### REQ-09 — Board size must be chosen so that placement is genuinely constrained; the differential pairs must not be given unlimited space.

Brief text:

> Aim for a board size that forces careful placement rather than giving the differential pairs unlimited space.

### REQ-10 — The switch vendor's reference layout must be followed.

Brief text:

> Follow the switch vendor's reference layout and PHY supply recommendations.

### REQ-11 — The vendor's PHY supply recommendations must be followed.

Brief text:

> Follow the switch vendor's reference layout and PHY supply recommendations.

### REQ-12 — Where the brief is silent, the design agent must make and document reasonable engineering decisions instead of inventing user requirements that were never stated.

Brief text:

> where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements

### REQ-13 — This repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not be pushed into the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

### REQ-14 — The requirements the brief does state are authoritative: they govern the design and are not to be reinterpreted, weakened or traded away against the agent's own preferences.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions

## Open — the design agent decides

### OPEN-01 — Which integrated switch IC is used - vendor, device, port configuration, integration level (integrated PHYs versus external), and package type.

The brief requires 'an integrated switch IC' and names no vendor, part or package, and does not say whether the PHYs sit inside that IC. Because the stressor list calls out BGA/QFN escape, the package choice is a real decision with routing consequences, not a detail.

*Decision:* **not yet made.**

### OPEN-02 — Whether management access is implemented as an on-board MCU or as a header, and if an MCU, which device and what it is responsible for.

The brief explicitly offers 'a small MCU or header' as alternatives and does not choose between them, name a device, or say what management functions must be reachable.

*Decision:* **not yet made.**

### OPEN-03 — The management bus and its off-board interface: which interface the switch is managed over, its pinout, voltage levels and whether it is exposed off-board at all.

The brief requires management access but is silent on the protocol, on how the interface is presented, and on whether it is for production configuration, field access, or bring-up only.

*Decision:* **not yet made.**

### OPEN-04 — Whether EEPROM/flash is populated at all, and if so its type, interface, size and how it is loaded.

The brief says 'if needed', making this conditional on the switch IC's boot and configuration model, which cannot be known until OPEN-01 is settled.

*Decision:* **not yet made.**

### OPEN-05 — Clock architecture: crystal versus oscillator, frequency, accuracy and stability grade, how many sources, and how clocks are distributed to the switch and any MCU.

The brief lists 'clocks' as a required block and states nothing about frequency, source type, tolerance or distribution.

*Decision:* **not yet made.**

### OPEN-06 — Power architecture: board input voltage and how power enters the board, the number of rails, their voltages and current budgets, regulator topology per rail, and any sequencing or ramp requirements.

The brief requires 'all power rails' but states no input, no rail count, no voltages and no currents, and says nothing about sequencing. These are consequences of the chosen switch IC and its supply recommendations, not stated requirements.

*Decision:* **not yet made.**

### OPEN-07 — Board outline, exact dimensions, aspect ratio, mounting-hole pattern and keepouts.

The brief gives only a qualitative size posture ('compact', tight enough to constrain placement) and no dimensions, mechanical envelope or enclosure.

*Decision:* **not yet made.**

### OPEN-08 — Stackup detail: whether the layer count is in fact six, the layer ordering and reference-plane assignment, dielectric materials and thicknesses, and copper weights.

Six layers is the metadata's 'likely' figure, not a requirement in the brief. The stackup must be justified by the escape and impedance needs of the chosen package.

*Decision:* **not yet made.**

### OPEN-09 — Differential-pair rules: the impedance target and its basis, intra-pair skew and inter-pair length budgets, spacing to other nets, and via count limits per pair.

The brief states no electrical routing numbers at all; these must come from the standard and the vendor's layout guidance once the IC is chosen.

*Decision:* **not yet made.**

### OPEN-10 — Magnetics implementation: discrete magnetics modules versus connectors with integrated magnetics, and single versus ganged port housings.

The brief requires 'the required magnetics/connectors' without specifying packaging. The metadata names magnetics placement as a stressor, so this choice drives the layout.

*Decision:* **not yet made.**

### OPEN-11 — Port-side termination and chassis-ground strategy: whether a common-mode termination network is fitted and in what arrangement, whether an isolation gap or moat is drawn, and how the connector shields are handled.

The brief is silent on the port boundary treatment beyond requiring magnetics; nothing in it fixes a termination network or a grounding scheme.

*Decision:* **not yet made.**

### OPEN-12 — Protection strategy for the port pins and any exposed management interface against ESD and cable-borne transients.

The brief does not mention protection at all. Any protection is an engineering decision to be justified, not a requirement the brief imposes.

*Decision:* **not yet made.**

### OPEN-13 — Package escape strategy: fan-out pattern, via technology (through-hole versus blind/buried versus via-in-pad), the pad and clearance geometry the chosen package demands, and the resulting fabrication class.

The brief is silent; the escape approach falls out of the package chosen in OPEN-01 and directly determines whether the layer count and fab capability are sufficient.

*Decision:* **not yet made.**

### OPEN-14 — Link and activity indication: whether LEDs are fitted, how many per port, and how they are driven.

The brief never mentions indicators. Adding them is allowed as an engineering choice but must not be recorded as a user requirement.

*Decision:* **not yet made.**

### OPEN-15 — Thermal strategy for the switch IC: copper area, thermal vias, whatever thermal land or pad the chosen package presents, and whether any airflow assumption is made.

The brief specifies neither an environment nor a power budget, but pairs an integrated switch IC with a deliberately compact board, so the thermal path must be reasoned about and stated.

*Decision:* **not yet made.**

### OPEN-16 — Bring-up and test provisioning: test points, programming or debug access, and how each rail and the management path is probed.

The brief says nothing about test access; the benchmark's test flow makes this a decision the design must record.

*Decision:* **not yet made.**

### OPEN-17 — Which vendor reference layout is treated as authoritative, and how any deviation from it is recorded and justified.

The brief mandates following the vendor's reference layout but the applicable document is unknown until the IC is chosen, and the brief does not say how deviations are to be handled.

*Decision:* **not yet made.**

### OPEN-18 — Fabrication and assembly targets: vendor, process class, single- versus double-sided assembly, and surface finish.

The brief names no fabricator or process constraints, yet the package escape and impedance control make the chosen capability set a binding constraint on the layout.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Answer it under its `OPEN-nn` heading above, with the reasoning and the
   evidence that made the choice.
2. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json).
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Naming a specific switch IC and then asserting reference-layout compliance without ever obtaining the vendor document. The brief makes that compliance a requirement, so an uncited claim of following it is a direct failure, not a shortcut.
- Quoting impedance, trace width and spacing numbers pulled from convention rather than from a stackup a fabricator will actually build. The brief states no electrical routing values, so every one of them must be derived and shown.
- Turning 'compact' into an invented dimension. The brief gives a placement-difficulty posture and no size at all; a stated board size is a design decision to be justified, never a requirement to be quoted back.
- Fabricating rail counts, voltages, currents, a board input or a sequencing requirement before the switch IC is chosen. These are consequences of the silicon and the vendor's supply recommendations; presenting them as brief requirements corrupts the record of what was actually specified.
- Assuming a package pitch, or an escape technology to match it, before the device is chosen. The brief and metadata say only that BGA/QFN escape is a stressor; whether blind, buried or in-pad vias are needed follows from the real ball map and the target process, not from an assumption about how fine the pitch is.
- Asserting a port-boundary scheme - common-mode termination, chassis-ground moat, creepage - from memory of typical Ethernet designs rather than from the magnetics datasheet and applicable standards.
- Adding features the brief never requested (PoE, an SFP uplink, a defined LED scheme, a console port) and then carrying them forward as though they were user requirements.
- Declaring 'management access' satisfied by a bare header without establishing what interface the chosen device is actually managed over, or whether it can reach an operational state without a host at all.
