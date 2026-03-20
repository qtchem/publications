## Citation

> **\"The Scaled Hirshfeld Partitioning: Mathematical Development and Information-Theoretic Foundation.\"**,
> F. Heidar‐Zadeh, [Entropy](URL).


## Load Data

We use the [IOData](https://github.com/theochem/iodata) to easily load the extended XYZ file format.

```python
from iodata import load_many

# define the columns in the extended XYZ file format
# default columns (in standard XYZ format) includes atomic symbols
# and Cartesian coordinates, which is extended by five
# columns for H, SH, CM5, AVH-B, and HLYGAt atomic charges.
atom_columns = iodata.formats.xyz.DEFAULT_ATOM_COLUMNS + [
    ("atcharges", "H", (), float, float, "{:10.6f}".format),
    ("atcharges", "SH", (), float, float, "{:10.6f}".format),
    ("atcharges", "CM5", (), float, float, "{:10.6f}".format),
    ("atcharges", "AVH-B", (), float, float, "{:10.6f}".format),
    ("atcharges", "HLYGAt", (), float, float, "{:10.6f}".format),
]

# load the data from the extended xyz file
molecules = load_many("2026_entropy_scaled_hirshfeld.xyz", atom_columns=atom_columns)

# loop over the loaded molecules and print existing information for each
for i, mol in enumerate(molecules):
    print(f"\nMolecule {i+1}:")
    print("  Atomic Numbers:", mol.atnums)
    print("  Atomic Coordinates:", mol.atcoords)
    # atom.atcharges is a dictionary that contains the atomic charges for different methods
    for method, atcharges in mol.atcharges.items():
        print(f"  {method} Charges:", atcharges)
```