# The Absent Archive
### Mapping Systemic Omission and Material Continuity in Andean Metadata
 
> The Metropolitan Museum of Art holds 484,956 objects, including 2,108 from Andean cultures. Andean cultures like the Inka Empire kept their records and accounting using *khipukuna* (also known as the *khipu*, which is a Quechua term for "knots"). **The Met holds none.**
 
This project treats that absence as its subject. Among Andean cultures, the *khipu* (a Quechua word meaning "knot"), was the primary system of record-keeping, computing, and accounting. Presently, and globally, around 900 khipu remain. These remaining khipu are scattered across three continents and 88 collections in museums. The remaining khipu, and the metadata that museums assign to them, are our only available way to reconstruct the shape of the Andean world. This network visualizes what holds the picture together when so much is missing.

## What was Discovered

Using the Met's open-access data, I built a network linking Andean objects to their **cultures** and **materials**, then used **betweenness centrality** to find the connective tissue — the attributes that bridge otherwise-separate parts of the Andean world. While reviewing the data, I found that there were no khipu (also referred to as *quipu*), in their collection's database. When this was discovered, the question being asked gained a new meaning... 

## The Question

If the records kept by a society are absent, what pieces connect the past to tell their story?
 
## Data
 
- **Source:** [The Metropolitan Museum of Art Open Access](https://github.com/metmuseum/openaccess) (`MetObjects.csv`), CC0 1.0 Universal.
- **Full collection:** 484,956 objects.
- **Andean subset:** 2,108 objects, filtered by culture (Moche, Paracas, Chimú, Nasca, Inca, Wari, Chancay, Lambayeque/Sicán, Tiwanaku, Chavín, and related/uncertain attributions).
- **khipu in the collection:** 0.
  
## Verifying the Absence
 
To confirm the zero reflects a genuine absence rather than a cataloging quirk, the notebook runs three checks:
 
| Check | What it does | Scope | Result |
|---|---|---|---|
| **Direct term search** | `(?i)\b(quipu\|khipu\|quipo)\b` across Object Name, Title, Classification | 484,956 objects | **0 matches** |
| **Archaic-synonym sweep** | historical / pre-standardization terms (knotted cord, quipucamayoc, khipukamayuq, talking knot, and others) | 484,956 objects | **0 matches** |
| **Material-form review** | Andean textile/fiber objects in khipu-forming materials, reviewed for misfiled cord-records | 422 records | **none found** |
 
## Honest Handling of Absence
 
Two fields were too sparse to build on, and rather than impute I preserved the gaps as part of the record:
 
- **Period:** unrecorded for all 2,108 objects.
- **Region:** recorded for only 201 (under 10%).

> Imputing them would mean inventing certainty the source doesn't support — the exact over-confident reconstruction this project is about. The network is built only on the fields that are complete: **Culture** and **Medium**. The sparseness is consistent with objects separated from their original excavation contexts; the data can show the gap, not prove its cause.
 
Curatorial uncertainty is also kept visible, as hedged attributions like "Chimú (?)" or "Moche or Chancay" remain in the graph as their own nodes. The uncertainty is, itself, evidence of reconstruction from material alone.
 
## The Network
 
- **Nodes:** 2,258 (objects + their culture and material attributes)
- **Edges:** 5,509
- **Distinct materials after cleaning:** 109
- **Metric:** betweenness centrality — which attribute nodes sit on the most paths between everything else.
![Andean network — betweenness centrality](Epistemology_of_Absence.png)
 
**▶ [Explore the interactive graph](https://ablackwellb.github.io/andean-heritage-network/Andean_Network_Betweenness_Centrality.html)** — drag, zoom, and hover for object type and betweenness scores.
 
## What the Network Reveals
 
| Rank | Node | Type | Betweenness |
|---|---|---|---|
| 1 | Moche | culture | 0.360 |
| 2 | ceramic | material | 0.292 |
| 3 | camelid hair | material | 0.158 |
| 4 | silver | material | 0.103 |
| 5 | cotton | material | 0.102 |
| 6 | Chimú | culture | 0.102 |
| 7 | copper | material | 0.094 |
| 8 | Inca | culture | 0.089 |
| 9 | Paracas | culture | 0.072 |
| 10 | pigment | material | 0.063 |
 
Two findings stand out. **Moche** is the single greatest bridge in the network — its objects share attributes across more of the Andean world than any other culture. And the top connectors are overwhelmingly **materials, not cultures**: ceramic, camelid hair, and cotton are what stitch distinct peoples together. When the written record is gone, these attributes can reveal the connections.
 
## Visualization
 
The interactive graph (created using PyVis) is styled to carry the argument:
 
- **Materials by vulnerability:** organic fibers in coral (perishable), inorganic ceramics in blue (durable survivors), precious metals in gold (frequently looted or melted).
- **Geometry of doubt:** securely identified cultures as circles, hedged attributions as diamonds.
- **Node size** scales with betweenness centrality, computed on the full object-plus-attribute graph.
- **Note:** for readability, the visualization shows the projected attribute view of **~52 nodes**.
  
## Method
 
1. Filter the Met open-access CSV to Andean objects.
2. Verify the khipu absence (three checks above).
3. Split and normalize the `Medium` field into individual materials.
4. Build a bipartite graph of objects → cultures + materials (`networkx`).
5. Compute betweenness centrality; project to an attribute graph for visualization (`pyvis`).

## Limitations

This is a single institution's collection, not the Andean world entire. The Met's holdings reflect its own acquisition history, and the absence of khipu here is institutional, not universal. The surviving khipu exist in scattered collections across North America, South America, and Europe - notably: Peru, Chile, and Germany. Harvard's Department of Anthropology contains the Khipu Database (HDAKD) which also catalogues the remaining khipu into the Open Khipu Repository, where each khipu is assigned a KH number. *A natural extension to this will be to compare a second institution's Andean holdings to see how differently each reconstructs the same lost world.*

## Repository Contents
 
- `MET.ipynb` — full analysis notebook (loading, verification, cleaning, network, betweenness, visualization)
- `Epistemology_of_Absence.png` — static network visualization
- `Andean_Network_Betweenness_Centrality.html` — interactive network (open in a browser)
- `requirements.txt` · `README.md`

## Running It
 
```bash
pip install -r requirements.txt
jupyter notebook # open MET.ipynb and Run All
```
 
*Or headless:*
 
```bash
jupyter nbconvert --to notebook --execute MET.ipynb --output MET.executed.ipynb
```
 
## References

- OKR Team. (2025). *The Open Khipu Repository.* (v2.1.0) Zenodo. https://doi.org/10.5281/zenodo.6908343
- Quilter, J., & Urton, G. (Eds.). (2002). *Narrative Threads: Accounting and Recounting in Andean Khipus.* University of Texas Press.
- The Metropolitan Museum of Art. (2024). *MetObjects: Open Access Dataset.* CC0 1.0. https://github.com/metmuseum/openaccess
- Trouillot, M.-R. (1995). *Silencing the Past: Power and the Production of History.* Beacon Press.
- Urton, G. (2002). *The Khipu Database Project.* Department of Anthropology, Harvard University.
- Urton, G. (2003). *Signs of the Inka Khipu: Binary Coding in the Andean Knotted-Cord Records.* University of Texas Press.

---
 
**Ashley Blackwell** — Applied Data Scientist
[LinkedIn](https://linkedin.com/in/ablackwellb) · [GitHub](https://github.com/ablackwellb) · [Hugging Face](https://huggingface.co/ablackwellb)
