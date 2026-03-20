# Methodology — DAC Site Suitability Index

**Version:** 0.1  
**Status:** Open for community review  
**Last updated:** March 2026  
**License:** CC BY 4.0 — cite as: *CDR Site Intelligence, DAC Suitability Index v0.1 (2026)*

---

## Overview

This tool scores global locations for their suitability as Direct Air Capture (DAC) deployment sites. It is a composite index built entirely from publicly available datasets. It is designed to support early-stage site screening, not to replace site-level feasibility studies.

The fundamental premise is that DAC deployment cost is primarily driven by five factors: the availability of low-cost zero-carbon energy, ambient humidity (which affects capture energy demand), access to geological CO₂ storage, grid electricity quality, and land/infrastructure accessibility. This methodology encodes proxy values for each factor and combines them into a weighted composite score (0–100).

---

## Scoring Model

### Composite formula

```
Score = (w₁·Solar + w₂·Humidity_inv + w₃·Storage + w₄·Grid + w₅·Land) / (w₁+w₂+w₃+w₄+w₅)
```

All five sub-scores are normalised to 0–100. Higher is always better for DAC deployment. Default weights are equal (1.0 each). Users can adjust weights interactively to reflect different deployment priorities.

---

## Factor Definitions and Data Sources

### Factor 1 — Renewable energy potential (`solar`)

**What it measures:** The long-run average solar irradiance and wind capacity factor at each location, as a proxy for the availability of low-cost zero-carbon electricity for DAC operations.

**Why it matters:** DAC systems require 1,500–2,500 kWh of electricity and/or heat per tonne of CO₂ captured. Collocating with stranded or curtailed renewable energy is the primary lever for reducing levelized cost of carbon removal. Sites with high irradiance and/or wind resources have the potential to produce electricity below $20–30/MWh in the 2030s, which is critical for sub-$200/t DAC economics.

**Proxy method:** Values are assigned using published solar resource zone classifications from the NREL Global Solar Atlas and the Global Wind Atlas. Locations within high-irradiance zones (GHI > 5.5 kWh/m²/day) receive scores of 85–100. Temperate zones with strong wind resources receive 55–75. High-latitude low-irradiance zones receive 25–50. Iceland receives a high score (28 on solar) offset by a very high score on grid cleanliness — reflecting that geothermal rather than solar is the relevant energy source there.

**Primary source:** NREL Global Solar Atlas; IRENA Global Renewables Resource Potential (2023)  
**Secondary source:** Global Wind Atlas v3 (DTU / World Bank)

---

### Factor 2 — Low humidity index (`humidity_inv`)

**What it measures:** The inverse of mean annual relative humidity. High scores indicate dry climates; low scores indicate humid climates.

