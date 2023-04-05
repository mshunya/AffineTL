# Overview
This repository provides Python code for the following four experiments conducted in Minami et al. (2022).

- Kinematics of the robot arms (Section 5.1)
- Lattice thermal conductivity of inorganic crystals (Section 5.2)
- Heat capacity of organic polymers (Section 5.3)
- Eigenvalue decay of the Hadamard product of two Gram matrices (Appendix C)

Some of the datasets are provided, but the rest must be downloaded from the distributor due to redistribution restrictions. 
The downloading instructions are given in the detailed description of each experiment.

# Repository Descriptions
Each repository consists of three folders: '/10_Data' (dataset folder), '/20_PGM' (python code folder) and '30_Output' (output folder).

## 11_SARCOS
We use SARCOS dataset (Williams & Rasmussen, 2006). 
The task is to predict the feed-forward torque required to follow the desired trajectory in the seven joints of the SARCOS anthropomorphic robot arm. 
21 features representing the joints’ position, velocity, and acceleration are used as input, and six torque other than the one used as the target domain are used as source features.

### Dataset
You should download two dataset; 'sarcos_inv.mat' and 'satcos_inv_test.mat' from the [web page](http://gaussianprocess.org/gpml/data/) for 'Gaussian Processes for Machine Learning.'
These dataset include 44,484 training samples and 4,449 test samples.

### Programs
Place the two datasets in [/10_Data/](https://github.com/mshunya/AffineTL/tree/main/11_SARCOS/10_Data) folder and run [300_TransferLearning.ipynb](https://github.com/mshunya/AffineTL/blob/main/11_SARCOS/20_PGM/300_TransferLearning.ipynb).
- [300_TransferLearning.ipynb](https://github.com/mshunya/AffineTL/blob/main/11_SARCOS/20_PGM/300_TransferLearning.ipynb) : Main code
- [400_MakeResult.ipynb](https://github.com/mshunya/AffineTL/blob/main/11_SARCOS/20_PGM/400_MakeResult.ipynb) : For figure in the paper

### References
- Christopher KI Williams and Carl Edward Rasmussen. Gaussian processes for machine learning, volume 2. MIT press Cambridge, MA, 2006.

## 12_LTC
The task is to predict the lattice thermal conductivity (LTC: the amount of vibrational energy propagated by phonons in a crystal) of inorganic crystalline materials.
We perform TL with the source task of predicting an alternative, computationally tractable physical property called scattering phase space (SPS), which is known to be physically related to LTC.

### Dataset
Two datasets obtained in Ju et al. (2021) are used, consisting of the lattice thermal conductivity (LTC) and scattering phase space (SPS), which are computed for 45 and 320 inorganic crystals, respectively. 
To obtain the input descriptors, [XenonPy](https://github.com/yoshida-lab/XenonPy) is used to generate compositional descriptors of a material, which describe 290 features of the elemental composition of a given material.
These dataset are placed in [/10_Data/](https://github.com/mshunya/AffineTL/tree/main/12_LTC/10_Data) (SPSTC_290.pkl).

### Programs
Run [100_MakeSourceModel.ipynb](https://github.com/mshunya/AffineTL/blob/main/12_LTC/20_PGM/100_MakeSourceModel.ipynb) to make the source models.
We use the top 10 source models that showed the highest generalization performance in the source domain (No.66, 83, 39, 36, 70, 95, 56, 72, 69, 42).
- [300_TransferLearning.ipynb](https://github.com/mshunya/AffineTL/blob/main/12_LTC/20_PGM/200_TransferLearning.ipynb) : Main code
- [400_MakeResult.ipynb](https://github.com/mshunya/AffineTL/blob/main/12_LTC/20_PGM/300_MakeResult.ipynb) : For figure in the paper

### Models
The source model we trained is placed in [/30_Output/100_MakeSourceModel/](https://github.com/mshunya/AffineTL/tree/main/12_LTC/30_Output/100_MakeSourceModel) and [/30_Output/40_pkl/100_MakeSourceModel/](https://github.com/mshunya/AffineTL/tree/main/12_LTC/30_Output/40_pkl).

### References
- Sheng Ju, Ryo Yoshida, Chang Liu, Kenta Hongo, Terumasa Tadano, and Junichiro Shiomi. Exploring diamond-like lattice thermal conductivity crystals via feature-based transfer learning. Physical Review Materials, 5(5):053801, 2021.
- Chang Liu, Erina Fujita, Yukari Katsura, Yuki Inada, Asuka Ishikawa, Ryuji Tamura, Kaoru Kimura, and Ryo Yoshida. Machine learning to predict quasicrystals from chemical compositions. Advanced Materials, 33(36):2102507, 2021.

## 13_Cp
The objective is to predict the specific heat capacity at constant pressure CP of any given organic polymer with its chemical structure in the repeating unit. 
We conduct TL to bridge the gap between experimental values and physical properties calculated from molecular dynamics (MD) simulations.

### Dataset
You should collect the dataset of experimental values of heat capacities from [PoLyInfo](https://polymer.nims.go.jp/en/) (Otsuka et al., 2011).
The PoLyInfo sample identifiers for the selected polymers are listed in [/10_Data/PI_Cp_masked.csv](https://github.com/mshunya/AffineTL/blob/main/13_Cp/10_Data/PI_Cp_masked.csv).
[MD_PI1070.csv](https://github.com/mshunya/AffineTL/blob/main/13_Cp/10_Data/MD_PI1070.csv) is the dataset of MD simulated values of these polymers and [PI_lib_FFKM.csv](https://github.com/mshunya/AffineTL/blob/main/13_Cp/10_Data/PI_lib_FFKM.csv) is 190-dimensional force field descriptors calculated by [Radonpy](https://github.com/RadonPy/RadonPy).

### Programs
Before performing transfer learning, you should collect the experimental values for 70 polymers and run [100_CheckData.ipynb](https://github.com/mshunya/AffineTL/blob/main/13_Cp/20_PGM/100_CheckData.ipynb), and then '100_Data.pkl' will be created in [/30_Output/40_pkl/100_CheckData/](https://github.com/mshunya/AffineTL/tree/main/13_Cp/30_Output/40_pkl/100_CheckData).
- [300_TransferLearning.ipynb](https://github.com/mshunya/AffineTL/blob/main/13_Cp/20_PGM/300_TransferLearning.ipynb) : Main code
- [400_MakeResult.ipynb](https://github.com/mshunya/AffineTL/blob/main/13_Cp/20_PGM/300_TransferLearning.ipynb) : For figure in the paper

### References
- Shingo Otsuka, Isao Kuwajima, Junko Hosoya, Yibin Xu, and Masayoshi Yamazaki. Polyinfo: Polymer database for polymeric materials design. In 2011 International Conference on Emerging Intelligent Data and Web Technologies, pp. 22–29. IEEE, 2011.
- Yoshihiro Hayashi, Junichiro Shiomi, Junko Morikawa, and Ryo Yoshida. Radonpy: Automated physical property calculation using all-atom classical molecular dynamics simulations for polymer informatics. ArXiv, abs/2203.14090, 2022.

## 21_CheckEigenvalues
The objective is to confirm experimentally how the decay rate in Corollary 4 in the paper is related to the size of the overlap between the spaces spanned by the original inputs and the source features.

### Programs
- [100_CheckEigenvalues.ipynb](https://github.com/mshunya/AffineTL/blob/main/21_CheckEigenvalues/20_PGM/100_CheckEigenvalues.ipynb) : Main code
- [400_MakeResult.ipynb](https://github.com/mshunya/AffineTL/blob/main/21_CheckEigenvalues/20_PGM/400_MakeResult.ipynb) : For figure in the paper
