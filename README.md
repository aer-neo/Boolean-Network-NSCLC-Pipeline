# NSCLC Boolean Network Reduction, Update-Scheme Analysis, and Rule Fitting

This repository contains the code and rule files used to reproduce the Boolean-network analyses for the manuscript:

> **Boolean-network simplification and rule fitting to unravel chemotherapy resistance in non-small cell lung cancer**  
> Alonso Espinoza, Eric Goles, Marco Montalva-Medel

The study reconstructs a published Boolean model of cisplatin/pemetrexed resistance in non-small-cell lung cancer (NSCLC), reduces it from **31 → 29 → 14 → 9 nodes**, evaluates synchronous and deterministic asynchronous dynamics, and applies Boolean rule fitting to remove spurious limit cycles while preserving the biologically relevant steady states: **Drug Resistance**, **Senescence**, and **Apoptosis**.

---

## Quick access: Google Colab notebooks

The Python notebooks can be run directly in Google Colab. Each notebook starts with an upload cell. When prompted, upload the corresponding BoolNet rule file (`nsclc_*.txt`) from this repository. The uploaded file path is stored in the notebook variable `file_rules` and reused by the following cells.

| Notebook | Purpose | Open in Colab |
|---|---|---|
| `Graph_NSCLC_Regulatory_Networks.ipynb` | Optional utility for drawing regulatory-network topology plots; the network figures in the manuscript were generated directly in TikZ. | <a href="https://colab.research.google.com/drive/1_I153wo_OhP5FxJhrQqSIHUwqnuuL_W1?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab" width="180"></a><br><a href="https://colab.research.google.com/drive/1_I153wo_OhP5FxJhrQqSIHUwqnuuL_W1?usp=sharing">Direct Colab link</a> |
| `Graph_NSCLC_Attraction_Basin.ipynb` | Draws synchronous attraction-basin maps for the 9-node NSCLC networks. | <a href="https://colab.research.google.com/drive/1hNmI-0QloeKSaUudv89rfALHLYL7mkNp?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab" width="180"></a><br><a href="https://colab.research.google.com/drive/1hNmI-0QloeKSaUudv89rfALHLYL7mkNp?usp=sharing">Direct Colab link</a> |
| `Different_Asynchronous_Update_Scheme_Tools.ipynb` | Enumerates representative deterministic update schemes and simulates attractors/basins for each equivalence class. | <a href="https://colab.research.google.com/drive/1A1uE1Mo-341J4lidbnlyNrkY4awhbxj6?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab" width="180"></a><br><a href="https://colab.research.google.com/drive/1A1uE1Mo-341J4lidbnlyNrkY4awhbxj6?usp=sharing">Direct Colab link</a> |
| `Fitting_Boolean_Rules_in_GNR.ipynb` | Performs exhaustive Boolean rule fitting for the 9-node core network. | <a href="https://colab.research.google.com/drive/1Hnxgjy5EJ6-6r1Lr3txCEYXcFfyCfPX6?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab" width="180"></a><br><a href="https://colab.research.google.com/drive/1Hnxgjy5EJ6-6r1Lr3txCEYXcFfyCfPX6?usp=sharing">Direct Colab link</a> |

---

## Single-repository reproducibility workflow

This repository is intended to contain the complete reproducibility package for the manuscript: the R script, the Python notebooks, all BoolNet rule files, and this README. A reviewer should be able to reproduce the main results by cloning or downloading this repository and then running the scripts/notebooks with the rule files included here.

### How to load the data

- **R synchronous simulations:** run `Simulation_synchrone.R` from the repository root and set `file_rules <- "./<rule_file>.txt"` in the configuration block.
- **Python notebooks in Colab:** open the relevant Colab notebook, run the first upload cell, and select the required `nsclc_*.txt` file from this repository.
- **Python notebooks locally:** place the notebooks and `nsclc_*.txt` files in the same working directory, open the notebook with Jupyter, and run the upload/load cell or set `file_rules` manually to the desired rule file path.

### What each workflow should produce

