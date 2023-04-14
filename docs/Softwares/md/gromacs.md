---
title: GROMACS
---

[GROMACS](https://www.gromacs.org) is a versatile package to perform molecular dynamics, i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

It is primarily designed for biochemical molecules like proteins, lipids and nucleic acids that have a lot of complicated bonded interactions, but since GROMACS is extremely fast at calculating the nonbonded interactions (that usually dominate simulations) many groups are also using it for research on non-biological systems, e.g. polymers.

## Availability

```python exec="on"
import pandas as pd

df = pd.read_csv('docs/assets/tables/module.csv')
soft = df.query('Software == "GROMACS"')
print(soft.to_markdown(index=False))
```


## Related Applications

* [LAMMPS](./lammps.md)

## User Contributed Information

!!! info "Please help us improve this page"
        Users are invited to contribute helpful information and corrections
        through our [Github repository](https://github.com/arcs-njit-edu/Docs/blob/main/CONTRIBUTING.md).


