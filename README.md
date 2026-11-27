# Neuro Data Analysis

Exploratory analyses of open neuroscience datasets with Python and **pandas**.

| # | Project | Notebook | Methods |
|---|---|---|---|
| 1 | Human vs. mouse cortical neurons | `allen_cell_types_analysis.ipynb` | `groupby`, `agg`, `apply`, text cleaning |
| 2 | Combining neuron data from several tables | `allen_merging_analysis.ipynb` | `concat`, `merge` (left / inner / outer), `join` |

Both projects use the **Allen Cell Types Database** (see *Data* below).

---

## 1 · Human vs. Mouse Cortical Neurons

Exploratory analysis of the electrophysiological properties of **2,333 single neurons** from human and mouse cortex.

**Questions**
1. Do human and mouse cortical neurons differ in their basic membrane properties (resting potential, input resistance, membrane time constant)?
2. Which cell types fire fastest – spiny (mostly excitatory) or aspiny (mostly inhibitory) neurons?
3. How is spike width related to dendrite type?
4. In human donors: do membrane properties differ between age groups?

**Key findings**

| | Human | Mouse |
|---|---|---|
| Resting potential (mV) | −69.6 | −71.9 |
| Input resistance (MΩ) | 145.2 | 181.4 |
| Membrane time constant (ms) | 25.3 | 17.9 |

- Human neurons have a **longer membrane time constant** and a **lower input resistance** than mouse neurons.
- In both species, **aspiny neurons fire much faster** (~42–47 Hz) than spiny neurons (~14–28 Hz).
- **Narrow spikes** occur almost exclusively in aspiny cells (524 vs. 10 in spiny cells) – consistent with fast-spiking inhibitory interneurons.
- In human donors, membrane properties hardly differ between donors under 40 and 40 and older.

---

## 2 · Combining Neuron Data from Several Tables

Real research databases store information in **separate tables**. Here the Allen data is split into four tables – neurons, electrophysiology, human donors and a (deliberately incomplete) lookup table of brain areas – and combined again.

**Questions**
1. Which rows survive a left, inner and outer join – and what gets lost?
2. How many neurons lack electrophysiological data or an area annotation?
3. How do firing rate and membrane time constant differ between cortical systems (visual, temporal, frontal) and dendrite types?

**Key findings**
- A left join with the area lookup table keeps all **2,333** neurons; **153** neurons come from areas missing in the lookup table, so an inner join keeps only **2,180**.
- An outer join with `indicator=True` reveals one area in the lookup table without any recorded neurons (primary motor area, MOp).
- **157** neurons have no electrophysiological recording – a `merge` without `how=` (default: inner join) silently drops them.
- The 413 human neurons come from only **42 donors** (many-to-one merge): counts of neurons and counts of donors must be computed from different tables.
- In every cortical system, **aspiny neurons fire fastest**; the human temporal cortex shows a clearly longer membrane time constant (≈ 27 ms) than the mouse visual cortex (≈ 18 ms).

---

## Data

- **Source:** Allen Institute for Brain Science – [Allen Cell Types Database](https://celltypes.brain-map.org/)
- **Download:** cell-level summary table via the Allen Brain Map API:
  `http://api.brain-map.org/api/v2/data/query.csv?criteria=model::ApiCellTypesSpecimenDetail,rma::options[num_rows$eqall]`
- Save the file as `allen_cells.csv` and adjust the variable `PFAD` at the top of each notebook to its location.
- 2,333 neurons (1,920 mouse, 413 human), 54 columns

*Note: These are descriptive, exploratory analyses without statistical testing.*

## Tools

Python 3 · pandas · Jupyter Notebook

## About

These projects are part of my work on data analysis for neuroscience (MSc Neurosciences, University of Bonn).

**Data citation:** Allen Institute for Brain Science (2015). Allen Cell Types Database. Available from celltypes.brain-map.org.