| Workflow | Main input files | Main expected outputs |
|---|---|---|
| Synchronous simulations | `nsclc_31_nodes_without_terminal.txt`, `nsclc_29_nodes.txt`, `nsclc_14_nodes.txt`, `nsclc_9_nodes.txt`, `nsclc_9_nodes_fit.txt` | `attractors_and_basins_<network>_<suffix>.csv` files with attractors, basin sizes, and basin percentages. |
| Optional network plotting | Any `nsclc_*.txt` rule file | `<base_name>_gene_regulatory_network.svg` and `<base_name>_gene_regulatory_network.png`; these plots are not the TikZ figures used in the manuscript. |
| 9-node basin maps | `nsclc_9_nodes.txt`, `nsclc_9_nodes_fit.txt` | `Basin_Attraction/` directory plus `<base_name>_Basin_Attraction.zip`. |
| Deterministic update-scheme analysis | `nsclc_9_nodes.txt`, `nsclc_9_nodes_fit.txt` | `determining_distinct_update_schemes/` outputs and a downloadable ZIP archive. |
| Boolean rule fitting | `nsclc_9_nodes.txt` | `All_rules.csv` and `Summary_inference.txt`; the selected fitted rule is already encoded in `nsclc_9_nodes_fit.txt`. |

---

## Repository contents