**Why it matters:** DAC systems using solid sorbents (e.g. Climeworks' amine-functionalized sorbents) perform significantly better in dry conditions. High ambient humidity increases the co-adsorption of water vapour, which competes with CO₂ for binding sites and increases regeneration energy demand. Liquid solvent systems (e.g. Carbon Engineering / 1PointFive) are less sensitive to humidity but still require energy-intensive water evaporation in humid environments. Published estimates suggest a 15–30% increase in capture energy demand moving from arid (~20% RH) to humid (~70% RH) climates.

**Proxy method:** Mean annual relative humidity from ERA5 climate reanalysis (1991–2020 climatology) was used to assign scores. Locations with mean annual RH < 25% receive scores of 88–96. RH 25–40% → 70–87. RH 40–60% → 50–69. RH > 60% → 20–49. Coastal tropical locations receive the lowest scores.

**Primary source:** ERA5 climate reanalysis, Copernicus Climate Change Service (C3S), 1991–2020 mean  
**Secondary source:** Fasihi et al. (2022), *Techno-economic assessment of CO₂ direct air capture plants*, Journal of Cleaner Production

---

### Factor 3 — Geological CO₂ storage suitability (`storage`)

**What it measures:** The proximity and quality of geological formations suitable for permanent CO₂ injection and storage, including deep saline aquifers, depleted oil and gas reservoirs, and basaltic formations.

**Why it matters:** For DAC with carbon storage (DACCS), the captured CO₂ must be permanently sequestered underground. Geological storage suitability is a hard constraint — not a cost optimisation. Without accessible storage within ~200–300 km, pipeline transport costs add $20–50/tonne and project complexity increases substantially. Proximity to high-injectivity saline aquifers or depleted hydrocarbon reservoirs with known storage capacity is the primary determinant of whether a given DAC site can achieve permanent removal at all.

**Proxy method:** Location scores are assigned based on the Global CCS Institute's CO₂ Storage Resource Catalogue and the IEA's World Energy Outlook geological storage assessments. Locations overlying or adjacent to major sedimentary basins (Permian Basin, North Sea basin, Cooper Basin AU, Tarim Basin CN, Arabian Platform) receive scores of 80–98. Locations in crystalline basement terrains with no known storage receive scores of 40–60 unless carbonate or basaltic mineralisation potential is documented. Iceland receives 98 due to the demonstrated Carbfix basalt mineralisation process.

**Primary source:** Global CCS Institute, CO₂ Storage Resource Catalogue (2023)  
**Secondary source:** IEA, *CCUS in Clean Energy Transitions* (2021); Snæbjörnsdóttir et al. (2020), *Carbon dioxide storage through mineral carbonation*, Nature Reviews Earth & Environment

---

### Factor 4 — Clean and affordable grid electricity (`grid_clean`)

**What it matters:** The current and projected carbon intensity and wholesale cost of grid electricity at each location, as a proxy for whether a DAC plant can operate on grid power without defeating its own purpose.

**Why it matters:** A DAC plant running on high-carbon grid electricity can have a negative net carbon balance — removing less CO₂ than its power supply emits. Grid carbon intensity below ~100 gCO₂/kWh is a rough threshold for net-positive operation. In addition, wholesale electricity price is the single largest operating cost component for most DAC designs. Locations with both low-carbon and low-cost grids — Nordic countries, Iceland, parts of the US Pacific Northwest — offer a structural cost advantage independent of on-site renewables.

**Proxy method:** Scores are assigned using Electricity Maps' 2023 average carbon intensity data and IEA country-level electricity price statistics. High renewable penetration grids (Iceland geothermal: ~99; Nordic hydro: 88–97; Pacific Northwest hydro: 72–82) receive top scores. Coal-heavy grids (India, parts of Southeast Asia, Eastern Europe) receive 30–52. Countries with rapidly expanding renewable grids receive scores reflecting projected 2028 conditions, noted in the data as forward-looking proxies.

**Primary source:** Electricity Maps, Annual Carbon Intensity Data 2023  
**Secondary source:** IEA, *Electricity Market Report* (2024); IRENA, *Renewable Power Generation Costs* (2023)

---

### Factor 5 — Land availability and infrastructure (`land`)

**What it measures:** A composite of available land area (low competing use, low population density), seismic hazard, proximity to industrial infrastructure (roads, rail, water supply), and permitting environment.

**Why it matters:** DAC plants at commercial scale require 0.5–5 km² of land depending on technology. Land cost, availability, and competing uses (agriculture, conservation, existing industry) are critical site selection constraints. Seismic hazard affects long-term injection well integrity. Access to water for cooling, construction logistics, and workforce availability all affect capital and operating costs.

**Proxy method:** Land scores are assigned using a combination of the Global Human Settlement Layer (population density), USGS Global Seismic Hazard Assessment, and regional infrastructure quality indices. High-scoring sites combine low population density, low seismic risk, and proximity to existing industrial corridors. The US Southwest, Australian outback, Arabian Peninsula, and Atacama region score 70–85. Dense urban areas, high seismic zones (Pacific Ring of Fire), and protected land areas receive lower scores.

**Primary source:** Global Human Settlement Layer, JRC (2023); USGS Global Seismic Hazard Program  
**Secondary source:** World Bank Logistics Performance Index (2023)

---

## Limitations and Known Issues

This is a v0.1 screening tool. The following limitations apply and are under active development:

**1. Proxy resolution.** All sub-scores are regional proxies, not site-level measurements. A score of 82 for "Tucson, USA" reflects the regional characteristics of the Sonoran Desert, not a specific parcel of land. Site-level feasibility requires dedicated surveys.

**2. Storage-energy co-location assumption.** The model implicitly assumes that all five factors can be optimised at the same location. In practice, the best geological storage sites and the best renewable energy sites are often hundreds of kilometres apart. A future version will add a transport cost penalty for storage-energy distance.

**3. Water availability not modelled.** Thermoelectric DAC designs (e.g. steam-based sorbent regeneration) require significant water. The driest, highest-scoring locations (Atacama, Sahara) may face water constraints that substantially affect DAC feasibility. Water stress index will be added in v0.2.

**4. Biomass availability excluded.** This index is for standalone DAC, not BECCS or BiCRS. Biomass proximity is not a factor.

**5. Policy and permitting environment.** Carbon capture storage permitting regimes vary enormously by jurisdiction. Some high-scoring locations (parts of North Africa, Central Asia) have limited or nonexistent CO₂ storage permitting frameworks. This is not currently reflected in scores.

**6. Forward-looking grid scores.** Grid electricity scores for several countries (India, Chile, Saudi Arabia, Morocco) reflect projected 2028 conditions based on announced renewable capacity additions, not current grid conditions. These are clearly signposted in the data where applicable.

---

## How to Contribute

This project is openly maintained. Contributions are welcome in the following forms:

**Data corrections:** If a sub-score for a specific location is clearly wrong based on published data you can cite, open a GitHub Issue using the "Report data error" button in the tool or directly at the repository.

**New data sources:** If you have access to higher-resolution proxies for any of the five factors — particularly geological storage capacity in underrepresented regions (Sub-Saharan Africa, Central Asia, Southeast Asia) — open a Pull Request with a data contribution following the schema in `data/README.md`.

**Methodology critique:** If you are a researcher working on DAC siting, CO₂ storage, or energy systems and you believe the weighting approach or proxy methodology is flawed, open a GitHub Discussion. We will engage with every substantive critique.

**New factors:** Proposals for additional factors (water stress, permafrost risk, grid frequency stability, CO₂ pipeline proximity) are welcome as GitHub Issues labelled `enhancement`.

---

## Citation

If you use this tool in research, please cite:

> CDR Site Intelligence. *DAC Site Suitability Index, v0.1*. 2026. Available at: https://github.com/CO2Ri/cdr-intelligence. Licensed under CC BY 4.0.

---

## Acknowledgements

This tool was built using exclusively open and publicly available data. It does not represent the views of any CDR company, research institution, or government body. All errors are the authors' own.

Data sources acknowledged: NREL, ERA5 / Copernicus Climate Change Service, Global CCS Institute, Electricity Maps, IEA, IRENA, Global Wind Atlas (DTU / World Bank), JRC Global Human Settlement Layer, USGS.
