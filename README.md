# CDR Site Intelligence

**Open DAC site suitability index. Public data. Reproducible methodology.**

→ **[Launch the tool](https://co2ri.github.io/cdr-intelligence)**

---

## What this is

A global screening tool that scores 312 locations for Direct Air Capture (DAC) deployment suitability. Built on publicly available datasets. Every scoring decision is documented and open to critique.

This is not a commercial product. It is infrastructure for the CDR research and deployment community — free to use, free to fork, and actively seeking corrections.

---

## The five factors

| Factor | What it proxies | Primary source |
|--------|----------------|----------------|
| Renewable energy potential | Solar irradiance + wind capacity factor | NREL Global Solar Atlas, Global Wind Atlas |
| Low humidity | Inverse of mean annual relative humidity | ERA5 / Copernicus Climate Change Service |
| Geological storage access | Proximity to saline aquifers and depleted reservoirs | Global CCS Institute Storage Catalogue |
| Clean grid electricity | Grid carbon intensity + wholesale cost | Electricity Maps, IEA |
| Land & infrastructure | Population density, seismic risk, access | JRC GHSL, USGS Seismic Hazard |

Weights are equal by default. The interactive sliders let you reprioritise — useful for comparing storage-first vs energy-first deployment strategies.

---

## Use it

**In the browser:** [co2ri.github.io/cdr-site-intelligence](https://co2ri.github.io/cdr-intelligence)

**Locally:**
```bash
git clone https://github.com/CO2Ri/cdr-site-intelligence
open index.html
```
No build step. No dependencies to install. One HTML file.

---

## Current limitations (v0.1)

This is a regional proxy model, not a site-level feasibility study. Known gaps:

- Water availability not yet modelled (critical for arid high-scoring sites)
- Storage-to-energy transport distance penalty not yet applied
- Policy and permitting environment not scored
- Grid scores for some countries use 2028 projections, not current conditions

Full methodology and limitations: [METHODOLOGY.md](./METHODOLOGY.md)

---

## Contribute

Corrections and improvements are welcome.

**Found a wrong score?** Open an issue with the site name, the factor, and a citable source for the correction.

**Missing a location?** Open an issue with coordinates and your proposed sub-scores with sources.

**Methodology critique?** Open a Discussion. Every substantive critique gets a response.

**New data layer?** Open a Pull Request. The data schema is in the site array inside `index.html` — each entry follows `[name, country, region, lat, lng, solar, humidity, storage, grid, land]`.

---

## Roadmap

- [ ] v0.2 — Water stress index, transport cost penalty, CSV export, uncertainty indicators
- [ ] v0.3 — Second methodology (ERW deployment suitability)
- [ ] v0.4 — API endpoint for programmatic access

---

## Citation

> CO2Ri. *CDR Site Intelligence — DAC Suitability Index, v0.1*. 2026.  
> https://github.com/CO2Ri/cdr-site-intelligence · CC BY 4.0

---

## License

Code: [MIT](./LICENSE)  
Data and methodology: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