| File | Purpose |
|---|---|
| `Simulation_synchrone.R` | R/BoolNet script for synchronous attractor and basin-size simulations. It also supports **in silico perturbation assays** through forced ON/OFF genes. |
| `Graph_NSCLC_Regulatory_Networks.ipynb` | Optional Python notebook for drawing regulatory-network topology plots as PNG/SVG. The manuscript network figures were generated directly in TikZ. Colab: [open notebook](https://colab.research.google.com/drive/1_I153wo_OhP5FxJhrQqSIHUwqnuuL_W1?usp=sharing). |
| `Graph_NSCLC_Attraction_Basin.ipynb` | Python notebook for drawing synchronous attraction-basin maps for the 9-node networks. Basin maps are exported as PNG/SVG/HTML plus a ZIP archive. Colab: [open notebook](https://colab.research.google.com/drive/1hNmI-0QloeKSaUudv89rfALHLYL7mkNp?usp=sharing). |
| `Different_Asynchronous_Update_Scheme_Tools.ipynb` | Python notebook for enumerating representative deterministic update schemes using update-digraph equivalence classes and simulating attractors/basins for each representative scheme. Colab: [open notebook](https://colab.research.google.com/drive/1A1uE1Mo-341J4lidbnlyNrkY4awhbxj6?usp=sharing). |
| `Fitting_Boolean_Rules_in_GNR.ipynb` | Python notebook for exhaustive Boolean rule fitting in the 9-node core network. It searches candidate Boolean rules that preserve the desired fixed points and remove spurious attractors. Colab: [open notebook](https://colab.research.google.com/drive/1Hnxgjy5EJ6-6r1Lr3txCEYXcFfyCfPX6?usp=sharing). |
| `nsclc_31_nodes.txt` | BoolNet-format rules for the reconstructed 31-node NSCLC network, including terminal phenotype nodes. Included for complete rule documentation and graphing. |
| `nsclc_31_nodes_without_terminal.txt` | BoolNet-format rules for the reconstructed network after removing terminal phenotype outputs. This is the file used to simulate the upstream regulatory part of the 31-node model with `Simulation_synchrone.R`. |
| `nsclc_29_nodes.txt` | BoolNet-format rules for the 29-node reduced network. |
| `nsclc_14_nodes.txt` | BoolNet-format rules for the 14-node reduced network under the persistent DNA-damage condition. |
| `nsclc_9_nodes.txt` | BoolNet-format rules for the minimal 9-node regulatory core. |
| `nsclc_9_nodes_fit.txt` | BoolNet-format rules for the final rule-fitted 9-node network. The BMI1 rule is replaced by `(!p53_A & !p53_K) | E2F1`. |
| `README.md` | Reproducibility instructions. |

---

## Input file format

All Boolean networks are provided as plain-text CSV files in **BoolNet-compatible format** with the following header:

```text
targets,factors
```

Boolean operators:

| Operator | Meaning |
|---|---|
| `&` | AND |
| <code>&#124;</code> | OR |
| `!` | NOT |

Example, from the 9-node core network:

```text
targets,factors
miR_145,p53 & !MALAT1 & !BMI1
Sp1,(BMI1) | !miR_145
MALAT1,Sp1
BMI1,E2F1
KLF4,!miR_145 | (E2F1 & p53)
p53,!KLF4 | !MALAT1
p53_A,!p53_K & p53
p53_K,!p53_A & p53
E2F1,MALAT1
```

---

## Software requirements

### Recommended route: Google Colab

For the Python notebooks, use the Colab links above. Colab is recommended for reviewers because it avoids local environment setup. The first cell of each notebook uploads the required rule file and stores its path in the variable `file_rules`.

### R synchronous simulations

Tested with:

- R 4.3.3
- BoolNet
- tools, included with base R

Install the R dependency:

```r
install.packages("BoolNet")
```

### Local Python execution

Tested with Python 3.10.5. Core packages:

```bash
pip install numpy pandas networkx matplotlib pyvis pydot dot2tex
```

For Graphviz layouts on Linux/Colab:

```bash
apt-get -y install graphviz libgraphviz-dev
pip install pygraphviz
pip install pydot dot2tex pyvis
```

Launch Jupyter locally with, for example:

```bash
jupyter notebook Graph_NSCLC_Regulatory_Networks.ipynb
jupyter notebook Graph_NSCLC_Attraction_Basin.ipynb
jupyter notebook Different_Asynchronous_Update_Scheme_Tools.ipynb
jupyter notebook Fitting_Boolean_Rules_in_GNR.ipynb
```

---

## Reproducing the synchronous simulations

Use `Simulation_synchrone.R` to reproduce the synchronous attractors and basin sizes reported for the reconstructed and reduced networks.

### 1. Select the network

Edit the configuration block at the top of `Simulation_synchrone.R`:

```r
file_rules <- "./nsclc_9_nodes_fit.txt"
```

To reproduce each network, replace `file_rules` with one of:

```r
file_rules <- "./nsclc_31_nodes_without_terminal.txt"
file_rules <- "./nsclc_29_nodes.txt"
file_rules <- "./nsclc_14_nodes.txt"
file_rules <- "./nsclc_9_nodes.txt"
file_rules <- "./nsclc_9_nodes_fit.txt"
```

Use `nsclc_31_nodes_without_terminal.txt` for the upstream regulatory component of the reconstructed 31-node network. The full `nsclc_31_nodes.txt` file is included for complete rule documentation and can be used for graphing, but the manuscript’s synchronous reproducibility workflow uses the version without terminal phenotype outputs.

### 2. Wild type versus perturbation assays

For manuscript baseline tables, use the wild-type setting:

```r
genes_ON  <- c()
genes_OFF <- c()
```

For **in silico mutation / perturbation assays**, force one or more genes ON or OFF. For example:

```r
genes_ON  <- c("miR_145", "p53_A")
genes_OFF <- c("BMI1")
```

This uses BoolNet's `genesON` and `genesOFF` arguments inside `getAttractors()`. Do not use forced ON/OFF genes when reproducing the wild-type manuscript tables.

### 3. Run the script

```bash
Rscript Simulation_synchrone.R
```

The script writes a semicolon-separated CSV file:

```text
attractors_and_basins_<network>_<perturbation_suffix>.csv
```

Examples:

```text
attractors_and_basins_nsclc_9_nodes_WT.csv
attractors_and_basins_nsclc_9_nodes_fit_miR_145_ON_p53_A_ON_BMI1_OFF.csv
```

The output contains one row per gene plus two summary rows: `BasinSize` and `BasinPercentage`.

---

## Optional network plots and attraction-basin maps

The regulatory-network figures included in the manuscript were generated directly in TikZ. `Graph_NSCLC_Regulatory_Networks.ipynb` is retained only as an optional visualization utility and is not mapped to any manuscript figure.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1_I153wo_OhP5FxJhrQqSIHUwqnuuL_W1?usp=sharing)

Direct Colab URL:

```text
https://colab.research.google.com/drive/1_I153wo_OhP5FxJhrQqSIHUwqnuuL_W1?usp=sharing
```

### Optional network topology plots

1. Open `Graph_NSCLC_Regulatory_Networks.ipynb` in Google Colab or Jupyter.
2. Run **Upload BoolNet rules file** and select a BoolNet rule file.
3. Run **Package Installation** if using Colab or if the Graphviz dependencies are missing locally.
4. Run **Graph network (SVG + PNG) with Graphviz (anti-overlap)**.

Output files:

```text
<base_name>_gene_regulatory_network.svg
<base_name>_gene_regulatory_network.png
```

Suggested inputs for optional topology plots:

| Optional visualization | Input file | Output |
|---|---|---|
| 29-node reduced network figure | `nsclc_29_nodes.txt` | `nsclc_29_nodes_gene_regulatory_network.svg/png` |
| 14-node reduced network figure | `nsclc_14_nodes.txt` | `nsclc_14_nodes_gene_regulatory_network.svg/png` |
| 9-node minimal network figure | `nsclc_9_nodes.txt` | `nsclc_9_nodes_gene_regulatory_network.svg/png` |
| 9-node fitted network figure | `nsclc_9_nodes_fit.txt` | `nsclc_9_nodes_fit_gene_regulatory_network.svg/png` |

### Attraction-basin map

Use `Graph_NSCLC_Attraction_Basin.ipynb`.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1hNmI-0QloeKSaUudv89rfALHLYL7mkNp?usp=sharing)

Direct Colab URL:

```text
https://colab.research.google.com/drive/1hNmI-0QloeKSaUudv89rfALHLYL7mkNp?usp=sharing
```

The basin-map cell is intended for the **9-node networks**, because it enumerates all `2^9 = 512` states and draws the global state-transition map.

1. Open `Graph_NSCLC_Attraction_Basin.ipynb` in Google Colab or Jupyter.
2. Upload `nsclc_9_nodes.txt` or `nsclc_9_nodes_fit.txt`.
3. Run the Graphviz/package-installation cell if needed.
4. Run **Basins & Attractors global & per-basin maps (PNG/SVG + HTML)**.

Default outputs:

```text
Basin_Attraction/<base_name>_attractors_summary_sync.csv
Basin_Attraction/<base_name>_basins_map_sync_plain.svg
Basin_Attraction/<base_name>_basins_map_sync_plain.png
Basin_Attraction/<base_name>_basins_map_sync_interactive_plain.html
<base_name>_Basin_Attraction.zip
```

Expected synchronous basin sizes for `nsclc_9_nodes.txt`:

| Attractor / phenotype | Basin size | Percentage |
|---|---:|---:|
| Drug Resistance | 504 | 98.44% |
| Senescence | 2 | 0.39% |
| Apoptosis | 2 | 0.39% |
| Limit cycle of length 2 | 4 | 0.78% |

Expected synchronous basin sizes for `nsclc_9_nodes_fit.txt`:

| Attractor / phenotype | Basin size | Percentage |
|---|---:|---:|
| Drug Resistance | 508 | 99.22% |
| Senescence | 2 | 0.39% |
| Apoptosis | 2 | 0.39% |

---

## Reproducing deterministic asynchronous update-scheme analyses

Use `Different_Asynchronous_Update_Scheme_Tools.ipynb`.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1A1uE1Mo-341J4lidbnlyNrkY4awhbxj6?usp=sharing)

Direct Colab URL:

```text
https://colab.research.google.com/drive/1A1uE1Mo-341J4lidbnlyNrkY4awhbxj6?usp=sharing
```

This notebook performs both stages in one workflow:

1. It enumerates representative update schemes by grouping block-sequential schedules into update-digraph equivalence classes.
2. It simulates one representative per equivalence class and computes attractors/basins.
3. It writes CSV/TXT outputs and creates a ZIP archive for download.

### Original 9-node network

1. Open the notebook in Google Colab or Jupyter.
2. Upload `nsclc_9_nodes.txt` when prompted.
3. Run **Enumerate and simulate all equivalence classes (update-digraphs)**.

Expected console output for `nsclc_9_nodes.txt`:

```text
Total brute-force schedules: 7087261
Equivalence classes (update-digraphs): 10632
```

Main outputs:

```text
determining_distinct_update_schemes/equiv_classes.csv
determining_distinct_update_schemes/Attractor_Results_equiv_class.csv
determining_distinct_update_schemes/summary_attractors_equiv_class.txt
nsclc_9_nodes_determining_distinct_update_schemes.zip
```

Expected summary for the original 9-node network:

| Result category | Number of representative schemes | Percentage |
|---|---:|---:|
| Only the three steady states | 7,356 | 69.19% |
| Includes at least one limit cycle | 3,276 | 30.81% |
| Total representatives | 10,632 | 100% |

Among the cycle-producing schemes, the manuscript reports 2,836 schemes with one limit cycle, 362 with two limit cycles, and 78 with five limit cycles.

### Rule-fitted 9-node network

Repeat the workflow using:

```text
nsclc_9_nodes_fit.txt
```

Expected console output for `nsclc_9_nodes_fit.txt`:

```text
Total brute-force schedules: 7087261
Equivalence classes (update-digraphs): 23107
```

Main outputs:

```text
determining_distinct_update_schemes/equiv_classes.csv
determining_distinct_update_schemes/Attractor_Results_equiv_class.csv
determining_distinct_update_schemes/summary_attractors_equiv_class.txt
nsclc_9_nodes_fit_determining_distinct_update_schemes.zip
```

Expected summary for the rule-fitted network:

| Result category | Number of representative schemes | Percentage |
|---|---:|---:|
| Only the three steady states | 21,858 | 94.59% |
| Includes at least one limit cycle | 1,249 | 5.41% |
| Total representatives | 23,107 | 100% |

Among the cycle-producing schemes, the manuscript reports 586 schemes with one limit cycle, 534 with two limit cycles, and 129 with three limit cycles. All detected limit cycles are of length 2.

---

## Reproducing Boolean rule fitting

Use `Fitting_Boolean_Rules_in_GNR.ipynb`.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Hnxgjy5EJ6-6r1Lr3txCEYXcFfyCfPX6?usp=sharing)

