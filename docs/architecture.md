# Architecture — Five-Port Gigabit Ethernet Switch

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- many Ethernet differential pairs
- BGA/QFN escape
- multiple supplies
- magnetics placement

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## Switch IC selection and port architecture

- Which integrated switch IC is chosen, and what evidence supports that it provides five 1000BASE-T ports as required?
- Are the PHYs integrated in the switch device, or does the architecture need external PHYs - and if external, is that still 'an integrated switch IC' as the brief requires?
- What package does the device come in, and what is its pitch, ball or pad count and body size?
- What management model does the device use - does it need a host to come up, or can it operate unmanaged after strapping?
- Does the device require external non-volatile configuration storage, which decides whether REQ-07's conditional EEPROM/flash applies?
- What is the device's total power draw and per-rail current, and where is that figure sourced from?

## Port front-end: magnetics, connectors and termination

- Are magnetics discrete or integrated into the port connectors, and what drove that choice?
- Are the five ports in individual housings or ganged, and how does that interact with the compact board size the brief demands?
- How far can magnetics sit from the connector and from the switch IC, and what does the vendor layout guidance say about that distance?
- Is any common-mode termination network fitted on the cable side - and if so, in what arrangement, and what evidence supports it?
- How are connector shields and any chassis ground handled relative to signal ground, and is a boundary between them drawn on the board at all?
- If such a boundary is drawn, what isolation or creepage distance is held across it, and on what basis?

## Differential-pair routing and signal integrity

- What differential impedance target is set for the 1000BASE-T pairs, and what document establishes it?
- What intra-pair skew and inter-pair length budgets apply, and how are they verified after routing?
- How many pairs must be routed in total across five ports, and does the compact outline leave room for all of them without violating spacing rules?
- Which layers carry the pairs, and does every pair have a continuous reference plane over its whole length?
- How many vias is a pair allowed, and what is done about the reference-plane transition at each one?
- What minimum spacing is kept between adjacent pairs and between pairs and unrelated nets, given the brief's explicit refusal to grant unlimited space?

## Package escape and stackup

- What is the escape strategy for the chosen package, and how many layers does it actually consume?
- Does the escape require blind, buried or in-pad vias, and does the intended fabricator support them at the required drill and pad sizes?
- Is six layers sufficient, or does the escape plus the pair routing force a different count - and is that change documented as a deviation from the metadata's likely figure?
- What is the full stackup: layer order, dielectric materials and thicknesses, copper weights, and which layers are the reference planes?
- Does that stackup produce the impedance target of the previous section with trace geometry the fabricator can build?
- What minimum trace and space does the escape demand, and is it within the chosen process class?

## Power architecture

- What supplies does the chosen switch IC require, at what voltages, tolerances and currents, and what is the source for each figure?
- What is the board's input - voltage, how power enters the board, and the expected source - and is that a decision or an assumption?
- What regulator topology is chosen for each rail, and what evidence - including anything the vendor's PHY supply recommendations say about noise, ripple or filtering - supports that choice rail by rail?
- Does the device impose a power-up sequence or ramp-rate constraint, and if it does, how is it enforced?
- What decoupling does the vendor's PHY supply recommendation call for, per rail and per pin group, and is it placed as the reference layout shows?
- If any rail uses a switching regulator, how are its loops and radiated fields kept away from the port pairs and magnetics on a board this small?

## Clocking

- What clock source or sources does the design use, at what frequency, and what does the switch IC require?
- What frequency accuracy and stability does 1000BASE-T operation demand of that source, and where is that requirement documented?
- Is the clock a crystal, an oscillator, or fed from elsewhere, and what load or drive-level constraints follow?
- How is the clock net routed, and what - if anything - is done to keep it from coupling into the Ethernet pairs?
- Does any MCU or management block need its own clock, or does it share?

## Management, configuration and bring-up

- Is management implemented as an on-board MCU or as a header, and what is the reasoning?
- If a header, what signals does it carry, at what logic levels, and what external equipment is assumed to drive it?
- If an MCU, what does it actually do at power-up, and does the switch depend on it to become operational?
- How is any EEPROM/flash written in production, and is that path reachable on an assembled board?
- What strapping or configuration pins does the switch IC have, and how is each one resolved in the schematic?
- What is the minimum sequence of steps to prove the board is alive, and what test points does that sequence need?

## Placement and mechanical

- What board outline and dimensions are chosen, and how do they satisfy the brief's demand that placement be forced rather than easy?
- Where do the five ports sit relative to the board edge, and does that face imply an enclosure or panel this design must assume?
- How is the switch IC placed relative to the five port groups so that pair lengths stay within budget for all five?
- Which components are on the bottom side, if any, and does that force double-sided assembly?
- Where are mounting holes, and what keepouts do they impose on the pair routing?

## Grounding, ESD and EMC

- What is the ground topology across the board, and is it split anywhere - if so, on what evidence?
- How does an ESD or cable-borne transient event on a port pin reach ground, and what handles it?
- Is any port protection fitted beyond the magnetics, and if so, is its capacitance compatible with 1000BASE-T signalling?
- What return-current paths exist under each differential pair, and are any of them interrupted?
- What is the strategy for keeping supply and clock emissions from radiating out through the cable ports?

## Thermal

- What is the estimated total board dissipation with five ports active, and how was it derived?
- How is heat removed from the switch IC package - copper pours, thermal vias, whatever thermal land the package provides - and how much area does that need?
- Does the compact outline leave enough copper area for that, or does it conflict with the routing channels?
- What ambient and airflow conditions are assumed, and is that an assumption or a stated constraint?

## Vendor reference-layout compliance

- Which specific vendor document is being followed as the reference layout, and has it actually been read?
- Which of its recommendations were followed as written, and which could not be, given the board size the brief demands?
- For each deviation, what is the justification and what risk does it carry?
- Do the PHY supply recommendations in that document match the power architecture chosen above, rail by rail?
- Is there a vendor schematic or layout checklist, and has every item on it been checked off with a result?

## Manufacturability and test

- What fabricator and process class is the design targeting, and does the escape strategy fit inside its stated capability?
- Is every footprint traceable to a datasheet land pattern or a documented standard?
- Can each of the five ports be tested independently, and what does that require on the board?
- What test points are needed to verify every power rail and the clock without cutting traces?
- What in the design is most likely to fail assembly, and what design choice reduces that risk?

## Answers still owed

All of them. See [status.md](status.md).
