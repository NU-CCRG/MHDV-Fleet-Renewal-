# MHDV Fleet Renewal: Emissions, Air Quality, Health, and Equity Analysis

## Overview

This repository contains code, workflows, and supporting analyses used to evaluate how alternative assumptions regarding medium- and heavy-duty vehicle (MHDV) activity, idling behavior, and fleet age distributions influence emissions, air quality, population exposure, health outcomes, and environmental justice metrics across the Greater Chicago region.

The project builds upon the EPA 2022v1 Emissions Modeling Platform and incorporates:

* Telematics-derived truck idling activity (LOCUS)
* HDV-specific on-road activity distributions
* Alternative fleet age distributions generated using MOVESv4.0
* WRF-CMAQ air quality simulations
* Population-weighted exposure analyses
* Health impact assessments

The overall workflow evaluates how inventory assumptions propagate through the emissions → air quality → exposure → health impact chain.

---

# Repository Structure

```text
MHDV-Fleet-Renewal
│
├── AgeDistribution
├── IdlingModifications
├── EmissionAnalysis
├── Air Quality & Health
└── Renewal & Zero Legacy
```

---

# Workflow Overview

```text
Vehicle Fleet Data
        │
        ▼
AgeDistribution
        │
        ├── Modified Fleet Age Distributions
        └── Modified MOVES Emission Factors
                     │
                     ▼
        Renewal & Zero Legacy
                     │
                     ▼

LOCUS Telematics Data
        │
        ▼
IdlingModifications
        │
        ├── County-Level Activity Updates
        ├── Spatial Surrogates
        └── SMOKE Input Modifications
                     │
                     ▼

EPA 2022v1 Emissions Platform
        │
        ▼
SMOKE Emissions Processing
        │
        ▼
EmissionAnalysis
        │
        ├── Gridded Emissions
        └── Population-Weighted Emissions
                     │
                     ▼

WRF-CMAQ Simulations
        │
        ▼
Air Quality & Health
        │
        ├── Concentration Changes
        ├── Exposure Assessment
        ├── Health Impacts
        └── Equity Analysis
```

---

# Directory Descriptions

---

## AgeDistribution

This directory develops alternative fleet age distributions and evaluates differences between default MOVES assumptions, Vehicle Inventory and Use Survey (VIUS) observations, and local freight fleet datasets.

### Objectives

* Evaluate regional truck age distributions.
* Compare MOVES default age distributions against observed fleet data.
* Develop alternative age distributions for sensitivity simulations.
* Generate modified emission factors using standalone MOVESv4.0 simulations.

### Key Analyses

* VIUS state-level fleet age distributions
* Local freight fleet age distributions
* License state analyses
* County-level emissions comparisons using alternative age distributions

### Outputs

* Fleet age distribution figures
* County-level emissions comparisons
* Inputs for fleet renewal simulations

---

## IdlingModifications

This directory incorporates telematics-derived LOCUS idling activity into the EPA 2022v1 Emissions Modeling Platform.

### Objectives

* Replace default EPA truck idling assumptions with observed idling activity.
* Create spatial surrogates representing actual idling locations.
* Modify county-level activity inputs used by SMOKE.

### Workflow

1. Convert gridded LOCUS activity into county-level totals.
2. Generate spatial surrogates using the CMAS Spatial Allocator.
3. Modify EPA county-level idling activity inputs.
4. Update MGREF files to incorporate LOCUS spatial surrogates.
5. Generate comparison figures between EPA and LOCUS estimates.

### Key Outputs

* County-level idling activity tables
* LOCUS spatial surrogates
* Modified SMOKE input files
* Activity comparison figures

---

## Renewal & Zero Legacy

This directory develops alternative fleet age scenarios and updates MOVES emission factors used by the EPA emissions platform.

### Scenarios

#### Accelerated Fleet Renewal

All pre-2010 trucks are replaced with model year 2022 vehicles.

#### Zero Legacy Trucks

All pre-2010 trucks are removed from the fleet.

### Workflow

1. Modify MOVES age distributions.
2. Run standalone MOVESv4.0 simulations.
3. Generate scenario-specific emission factors.
4. Replace default EPA emission factors.
5. Create modified SMOKE input files.

### Key Outputs

* Modified age distributions
* Updated emission factors
* Scenario-specific SMOKE inputs

---

## EmissionAnalysis

This directory evaluates how inventory modifications influence gridded emissions and population-weighted emissions burdens.

### Objectives

* Quantify emissions differences between scenarios.
* Evaluate spatial redistribution of emissions.
* Assess population-weighted emissions burdens.

### Scenarios Compared

* EPA Default
* LOCUS Idling
* HDV On-Road Activity
* LOCUS + HDV Activity
* Accelerated Fleet Renewal
* Zero Legacy Trucks

### Outputs

#### Gridded Products

* Annual-average emissions maps
* Difference maps
* Percent-change maps

#### Population-Weighted Products

* Domain-average emissions burdens
* Demographic-specific burdens
* Relative disparity metrics

---

## Air Quality & Health

This directory processes WRF-CMAQ outputs and evaluates resulting changes in air quality, exposure, health impacts, and environmental justice outcomes.

### Objectives

* Quantify concentration changes resulting from inventory modifications.
* Evaluate exposure disparities.
* Estimate health impacts.
* Assess environmental justice implications.

### Workflow

#### Step 1: NetCDF to Shapefile Conversion

Converts WRF-CMAQ outputs into GIS-compatible shapefiles.

```text
NetCDF Outputs
      │
      ▼
DataProcessing_Step1_nc_to_shapefile.ipynb
      │
      ▼
Gridded Shapefiles
```

#### Step 2: Concentration Comparisons

Compare pollutant concentrations across scenarios.

Pollutants include:

* NO₂
* PM₂.₅
* PM₂.₅ EC
* O₃

#### Step 3: Census Tract Analysis

Overlay modeled concentrations with census tract boundaries.

#### Step 4: Exposure Assessment

Calculate population-weighted concentrations for:

* Total Population
* White
* Black
* Hispanic
* Asian
* Other

#### Step 5: Health Impact Assessment

Estimate changes in:

* Premature mortality
* Pollutant-attributable health burdens
* Demographic-specific impacts

### Key Outputs

#### Air Quality

* Gridded concentration maps
* Difference maps
* Census tract summaries

#### Exposure

* Population-weighted concentrations
* Exposure disparity metrics

#### Health

* Mortality estimates
* Health burden comparisons
* Equity analyses

---

# Modeling Framework

## Emissions Modeling

* EPA 2022v1 Emissions Modeling Platform
* MOVESv4.0
* SMOKE

## Air Quality Modeling

* WRF v4.5.1
* CMAQ v5.5

## Health Analysis

* NHGIS Demographic Data
* USALEEP Mortality Data
* BenMAP-derived concentration-response functions

---

# Study Domain

The analysis focuses on the Greater Chicago region:

* Cook County
* DuPage County
* Kane County
* Kendall County
* Lake County
* McHenry County
* Will County

Air quality simulations were conducted using a high-resolution inner modeling domain (~1.3 km grid spacing) nested within a larger regional WRF-CMAQ framework.

---

# Citation

If using these workflows, data products, or figures, please cite the associated manuscript(s) and repository.

Repository:

https://github.com/Vlang11/MHDV-Fleet-Renewal

---

# Contact

Victoria Lang, Ph.D. 
Northwestern University
Department of Earth, Environmental, and Planetary Sciences
