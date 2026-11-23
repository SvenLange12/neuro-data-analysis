# Human vs. Mouse Cortical Neurons – Allen Cell Types Database

Exploratory analysis of the electrophysiological properties of **2,333 single neurons** from human and mouse cortex, using Python and **pandas**.

## Questions

1. Do human and mouse cortical neurons differ in their basic membrane properties (resting potential, input resistance, membrane time constant)?
2. Which cell types fire fastest – spiny (mostly excitatory) or aspiny (mostly inhibitory) neurons?
3. How is spike width related to dendrite type?
4. In human donors: do membrane properties differ between age groups?

## Data

- **Source:** Allen Institute for Brain Science – [Allen Cell Types Database](https://celltypes.brain-map.org/)
- **Download:** cell-level summary table via the Allen Brain Map API:
  `http://api.brain-map.org/api/v2/data/query.csv?criteria=model::ApiCellTypesSpecimenDetail,rma::options[num_rows$eqall]`
- Save the file as `allen_cells.csv` in the same folder as the notebook.
- 2,333 neurons (1,920 mouse, 413 human), 54 columns

## Methods

- Selecting and renaming relevant columns, cleaning categorical values
- Handling missing values (`count` vs. `size`, `isna`)
- Group comparisons with `groupby`, `agg` and `unstack`
- Custom classification functions with `apply` (spike width: upstroke/downstroke ratio < 2 = "narrow")
- Converting text to numbers (`"25 yrs"` → `25`) with `str.split`

## Key findings

| | Human | Mouse |
|---|---|---|
| Resting potential (mV) | −69.6 | −71.9 |
| Input resistance (MΩ) | 145.2 | 181.4 |
| Membrane time constant (ms) | 25.3 | 17.9 |

- Human neurons have a **longer membrane time constant** and a **lower input resistance** than mouse neurons.
- In both species, **aspiny neurons fire much faster** (~42–47 Hz) than spiny neurons (~14–28 Hz).
- **Narrow spikes** occur almost exclusively in aspiny cells (524 vs. 10 in spiny cells) – consistent with fast-spiking inhibitory interneurons.
- In human donors, membrane properties hardly differ between donors under 40 and 40 and older.

*Note: This is a descriptive, exploratory analysis without statistical testing.*

## Tools

Python 3 · pandas · Jupyter Notebook

## About

This project is part of my work on data analysis for neuroscience (MSc Neurosciences, University of Bonn).

**Data citation:** Allen Institute for Brain Science (2015). Allen Cell Types Database. Available from celltypes.brain-map.org.