Direct Colab URL:

```text
https://colab.research.google.com/drive/1Hnxgjy5EJ6-6r1Lr3txCEYXcFfyCfPX6?usp=sharing
```

The rule-fitting notebook takes the 9-node core network, computes its synchronous fixed points, and exhaustively searches candidate Boolean expressions that preserve exactly those desired fixed points while removing the unwanted synchronous limit cycle. For the analysis reported in the manuscript, candidate rules were restricted to a maximum of three regulators and self-regulation was not allowed.

### Steps

1. Open `Fitting_Boolean_Rules_in_GNR.ipynb` in Google Colab or Jupyter.
2. Upload:

```text
nsclc_9_nodes.txt
```

3. Run **Upload BoolNet Rules File**. Expected network summary:

```text
The network contains 9 nodes.
Average K (mean number of regulators per node): 1.89
```

4. Run **Fitting and validation of rules using real-time fixed-point calculation**. When prompted, use the following search configuration:

```text
MAX_VARS_PER_RULE   = 3
ALLOW_SELF_IN_RULES = False
```

Expected fixed points, in node order `miR_145, Sp1, MALAT1, BMI1, KLF4, p53, p53_A, p53_K, E2F1`:

```text
[0, 1, 1, 1, 1, 0, 0, 0, 1]
[1, 0, 0, 0, 0, 1, 0, 1, 0]
[1, 0, 0, 0, 0, 1, 1, 0, 0]
```

