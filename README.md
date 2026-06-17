# Dynamic Denoising Method Based on Semantic Prompts for Mixed Noise Suppression in Seismic Data

<img width="3347" height="519" alt="1" src="https://github.com/user-attachments/assets/5fb65d5b-d39d-447d-951d-c7fa749f6e50" />
Fig 1. SP-DDNet denoising workflow.

## 1 Network structure
SP-DDNet consists of the CSE, DSFE, AFPL and an output layer. The specific parameters of each module are shown in Table 1.
Tabel 1. The structure settings of each module of SP-DDNet
<img width="3407" height="2228" alt="T1" src="https://github.com/user-attachments/assets/1febaa4e-5b2b-40f2-beb5-545803d7fac0" />

## 2 Training dataset
The training sets consist of semantic recognition datasets and denoising datasets, and the specific process of dataset production is shown in Fig. 2.
<img width="6797" height="2495" alt="T2" src="https://github.com/user-attachments/assets/592b3914-61c3-4372-b490-9f6809a1f84a" />
Fig 2. The composition of the training dataset.

Notably, the datasets were split into training and validation sets at 8:2. Field noise was multiplied by a random value within (0, 3] to diversify noise levels, and test noise was from independent sources.

## 2 Training details
All deep learning network models are implemented with PyTorch and trained with three Nvidia GeForce GTX 1080Ti GPUs.
The loss function consists of mean square error loss $L_{mse}$, structure-detail loss $L_{sd}$ and semantic loss $L_{se}$，

Loss= $L_{mse}$ + $\alpha_{1}$ $L_{sd}$ + $\alpha_{2}$ $L_{se}$

where, $\alpha_{1}$=0.3, $\alpha_{2}$=0.002.

Semantic recognition training: Adam optimizer, initial learning rate = 0.001, 500 epochs, the learning rate is halved every 100 epochs, batch size=32.

Seismic denoising training: Adam optimizer, initial learning rate = 0.0001, 200 epochs, knowledge accumulation–deepening strategy, batch size=16.  
SP-DDNet is first trained for 120 epochs on four single-type noise datasets, with 30 epochs allocated to each noise type. It is then trained for another 80 epochs on the mixed noise dataset to refine prior learned knowledge.












