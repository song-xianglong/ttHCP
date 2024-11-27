# $t\bar{t}H+tH$ CP analysis on ATLAS

## Project Description
This project aims to improve the sensitivity of the ttH/tH charge-parity (CP) analysis, which measures the CP structure of the Higgs-top interaction. The focus is on approaches for the combinatorial jet assignment to top quark candidates and training a neural network (NN) to simultaneously discriminate between signal/background and CP even/odd signal production.

## Repository Contents
- `DataLoading-mxaod-ttH.ipynb`: A Jupyter notebook for exploring the MxAOD Monte Carlo (MC) datasets. It focuses on understanding the properties of final-state objects in ttH events (assuming the Standard Model).
- `new_chi2.ipynb`: Implements a chi-squared algorithm to reconstruct top quarks from jets in ttH events.
- `DNN.ipynb`: Builds upon the chi-squared algorithm by developing a deep neural network for further classification tasks.
- `reco_jets.h5`: Input file containing reconstructed jet data, used in `new_chi2.ipynb` and `DNN.ipynb`.
- `true_jets.h5`: Input file containing truth-level jet data, used in `new_chi2.ipynb` and `DNN.ipynb`.

## Project Details
The initial focus is to study the resolution of variables that provide CP-discrimination, such as the kinematics of the $tH$, $\bar{t}H$, and $t\bar{t}H$ systems. The studies use MxAOD MC samples containing both reconstruction-level and truth-level quantities. 

### Key Datasets
The datasets for this analysis are located in the following directory: `/eos/atlas/atlascerngroupdisk/phys-higgs/HSG1/MxAOD/h028/mc16*/Nominal/mc16*.PowhegPy8_ttH125_*_h028.root`.

### Useful Dataset Branches
```
# Photon quantities
*Br    4 :HGamPhotonsAuxDyn.Rconv : vector<float>                            * 
*Br   26 :HGamPhotonsAuxDyn.eta : vector<float>                              *
*Br   33 :HGamPhotonsAuxDyn.isIsoFixedCutLoose : vector<char>                *
*Br   35 :HGamPhotonsAuxDyn.isIsoFixedCutTight : vector<char>                *
*Br   37 :HGamPhotonsAuxDyn.isTight : vector<char>                           *
*Br   39 :HGamPhotonsAuxDyn.m : vector<float>                                *
*Br   49 :HGamPhotonsAuxDyn.parentPdgId : vector<int>                        *
*Br   51 :HGamPhotonsAuxDyn.phi : vector<float>                              *
*Br   52 :HGamPhotonsAuxDyn.pt : vector<float>                               *

# Jet quantities
*Br  110 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.DL1r_bin : vector<int>      *
*Br  114 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.DetectorEta : vector<float> *
*Br  123 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.HadronConeExclTruthLabelID : *
*Br  126 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.OneMu_eta : vector<float>   *
*Br  127 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.OneMu_m : vector<float>     *
*Br  128 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.OneMu_phi : vector<float>   *
*Br  129 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.OneMu_pt : vector<float>    *
*Br  131 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.PtRecoSF : vector<float>    *
*Br  147 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.eta : vector<float>         *
*Br  150 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.m : vector<float>           *
*Br  153 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.phi : vector<float>         *
*Br  154 :HGamAntiKt4PFlowCustomVtxHggJetsAuxDyn.pt : vector<float>          *

# Truth jet quantities 
*Br  635 :HGamAntiKt4TruthWZJetsAuxDyn.HadronConeExclTruthLabelID :          *
*Br  637 :HGamAntiKt4TruthWZJetsAuxDyn.eta : vector<float>                   *
*Br  638 :HGamAntiKt4TruthWZJetsAuxDyn.m : vector<float>                     *
*Br  639 :HGamAntiKt4TruthWZJetsAuxDyn.phi : vector<float>                   *
*Br  640 :HGamAntiKt4TruthWZJetsAuxDyn.pt : vector<float>   

# Truth Higgs boson quantities
*Br  650 :HGamTruthHiggsBosonsAuxDyn.e : vector<float>                       *
*Br  651 :HGamTruthHiggsBosonsAuxDyn.m : vector<float>                       *
*Br  652 :HGamTruthHiggsBosonsAuxDyn.pt : vector<float>                      *
*Br  653 :HGamTruthHiggsBosonsAuxDyn.px : vector<float>                      *
*Br  654 :HGamTruthHiggsBosonsAuxDyn.py : vector<float>                      *
*Br  655 :HGamTruthHiggsBosonsAuxDyn.pz : vector<float>                      *
```

## Usage Instructions
Below are instructions for setup and usage:

### Framework Setup
1. Clone the ATLAS HH Legacy Analysis framework:
    ```bash
    git clone --recursive ssh://git@gitlab.cern.ch:7999/atlas-physics/HDBS/DiHiggs/yybb/hh_legacy_analysis/HH_Legacy_analysis_code.git
    ```
2. Modify the `setup.sh` file to adapt to your environment:
    ```bash
    [Line 94] x86_64-centos7-gcc11-opt -> x86_64-el9-gcc13-opt
    ```
3. Compile the framework:
    ```bash
    source compile.sh
    ```
4. Copy the `DataLoading-mxaod-ttH.ipynb` notebook to your workspace:
    ```bash
    cp ~DataLoading-mxaod-ttH.ipynb /eos/user/<yourpath>
    ```

### Running the Notebooks
1. Start a SWAN session with the following configuration:
    - OS: AlmaLinux
    - Environment Script: `/afs/cern.ch/user/x/xianglon/public/setup.sh`
    - Resources: 4 cores, maximum memory.
2. Open the relevant Jupyter notebooks in your SWAN session:
    - Use `DataLoading-mxaod-ttH.ipynb` for data exploration.
    - Use `new_chi2.ipynb` to reconstruct top quarks using the chi-squared algorithm.
    - Use `DNN.ipynb` to train a neural network on the reconstructed jets.

## Next Steps
We are working on training a neural network, potentially leveraging transformer architectures, to classify events as signal/background and CP even/odd simultaneously. Once complete, the updated notebooks and results will be uploaded to this repository.