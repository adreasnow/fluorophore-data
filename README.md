# Raw data from the fluorophore dataset

## Directory structure

```
.
├── README.md
├── abs                                   <- Absorbance Data
|   └── <fluorophore>
|       └── <fluorophore>_<solvent>.csv
├── fluor                                 <- Fluorescence Data
|   └── <fluorophore>
|       └── <fluorophore>_<solvent>.csv
└── tr                                    <- Time resolved Data
    └── <fluorophore>
        ├── IRF.txt
        └── <fluorophore>_<solvent>_<rep rate>_<bin size>_<monochromater>.txt
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
* asp: α-Sexithiophene

Reference:
* r6g: Rhodamine 6G
* rb: Rhodamine B
* cv:Cresyl Violet

## Solvents
Dataset:
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

Reference:
* meoh: Methanol
* h2o: water