Notebook outputs:

```text
All_rules.csv
Summary_inference.txt
```

The notebook evaluates all candidate Boolean expressions generated from combinations of up to three regulators, excluding the target node itself to prevent self-loops. For each target node, a candidate is first tested for functional agreement on the three desired fixed points and is then evaluated in the complete network dynamics. Under this configuration, the exhaustive search returns 52 dynamically admissible substitutions across the nine target nodes. Every admissible substitution preserves exactly the three desired fixed points and removes the unwanted synchronous limit cycle. The complete evaluation, including the 52 admissible substitutions, is recorded in `All_rules.csv`; the admissible rules are also summarized by target node in `Summary_inference.txt`.

The exhaustive output should not be interpreted as containing only five rules. A subsequent review of the 52 dynamically admissible substitutions prioritized five candidates for detailed biological comparison. Expected biologically prioritized candidates, ordered by the revised biological-evidence ranking, are:

| Biological-evidence rank | Target node | Candidate rule | Use in the fitted model |
|---:|---|---|---|
| 1 | `BMI1` | `(!p53_A & !p53_K) \| E2F1` | Selected |
| 2 | `MALAT1` | `(!p53_A & !p53_K) \| Sp1` | Biologically plausible alternative |
| 3 | `miR_145` | `(p53_A \| p53_K) & !MALAT1` | Biologically plausible alternative |
| 4 | `p53` | `(!p53_A \| !p53_K) & !MALAT1` | Biologically plausible alternative |
| 5 | `p53` | `(!p53_A \| !p53_K) & !KLF4` | Biologically plausible alternative |

