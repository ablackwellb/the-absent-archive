# The Absent Archive: Mapping Systemic Omission and Material Continuity in Andean Metadata

An empirical graph analysis investigating institutional data absence within **The Metropolitan Museum of Art Open Access Dataset**. Out of 484,956 master records, this project focuses on the 2,108 artifacts representing pre-Columbian Andean cultural horizons, revealing a stark historical paradox: the structural tracking count for the primary text infrastructure of the Andes—the knotted-cord **quipu**—stands at exactly **ZERO**.

This repository does not treat absence as self-explanatory proof. Instead, it maps how institutional metadata records a striking omission: within the Met’s Open Access Dataset, the structural tracking count for quipu-related terms is zero, even as other Andean materials remain present. The 1583 Third Council of Lima, which ordered the destruction of quipus, is therefore used here as historical context for interpreting archival absence, not as a cause that this dataset alone can prove.

---

## Data Provenance & Fractional Data Collection

*   **Primary Empirical Source:** [The Metropolitan Museum of Art Open Access Data](https://github.com/metmuseum/openaccess) (`MetObjects.csv`), distributed under a CC0 1.0 Universal designation.

*   **Full Collection Scope:** 484,956 objects parsed.

*   **Target Andean Subset:** 2,108 objects isolated via explicit cultural filter hooks (*Chavín, Paracas, Nasca, Moche, Tiwanaku, Wari, Lambayeque/Sicán, Chimú, Chancay, Inca*).

*   **Temporal and Spatial Baseline Data:** This pipeline queries the live data repository streaming directly from the museum's distribution endpoint. Because curatorial teams actively update records, this network represents a diagnostic repository snapshot captured in **July 2026**.

---

## Algorithmic Ingestion & Fractional Data Auditing

To test whether this zero-count reflects a simple cataloging miss, a keyword limitation, or a broader institutional absence, the pipeline executes a multi-stage validation check over the full Met dataset. The result does not prove the cause of the omission; it establishes the shape and consistency of the absence within this repository snapshot.

| Audit Phase | Strategy Type | Target Filter Parameters & Regex | Scope Evaluated | Outcome & Metric Verified |
| :--- | :--- | :--- | :--- | :--- |
| **Phase 1: Direct** | Explicit Search | `\b(quipu\|khipu\|quipo)\b` | 484,956 Objects | **0 Matches Found** |
| **Phase 2: Archaic** | Synonym Search | `\b(knot-record\|knot record\|knotted cord\|knotted string\|quipucamayoc\|khipukamayug\|accounting device\|peruvian thread\|talk knots\|talking knot\|assembled cords)\b` | 484,956 Objects | **0 Hits** |
| **Phase 3: Material** | Manual Review Sweep | `\b(Fiber/textile objects in quipu-forming materials)\b` | 422 Andean textiles | **Reviewed; no misfiled cord-records identified** |


### Archival Data Sparseness Analysis
The diagnostic audit may expose systematic metadata fragmentation downstream from cultural racketeering, illicit antiquities trafficking, and the resulting separation of unique Andean fiber records from their stratigraphic contexts:
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

## Interactive graph

[Open the network visualization](https://ablackwellb.github.io/andean-heritage-network/Andean_Network_Betweenness_Centrality.html)

### This interactive PyVis graph maps Andean culture and medium co-occurrences, with node size scaled to betweenness centrality and node styling used to distinguish materials and uncertain classifications.

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

This is a single institution's collection, not the Andean world entire. The Met's holdings reflect its own acquisition history, and the absence of quipu here is institutional, not universal — surviving quipu exist in scattered collections elsewhere (notably in Peru, Chile, and Germany, and catalogued in part by Harvard's Khipu Database Project). A natural extension is to compare a second institution's Andean holdings to see how differently each reconstructs the same lost world. With this being said, this repository uses graph analysis to examine a historical paradox: when textual infrastructures are absent from institutional metadata, surviving physical substances—ceramics, camelid hair, cotton, and other materials—may still preserve traces of civilizational continuity.

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
