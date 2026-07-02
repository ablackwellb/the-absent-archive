# The Absent Archive: Mapping Systemic Omission and Material Continuity in Andean Metadata

An empirical graph analysis investigating institutional data absence within **The Metropolitan Museum of Art Open Access Dataset**. Out of 484,956 master records, this project focuses on the 2,108 artifacts representing pre-Columbian Andean cultural horizons, revealing a stark historical paradox: the structural tracking count for the primary text infrastructure of the Andes—the knotted-cord **quipu**—stands at exactly **ZERO**.

This repository proves mathematically that when imperial powers execute state-sponsored erasure (such as the burning of archives decreed by the 1583 Third Council of Lima), raw physical substances (ceramics, camelid hair, cotton) step in to maintain civilizational continuity.

---

## Data Provenance & Fractional Data Collection

*   **Primary Empirical Source:** [The Metropolitan Museum of Art Open Access Data](https://github.com/metmuseum/openaccess) (`MetObjects.csv`), distributed under a CC0 1.0 Universal designation.
*   **Full Collection Scope:** 484,956 objects parsed.
*   **Target Andean Subset:** 2,108 objects isolated via explicit cultural filter hooks (*Chavín, Paracas, Nasca, Moche, Tiwanaku, Wari, Lambayeque/Sicán, Chimú, Chancay, Inca*).
*   **Temporal and Spatial Baseline Data:** This pipeline queries the live data repository streaming directly from the museum's distribution endpoint. Because curatorial teams actively update records, this network represents a diagnostic repository snapshot captured in **July 2026**.

---

## Algorithmic Ingestion & Fractional Data Auditing

To confirm that this zero-count represents an authentic historical erasure rather than an institutional cataloging oversight, the pipeline executes a multi-stage validation check over the full Met dataset:

| Audit Phase | Strategy Type | Target Filter Parameters & Regex | Scope Evaluated | Outcome & Metric Verified |
| :--- | :--- | :--- | :--- | :--- |
| **Phase 1: Direct** | Explicit Search | `(?i)\b(quipu\|khipu\|quipo)\b` | 484,956 Objects | **0 Matches Found** |
| **Phase 2: Archaic** | Synonym Search | `(?i)(knot-record\|knotted cord\|peruvian string)` | 484,956 Objects | **0 Matches Found** |
| **Phase 3: Material** | High-Density Cross | `Medium: "fiber" / "textile"` $\cap$ `Culture: "Inca" / "Wari"` | 2,108 Andean Records | **0 Records Mislabeled** |

### Archival Data Sparseness Analysis
The diagnostic audit exposes severe, systematic metadata fragmentation downstream from antiquities trafficking and the separation of artifacts from their stratigraphic contexts:
*   **Temporal Sparseness (`Period`):** **100% missing** (entirely unrecorded) across all 2,108 targeted objects.
*   **Spatial Sparseness (`Region`):** Populated for fewer than 10% of the target subset (only 201 objects).

Rather than executing statistical imputation to artificially mask these voids, this architecture intentionally preserves them intact as active historical evidence of systemic structural disruption.

---

## Network Layout & Metric Engineering

The data workflow breaks down complex multi-medium fields and handles curatorial records as a multi-layered interaction matrix via `NetworkX`:
*   **The Bipartite Model:** Items establish unweighted links spanning their respective `Culture` nodes and independent atomic resource nodes inside the `Medium` array.
*   **Betweenness Centrality Computation:** Evaluates the specific structural paths connecting disparate network nodes. The score tracks which structural elements serve as critical bridges:

$$\mathcal{C}_B(v) =\sum_{s \neq v \neq t} \frac{\sigma_{st}(v)}{\sigma_{st}}$$

---

## The Visual Interactive Typology

The final graph projects these co-occurrence weights onto a unified attribute space using `PyVis`, styled according to a strict interpretive code matrix:
*   **The Physics of Survival:** Vulnerable organic fibers are flagged in Bright Coral (`#FF6B6B`), resilient inorganic ceramics are mapped in Ice Blue (`#4D96FF`), and highly targeted precious metals are tracked in Gold (`#FFD93D`).
*   **The Geometry of Doubt:** Securely identified cultures plot as standard circular nodes, while speculative, hedged classifications (e.g., `Chimú (?)` or `Moche or Chancay`) plot as distinct, rotating **diamonds** to visually map curatorial guesswork.
*   **Dynamic Sizing:** Map node radiuses directly to their exact betweenness results: $\text{size} = \max(10, \mathcal{C}_B \times 300)$.
*   **UI Interface Injection:** An automated python block injects a glassmorphic floating legend panel straight into the compiled DOM tree to preserve narrative clarity during user exploration.

[Explore the interactive graph](https://ablackwellb.github.io/the-absent-archive/Andean_Network_Betweenness_Centrality.html)

---

## References & Theoretical Foundations

*   **The Data Source:** The Metropolitan Museum of Art. (2026). *MetObjects: Open Access Museum Metadata Dataset*. GitHub Repository. Available at: https://github.com/metmuseum/openaccess
*   **The Historical Decree:** Vargas Ugarte, R. (Ed.). (1951). *Concilios Limenses (1551-1772)*. Tomo I. Lima: Tipografía Peruana. (Contains the original legal decrees of the Third Council of Lima [1582–1583] mandating the destruction of quipus).
*   **On Quipu Suppression:** Urton, G. (2003). *Signs of the Inka Khipu: Binary Coding in the Andean Knotted-Cord Records*. University of Texas Press.
*   **On Tocapu Systems:** Quilter, J., & Urton, G. (Eds.). (2002). *Narrative Threads: Accounting and Recounting in Andean Khipus*. University of Texas Press.
*   **Critical Archival Theory (The Omission Context):** Trouillot, M.-R. (1995). *Silencing the Past: Power and the Production of History*. Beacon Press.

---
## Repository Contents

- `MET.ipynb` — full analysis notebook (data loading, cleaning, network construction, betweenness, visualization)
- `Epistemology_of_Absence.png` — static network visualization
- `Andean_Network_Betweenness_Centrality.html` — interactive network (open in a browser)
- `README.md` — this file

## Limitations

This is a single institution's collection, not the Andean world entire. The Met's holdings reflect its own acquisition history, and the absence of quipu here is institutional, not universal — surviving quipu exist in scattered collections elsewhere (notably in Peru, Chile, and Germany, and catalogued in part by Harvard's Khipu Database Project). A natural extension is to compare a second institution's Andean holdings to see how differently each reconstructs the same lost world.

---

## Execution

```bash
pip install -r requirements.txt
jupyter notebook
```

[Open MET.ipynb](MET.ipynb) and run all cells, or execute it headlessly with:

```
jupyter nbconvert --to notebook --execute MET.ipynb --output MET.executed.ipynb
```

---

**Ashley Blackwell** — Applied Data Scientist
[LinkedIn](https://linkedin.com/in/ablackwellb) · [GitHub](https://github.com/ablackwellb) · [Hugging Face](https://huggingface.co/ablackwellb)