The rank-1 BMI1 rule was carried forward into the fitted-network analyses:

```text
BMI1 = (!p53_A & !p53_K) | E2F1
```

This selected rule is already included in:

```text
nsclc_9_nodes_fit.txt
```

After generating or confirming `nsclc_9_nodes_fit.txt`, rerun:

1. `Simulation_synchrone.R` with `file_rules <- "./nsclc_9_nodes_fit.txt"`.
2. `Different_Asynchronous_Update_Scheme_Tools.ipynb` with `nsclc_9_nodes_fit.txt`.
3. `Graph_NSCLC_Attraction_Basin.ipynb` with `nsclc_9_nodes_fit.txt`, if a fitted-network basin map is required.

---

## Mapping files to manuscript results

| Manuscript result | Script/notebook | Input file(s) | Main output(s) |
|---|---|---|---|
| Reconstructed 31-node synchronous dynamics, S4 Table | `Simulation_synchrone.R` | `nsclc_31_nodes_without_terminal.txt`; `nsclc_31_nodes.txt` for complete rule documentation | `attractors_and_basins_nsclc_31_nodes_without_terminal_WT.csv` |
| 29-node synchronous results, Table 1 | `Simulation_synchrone.R` | `nsclc_29_nodes.txt` | `attractors_and_basins_nsclc_29_nodes_WT.csv` |
| 14-node synchronous results, S7 Table | `Simulation_synchrone.R` | `nsclc_14_nodes.txt` | `attractors_and_basins_nsclc_14_nodes_WT.csv` |
| 9-node synchronous results, Table 2 | `Simulation_synchrone.R` | `nsclc_9_nodes.txt` | `attractors_and_basins_nsclc_9_nodes_WT.csv` |
| 9-node basin map, S5 Fig | `Graph_NSCLC_Attraction_Basin.ipynb` | `nsclc_9_nodes.txt` | `Basin_Attraction/*`, `nsclc_9_nodes_Basin_Attraction.zip` |
| 9-node deterministic update-scheme analysis, S9–S10 Tables | `Different_Asynchronous_Update_Scheme_Tools.ipynb` | `nsclc_9_nodes.txt` | `determining_distinct_update_schemes/equiv_classes.csv`, `determining_distinct_update_schemes/Attractor_Results_equiv_class.csv`, `determining_distinct_update_schemes/summary_attractors_equiv_class.txt`, `nsclc_9_nodes_determining_distinct_update_schemes.zip` |
| Rule-fitting candidate rules, S11 Table | `Fitting_Boolean_Rules_in_GNR.ipynb` | `nsclc_9_nodes.txt` | `All_rules.csv`, `Summary_inference.txt` |
| Fitted 9-node Boolean rules, S12 Table | `Fitting_Boolean_Rules_in_GNR.ipynb` and selected-rule substitution | `nsclc_9_nodes.txt` | `nsclc_9_nodes_fit.txt` |
| Fitted 9-node synchronous results, S13 Table | `Simulation_synchrone.R` | `nsclc_9_nodes_fit.txt` | `attractors_and_basins_nsclc_9_nodes_fit_WT.csv` |
| Fitted 9-node deterministic update-scheme analysis, S14–S15 Tables | `Different_Asynchronous_Update_Scheme_Tools.ipynb` | `nsclc_9_nodes_fit.txt` | `determining_distinct_update_schemes/equiv_classes.csv`, `determining_distinct_update_schemes/Attractor_Results_equiv_class.csv`, `determining_distinct_update_schemes/summary_attractors_equiv_class.txt`, `nsclc_9_nodes_fit_determining_distinct_update_schemes.zip` |
| Combined fitted-network perturbation, S16 Table | `Simulation_synchrone.R` | `nsclc_9_nodes_fit.txt`; force `miR_145=1`, `p53_A=1`, and `BMI1=0` | `attractors_and_basins_<network>_<perturbation_suffix>.csv` |
| Qualitative basin/clinical comparison, Table 3 | `Simulation_synchrone.R`; `Different_Asynchronous_Update_Scheme_Tools.ipynb` | `nsclc_14_nodes.txt`, `nsclc_9_nodes.txt`, `nsclc_9_nodes_fit.txt` | Synchronous basin CSVs and asynchronous summary outputs listed above |

