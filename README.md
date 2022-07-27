
![viewer](https://github.com/quocnh/FL_Encoder/blob/main/Screen%20Shot%202022-07-26%20at%2010.06.46%20PM.png)
## Prerequisite
Install command line tool `unar`: 

for MacOS
```
brew install unar
```
for Linux
```
sudo apt-get install unar
```
## Setup
Reproducing this source https://github.com/FedML-AI/FedML/tree/master/app/fediot/anomaly_detection_for_cybersecurity

Must be conda env python >= 3.8

```
conda create -n fedml python=3.8
conda activate fedml
```

Install FedML version 0.7.98 (instal from source) -> does not work

```
git clone https://github.com/FedML-AI/FedML.git && \
cd ./FedML/python && \
python setup.py install
```
-> should install using 
```
pip install fedml==0.7.98
```
Git clone https://github.com/FedML-AI/FedML.git
Link to https://github.com/FedML-AI/FedML/tree/master/app/fediot/anomaly_detection_for_cybersecurity
Run

## Real-deployment Training Script

At the client side, the client ID (a.k.a rank) starts from 1.
Please also modify config/fedml_config.yaml, changing the `client_num_in_total`, `client_num_per_round`, `worker_num` 
as the number of clients you plan to run.

For this application, the number of clients is up to 9 since there are 9 types of IoT devices in N-BaIoT dataset.

At the server side, run the following script:
```
bash run_server.sh
```

For client 1, run the following script:
```
bash run_client.sh 1
```
For client 2, run the following script:
```
bash run_client.sh 2
```
Note: please run the server first.

## Centralized Simulation Training Script

We also support centralized simulation for FedIoT, which means one PC could simulate both server and clients as you need.
All training related parameters are inside config_simulation/fedml_config.yaml, please modify it per your need.
The worker_num under the device_args represents number of processes in MPI, as the number of parallel clients.

For this application, the number of clients is up to 9 since there are 9 types of IoT devices in N-BaIoT dataset.
Run the following script to begin the training:
```
sh run_simulation.sh 9
```
9 in the above script represents the number of parallel clients, which should be identical to the worker_num inside config_simulation/fedml_config.yaml.


