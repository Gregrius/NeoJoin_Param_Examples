# NeoJoin SPL Examples

This repository contains examples for using [NeoJoin](https://github.com/vitruv-tools/NeoJoin) in the context of Software Product Lines.

The `templates` folder contains a set of reusable templates for adding variability information to existing models.
The templates rely on a UVL-based feature model, and on the Vitruvius correspondence model from [Vitruv-Change](https://github.com/vitruv-tools/Vitruv-Change) for the feature-to-artifact mapping.

The `car-infotainment` folder contains a complete hypothetical example of an SPL, including all the necessary metamodals, instance files and NeoJoin queries. Refer to the [car-infotainment/README.md](car-infotainment/README.md) for details. It relies on an extention of NeoJoin to support parameterized queries (currently available in this [NeoJoin fork](https://github.com/Gregrius/NeoJoin/tree/param)).