---

## Expected synchronous basin percentages

These values can be used as a quick check that the code and input files are being run correctly.

| Network | Expected attractors / phenotypes | Expected basin percentages |
|---|---|---|
| `nsclc_29_nodes.txt` | Proliferation, Drug Resistance, Senescence, Apoptosis, limit cycle | 50.00%, 49.89%, 0.01%, 0.04%, 0.05% |
| `nsclc_14_nodes.txt` | Drug Resistance, Senescence, Apoptosis, limit cycle | 98.44%, 0.39%, 0.39%, 0.78% |
| `nsclc_9_nodes.txt` | Drug Resistance, Senescence, Apoptosis, limit cycle | 98.44%, 0.39%, 0.39%, 0.78% |
| `nsclc_9_nodes_fit.txt` | Drug Resistance, Senescence, Apoptosis | 99.22%, 0.39%, 0.39% |

---

## Notes on computational scope

- The R script is intended for synchronous simulations with BoolNet and for in silico perturbation assays using forced ON/OFF genes.
- The reconstructed full `nsclc_31_nodes.txt` file is provided for completeness, while `nsclc_31_nodes_without_terminal.txt` is the practical file used for synchronous simulation of the upstream regulatory part of the 31-node reconstruction.
- The reduced `nsclc_29_nodes.txt`, `nsclc_14_nodes.txt`, `nsclc_9_nodes.txt`, and `nsclc_9_nodes_fit.txt` files can be simulated directly with the R script.
- The asynchronous update-scheme notebook is intended for the 9-node networks, where all `2^9 = 512` initial states can be exhaustively simulated for every representative update scheme.
- The rule-fitting notebook performs exhaustive candidate-rule evaluation on the 9-node network only. Applying the same exhaustive search directly to the 31-node network is not computationally practical without additional pruning or heuristic search.

---

## Citation

If you use this code, please cite the associated manuscript:

```bibtex
@article{espinoza_nsclc_boolean_network,
  title  = {Boolean-network simplification and rule fitting to unravel chemotherapy resistance in non-small cell lung cancer},
  author = {Espinoza, Alonso and Goles, Eric and Montalva-Medel, Marco},
  year   = {2026},
  note   = {Manuscript under review}
}
```

Also cite the original NSCLC Boolean model reconstructed in the manuscript:

```bibtex
@article{gupta2024dynamic,
  title   = {A dynamic Boolean network reveals that the BMI1 and MALAT1 axis is associated with drug resistance by limiting miR-145-5p in non-small cell lung cancer},
  author  = {Gupta, Shantanu and Silveira, Daner A. and Piedade, Gabriel P. S. and Ostrowski, Miguel P. and Mombach, Jos\'e Carlos M. and Hashimoto, Ronaldo F.},
  journal = {Non-coding RNA Research},
  volume  = {9},
  number  = {1},
  pages   = {185--193},
  year    = {2024}
}
```

---
