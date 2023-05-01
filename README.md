# Raw data from the fluorophore dataset

## Notes

### TCSPC

The TCSPC setup is a bespoke implementation utilising:

* Fianium SC-400-pp white laser for excitation, (with wavelength selection filters)
  * The trigger signal came from a PicoQuant TDA 200 trigger diode, which was triggered by a cover slip redirecting10-12% of the photon flux to the diode

* ThorLabs 375nm laser diode head driven by a PicoQuant PDL 800-D for UV excitation
  * The trigger signal was taken directly from the PDL 800-D sync output

* PicoHarp 300 for correlating the laser trigger and micro-channel plate detection signals
* ThorLabs PF10-03-F01 mirrors (250-450 nm) for the UV path
* ThorLabs BB1-EO2 mirrors (400-750 nm) for the Visible path

Stil investigating

* The Micro-channel plate PMT

The time resolved data is stored in a mix of .txt and .phd files. The .phd importer wasn't written until just after data acquisition started, so a few histograms were still stored via the "copy-paste from the PicoHarp software into notepad" method.

The newly written .phd file importer is available at [picoharp-phd](https://github.com/adreasnow/picoharp-phd).

### UV-Vis

This data was all recorded on an Agilent Cary 60 UV-Vis spectrophotometer. Validation of the instrument was performed by a registered Agilent technician and was within operating standards

### Fluorescence and Excitation

This data was all collected on an Agilent Cary Eclipse fluorescence spectrometer and has been corrected for using the correction curves provided in the corrections folder. Validation of the instrument was performed by a registered Agilent technician and was within operating standards

#### Corrections

The corrections provided are `exCorr` for the excitation lamp (220- 600nm), `emCorr` for the PMT sensitivity (220-800nm), and `cuvette_trans` which accounts for the small difference in transmission for shorter wavelengths (200-800nm). They're applied as such...

For emission spectra:
```python
yCorrected = []
for x, y in zip(x, y):
  yCorrected += [y * emCorr[*int*(x)] * exCorr[enLambda] * cuvette_trans[*int*(x)] * cuvette_trans[enLambda]]
```

For excitation spectra:

```python
yCorrected = []
for x, y in zip(x, y):
    yCorrected += [y * exCorr[int(x)] * emCorr[enLambda] * cuvette_trans[int(x)] * cuvette_trans[enLambda]]
```

Solvent baseline spectra were also been collected for each emission and excitation spectrum in order to account for any solvent fluorescence, Raman scatter and second order Rayleigh scatter.

## Directory structure

```
.
├── README.md
├── corrections                           <- Correction factors
|   ├── emCorr.csv                        <- PMT correction factors
|   ├── exCorr.csv                        <- Excitation lamp correction factors
|   └── cuvette_pT.csv                    <- Cuvette transparency
├── abs                                   <- Absorbance data
|   └── <fluorophore>
|       └── <fluorophore>_<solvent>.csv
├── fluor                                 <- Fluorescence data
|   └── <fluorophore>
|       ├── <fluorophore>_<solvent>.csv
|       └── <fluorophore>_<solvent>_solv.csv
├── ex                                    <- Excitation data
|   └── <fluorophore>
|       ├── <fluorophore>_<solvent>.csv
|       └── <fluorophore>_<solvent>_solv.csv
└── tr                                    <- Time resolved data
    └── <fluorophore>
        ├── <fluorophore>_<solvent>_irf.phd
        └── <fluorophore>_<solvent>.phd
        or
        ├── <fluorophore>_<solvent>_<bin size>_irf.txt
        └── <fluorophore>_<solvent>_<bin size>.txt
```


## Fluorophores
Dataset: 
* az: Azulene
* r800: Rhodamine 800
* aaq: 1-Aminoanthraquinone
* c153: Coumarin 153 
* nr: Nile Red
* bod493: BODIPY 493/503
* nda: Naphthalamide
* dapi: DAPI
* daa: Dansyl amide
* bsc: Boron Subphthalocyanine Chloride

## Solvents



Dataset:
* nhex: *n*-hexane
* tol: Toluene
* ans: Anisole
* ether: Ether
* chcl3: Chloroform
* thf: THF
* dcm: DCM
* c8oh: Octanol
* etoh: Ethanol
* acn: ACN
* dmf: DMF
* dmso: DMSO
