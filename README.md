## Title: An Efficient ML-based Detection Framework for DDoS Attacks in 5G Near Real-Time RIC
### Abstract:
As 5G networks evolve, detecting Distributed Denial of Service (DDoS) attacks remains crucial. This paper presents a supervised learning ML-based 5G Core DDoS detection framework, that can be implemented as an xApp within the Near-RT RIC. Utilising statistical features from UE and CELL-specific key performance metrics, our framework achieves high detection rates and low false positives. Testing confirms its effectiveness, with F1-scores of up to 98\%, and detection rates of over 91\%. These results demonstrate the potential use of ML techniques in Open RAN environments to defend 5G networks.

### Open RAN based architecture:
![plot](https://github.com/sotirischatzimiltis/DDoS_5G_network_KPM/blob/main/Figrures/arch_working_final_letter.png)

### Dataset
The raw dataset can be downloaded from here: [NCSRD-DS-5GDDoS](https://zenodo.org/records/13900057)

### Overview of DDoS attack types, occurrence times, and participating devices

| #  | Attack Type       | Date       | Time              | Devices (IP)                                     |
|----|--------------------|------------|-------------------|--------------------------------------------------|
| 1  | SYN Flood         | 18.08.2024 | 07:00 - 08:00    | 10.20.10.2<br>10.20.10.4                         |
| 2  | ICMP Flood        | 19.08.2024 | 07:00 - 09:41    | 10.20.10.2<br>10.20.10.4                         |
| 3  | UDP Fragmentation | 19.08.2024 | 17:00 - 18:00    | 10.20.10.2<br>10.20.10.4                         |
| 4  | DNS Flood         | 21.08.2024 | 12:00 - 13:00    | 10.20.10.2<br>10.20.10.4                         |
| 5  | GTP-U Flood       | 21.08.2024 | 17:00 - 18:00    | 10.20.10.2<br>10.20.10.4<br>10.20.10.6<br>10.20.10.8<br>10.20.10.10 |


### Data Pre-processing
The following scripts can be followed serially in order to replicate the final datasets used for the experiments. Otherwise, the final datasets are located in the dedicated [folder](https://github.com/sotirischatzimiltis/ML_framework_DDoS_5G/tree/main/Datasets).
1. This [script](https://github.com/sotirischatzimiltis/ML_framework_DDoS_5G/blob/main/Scripts/UE_Initial_Feature_Drop_01.ipynb) performs an initial UE feature reduction, removing primarily identification features or session features that do not directly quantify performance. 
2. This [script](https://github.com/sotirischatzimiltis/ML_framework_DDoS_5G/blob/main/Scripts/Per_UE_Dataset_Creation_02.ipynb) is responsible for creating a new folder containing a CSV file per UE in the dataset. This script also fills the NaN values. 
3. This [script](https://github.com/sotirischatzimiltis/ML_framework_DDoS_5G/blob/main/Scripts/Final_per_UE_datasets_03.ipynb) creates two folders containing the finalized UE datasets. One [folder](https://github.com/sotirischatzimiltis/ML_framework_DDoS_5G/tree/main/Datasets/UE_datasets) contains the regular record values and the other [folder](https://github.com/sotirischatzimiltis/ML_framework_DDoS_5G/tree/main/Datasets/UE_datasets_roc) the rate of change between two records. Also, this script identifies the periods where an UE reconnects to the core after inactivity and labels the records as normal or malicious (and a more specific type for multiclass classification) since only some UEs contribute to each attack. 
   
### ML training
1. GridSearch for traditional ml models [script](https://github.com/sotirischatzimiltis/DDoS_5G_network_KPM/blob/main/Scripts/gridsearch_cv.ipynb)
1. Download and execute [supervised ml training script](https://github.com/sotirischatzimiltis/DDoS_5G_network_KPM/blob/main/Scripts/supervised_learning_approach.py)
2. For LSTM training you can download the following script [lstm](https://github.com/sotirischatzimiltis/DDoS_5G_network_KPM/blob/main/Scripts/lstm.ipynb)
   > Note: [auxiliary.py](https://github.com/sotirischatzimiltis/DDoS_5G_network_KPM/blob/main/Scripts/auxiliary.py) script should be downloaded. Responsible to form the training and inference sequences
