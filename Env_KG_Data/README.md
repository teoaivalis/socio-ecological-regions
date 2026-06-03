# FrED: Environmental Knowledge Graph (G_E)

This folder contains the data and schemas required to establish the **Environmental Knowledge Graph ($\mathcal{G}_E$)**. This graph bridges the scale mismatch between coarse $0.25^\circ$ meteorological grids and localized geographical features, enabling high-resolution data attribution for global flood events.

---

## 🏛️ Domain Modeling & Source Integration

The Environmental Knowledge Graph ($\mathcal{G}_E$) is constructed by projecting grid-level meteorological predictions into a structured semantic space. Each flood event is anchored by precise spatial and temporal coordinates, enabling the framework to link atmospheric states directly to three primary layers of discrete domain knowledge:

1. **Biological Axis (iNaturalist):** Verified taxonomic data arranged into a deterministic hierarchy (*Kingdom* $\rightarrow$ *Species*) retrieved within a 10km radius of each flood epicenter. These biological footprints serve as proxies for localized long-term micro-climatic baselines and regional hydrological characteristics.
2. **Urban Morphology & Exposure Axis (GHSL & LCZ):** Structural density configurations mapped via the Global Map of Local Climate Zones (LCZ) and coupled with exposure profiles from the Global Human Settlement Layer (GHSL). This axis isolates population pools, settlement typologies, and volumetric building metrics to differentiate high-exposure urban centers from lower-density rural environments.
3. **Physical Land Cover Axis (ESA WorldCover):** High-resolution, 10m-resolution land-cover allocations (e.g., tree cover, wetlands, open water, and croplands) calculated within a 10km buffer zone. This layer defines the localized surface characteristics and natural water retention capabilities that influence flood severity.

---

## 📂 Folder Structure

* **`extreme_floods_updated.json`**: The foundational registry of global flood events (sourced from ExtremeKG), supplying unique disaster identifiers, temporal coordinates, and core GPS footprints to the pipeline.
* **`queries_for_floods.txt`**: A repository of reference Cypher queries used to establish database constraints, map indices, and verify topological performance inside Neo4j.
* **`flood_event_human/`**: Compiled socioeconomic data arrays linking localized flood regions to continuous human population density counts and settlement classifications.
* **`flood_event_lcz/`**: Extracted surface morphology vectors connecting specific disaster coordinates to local climate zone rough-surface sharing allocations.
* **`flood_event_species/`**: A collection of biological observations retrieved from the iNaturalist database mapping regional hubs to localized taxonomic occurrences (Kingdom $\rightarrow$ Species).
* **`GHSL/`**: A structural repository containing the global Earth Observation source rasters and grid matrices managed by the European Commission's Joint Research Centre (JRC), tracking population estimates (`GHS_POP`), surface build density (`GHS_BUILT_S`), average structural height (`GHS_BUILT_H`), volumetric totals (`GHS_BUILT_V`), and degree-of-urbanization classes (`GHS_SMOD`). (Note: You can download these data from https://human-settlement.emergency.copernicus.eu/download.php)
* **`extract_species.py`**: The automation script responsible for interfacing with the external iNaturalist endpoint to pull and filter taxonomic instances inside the spatiotemporal limits of each hazard epicenter.
* **`new_insert_floods.py`**: The Neo4j graph instantiation engine that reads the parsed geospatial JSON arrays, maps the metadata values to target node properties, and compiles transactional Cypher strings.

---

## 🏛️ Ontological Schema (Neo4j)

All data streams are formalized and instantiated within a native Neo4j graph database. To enforce a strict semantic hierarchy, the graph schema is centered on the **Region** node, which serves as the primary grounding hub linking physical hazard events (**Disasters**) directly to local ecological, morphological, and land-use vulnerabilities.

### Final Node and Edge Property Registry
The internal attributes stored within the network nodes and connecting relationships enable topological filters and graph-native representation learning:

| Element Type | Label / Edge Type | Internal Properties / Metadata Fields |
| :--- | :--- | :--- |
| **Node** | `Disaster` | `name`, `date`, `status`, `iso3`, `latitude`, `longitude`, `displacedPeople`, `housesCollapsed`, `powerOutage`, `waterSupplyCut` |
| **Node** | `Region` | `name`, `latitude`, `longitude`, `population_10km`, `built_volume_10km`, `building_density_10km`, `avg_building_height_10km`, `treesCount`, `springsCount`, `mountainsCount`, `watersCount`, `woodsCount`, `scrubsCount`, `wetlandsCount`, `grasslandsCount` |
| **Node** | `Species` | `scientificName`, `inaturalistId`, `category`, `wikipediaUrl`, `photoUrl` |
| **Node** | `LCZ_Class` | `id`, `name` |
| **Node** | `SettlementModel` | `code`, `name` |
| **Edge** | `hasLandCover` | `area_km2` |
| **Edge** | `hasBiodiversity` | `observations` |
| **Edge** | `hasMorphology` | `percentage` |

---

## 📊 Graph Connectivity & Semantic Diversity

An analysis of the structural depth across the 149 processed geographical regions reveals a dense network layout optimized for local environmental tracking:

* **Taxonomic Gradients:** The framework logs an average density of **121.24 unique species per region**, anchoring over **18,065 unique biodiversity edges** across nearly **9,910 unique Species nodes**. This configuration provides a highly localized taxonomic signature for ecological grounding.
* **Urban Exposure Stratification:** Each regional hub maintains an average of **8.25 directed morphological and urban links**. Utilizing the Global Human Settlement Layer (GHSL), the engine maps **119 regions** into the low-density infrastructure footprint of `Very low density rural`, while isolating high-exposure `Urban Centres` and `Suburban` hubs.
* **Surface Layout Configurations:** Surface variations are cross-referenced across Local Climate Zone (`LCZ_Class`) and ESA LandCover distributions, tracking regional landscape elements such as `Low plants` and `Dense trees`.

This multi-axis structural configuration replaces broad, pixel-level latent approximations with precise grounding, allowing the downstream re-ranking pipeline to identify authentic socio-environmental and physical twins.
