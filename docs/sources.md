# Sources — Five-Port Gigabit Ethernet Switch

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Switch IC datasheet: ball or pad map, package dimensions and pitch, per-rail supply voltages and currents, strapping pins, and thermal characteristics | Everything downstream - rail count, escape strategy, thermal copper, configuration model - is a consequence of the chosen device, and the brief fixes none of it. |
| Switch vendor hardware design guide, reference schematic and reference layout package | The brief makes following the vendor's reference layout a hard requirement, so the actual document must be cited rather than paraphrased from convention. |
| Vendor PHY supply and power-rail recommendations, including decoupling, filtering, sequencing and ripple limits | The brief separately names PHY supply recommendations as something to follow, making them a distinct citable source from the general layout guide. |
| IEEE 802.3 1000BASE-T clauses: signalling, channel and port-interface requirements | The brief names 1000BASE-T, so port-level electrical claims should trace to the standard that defines it rather than to the switch datasheet alone. |
| LAN magnetics datasheet: turns ratio, common-mode choke configuration, insulation and isolation ratings, pinout and placement notes | Magnetics placement is a listed stressor and the brief requires magnetics on the board; the part's own constraints drive the port-side layout. |
| Port connector datasheet: footprint and mechanical drawing, retention, shield tabs, and integrated-magnetics pinout where applicable | The connector fixes the port pitch and much of the escape geometry on a deliberately compact board, and drives where the port face ends up. |
| Regulator and power-device datasheets plus their reference designs and layout sections | The brief requires all rails with no values stated, so each rail's topology and layout must be justified from its own device documentation. |
| Clock source datasheet: frequency tolerance, stability over temperature, jitter or phase noise, and load capacitance requirements | The brief requires clocks but states no parameters; the acceptability of a source has to be shown against what the switch IC demands. |
| Fabricator capability and impedance-controlled stackup documents for the chosen layer count | The escape and the differential impedance target are only credible if the trace, space, via and stackup values come from a real process the fabricator publishes. |
| Assembly-house process capability for the chosen BGA or QFN package: land pattern, stencil, paste and inspection requirements | BGA/QFN escape is a named stressor, and the design is only manufacturable if the pad and via geometry match a documented assembly process at the package's actual pitch. |
| IPC land-pattern, stackup and high-speed design standards | Provides the neutral basis for footprint geometry and layout practice where no vendor or fabricator document covers the question. |
| ESD and EMC standards and application notes for Ethernet port boundaries | Any protection, shield-handling or isolation-gap choice is an engineering decision the brief does not make, so it needs external grounding to be defensible. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
