# agrisolar-platform
End-to-end agri cold chain feasibility- from solar PV design to financial analysis, in a browser

A single-file, zero-dependency browser application that integrates physics-based solar PV design with ASHRAE cold storage sizing and full techno-economic analysis — built for farmers, agri-entrepreneurs, NGO field workers, and policy planners with no engineering background.

What Problem Does This Solve?
India's cold chain infrastructure deficit ranges from 85% to 99.6% across facility types (pack houses, cold hubs, ripening chambers, reefer vehicles). A farmer evaluating a solar-powered cold storage investment currently needs:

A solar installer (PV sizing)
A refrigeration contractor (cold room design)
A financial advisor (feasibility analysis)

Three separate, inconsistent engagements. AgriSolar replaces all three with one browser tab.

Workflow
The platform runs as a guided 4-step pipeline:
Step 1- Location & Crop Input
The user enters their location and selects a crop from a database of 50+ crops, each with ASHRAE 2018 (Ch. 35) crop-specific storage temperatures and respiration rates. Location drives irradiance retrieval; crop drives both thermal sizing and revenue modelling.
Step 2- Solar PV Design

Retrieves NASA POWER monthly climatological irradiance data for the site
Synthesises energy-conserving hourly irradiance profiles
Performs continuous tilt–azimuth optimisation for maximum plane-of-array (POA) irradiance
Calculates worst-case inter-row shading from winter-solstice geometry
Runs land-constrained layout optimisation
Corrects azimuth to magnetic bearing
Outputs a full Bill of Materials and panel layout drawing
Structural compliance: IS 875-3 (wind loads), IS 800 (steel structures)
Validated against PVGIS across 10 Indian cities: <0.3% deviation in annual energy yield

Step 3- Cold Storage Thermal Sizing
A 7-component ASHRAE heat load engine covering:

Wall, floor, and ceiling transmission
Product pull-down load
Door infiltration
Fan motor heat
Lighting load
Respiration heat (crop-specific)
Miscellaneous internal gains

Output: refrigeration tonnage (TR), unit selection from Daikin India catalogue, IS 11665–compliant PUF panel specification. Cross-validated using CoolPack — convergence within ±10%.
Step 4-Techno-Economic Analysis
Solar BOM output automatically populates the financial model. The engine runs:

20-year DCF in real (constant) rupees at 10% real WACC
NPV, IRR, MIRR, simple payback, and discounted payback
1,000 Monte Carlo simulations per run using Ornstein-Uhlenbeck price paths with jump diffusion and harvest-price negative correlation (ρ = −0.40)
P5 / P50 / P95 NPV scenarios — usable directly in AIF loan applications
Bear / Base / Bull scenario matrix
Tornado sensitivity chart
Side-by-side revenue comparison: income with vs. without cold storage
Real-time sensitivity slider: harvest volume ±50%

Sample output (Capsicum, Pune): NPV ₹35.2L | IRR 39.8% | Payback 3 years | PI 3.94× | Total CAPEX ₹12.0L

Key Features

Zero installation — runs entirely in the browser, single HTML file
Device-agnostic — works on desktop, tablet, mobile
50+ crops with validated ASHRAE storage parameters
10 Indian cities validated against PVGIS
IS / ASHRAE standards compliant throughout
No backend, no API keys, no dependencies


Validation
ComponentMethodResultSolar PV yieldPVGIS comparison, 10 cities<0.3% deviationCold room heat loadCoolPack software±10% convergencePrice modellingOrnstein-Uhlenbeck vs Agmarknet modal pricesMean-reverting, empirically calibratedFinancial modelManual DCF audit vs tool outputExact match

Limitations

Solar module uses a fixed performance ratio (PR = 0.80); does not resolve temperature-dependent efficiency, soiling losses, or annual degradation
Heat load follows ASHRAE steady-state methodology; transient defrost cycles and pull-down dynamics are not modelled
Financial model assumes single-crop, single-season storage; polyculture and multi-tenant configurations are not implemented
Commodity prices are calibrated to Agmarknet national modal prices, which may differ from local mandi conditions
Fixed-tilt systems only — solar tracking, agrivoltaic elevated structures use the same geometric engine without modification
No electrical modelling — inverter sizing, DC/AC ratio, wiring losses, and module degradation are outside scope (addressed in bankability-grade tools like PVsyst)
Single-chamber cold rooms with uniform PUF insulation per IS 11665 — multi-chamber, controlled atmosphere, and blast-freeze configurations are out of scope


Future Scope
1. Heat Pump Integration
Replace the conventional vapour-compression unit with a solar-driven heat pump, thermodynamically coupling its COP profile to the PV generation curve. This would reduce diesel backup dependency and improve overall system efficiency, particularly during peak summer irradiance.
2. Extended Economic Analysis
Add explicit tax shield modelling, MNRE/PM-KUSUM subsidy tranches, AIF loan auto-population, DSCR analysis, and depreciation schedules. Include polyculture and multi-tenant storage economics where multiple farmers share a single cold room.
3. Bifacial PV & Advanced Irradiance Modelling
Extend the irradiance engine to model bifacial rear-side gain, incorporate Perez transposition for diffuse irradiance, and add soiling and degradation rates for a full bankability-grade yield estimate.
4. Direct AIF Application Output
Auto-generate populated annexures for Agriculture Infrastructure Fund loan applications based on the platform's techno-economic outputs — reducing the documentation barrier for smallholder applicants.
5. Real-Time Agmarknet Price Integration
Replace static crop price tables with live Agmarknet API feeds, enabling the Monte Carlo engine to calibrate OU parameters to actual rolling mandi price data for the user's district.

Related Work
This platform integrates and extends a standalone PV optimization framework:
Physics-Based PV Layout Optimization Framework
Reproducible framework for early-stage PV system orientation and land-constrained layout optimization — the solar engine that powers the AgriSolar Platform.

Standards & References

ASHRAE Refrigeration Handbook, 2018, Chapter 35
IS 11665: Cold Storage — Code of Practice
IS 875-3:2015: Wind Loads on Structures
IS 800:2007: General Construction in Steel
NASA POWER Climatological Data
PVGIS (JRC European Commission) — validation benchmark
Daikin India Catalogue — refrigeration unit selection
