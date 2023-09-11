# DriveLLM, The offical code repo for DriveLLM

This repository contains the official implementation of the DriveLLM system, which leverages large language model (LLM) capabilities to enhance autonomous driving decision-making processes. 
The LLM-service backend is implemented using [Fast-API](https://fastapi.tiangolo.com/) and [langchain](https://python.langchain.com/docs/get_started/introduction). 
The LLM-Autonomous driving bridge is implemented for ROS 1 designed for a modified version of [Autoware stack](https://github.com/tier4/AutowareArchitectureProposal.proj/tree/ros1)

## Other resources:
### Testing rosbags recorded on all-weather autonomous shuttle bus (WATonoBus) project

[NAS link](http://tunnel.loopx.ai:5000/)

### instruction-following Finetune Dataset for General Driving Application
This contained a [20K dataset]((https://huggingface.co/datasets/dongdongcui/alpaca-dataset-max)) generated using self-instruct and is designed for general driving applications.
Relevant dataset code on dataset generation, cleaning and formatting is [here](https://github.com/loopx-ai/Drive-LlamaV2/tree/self-instruct-dataset) 


### Finetuned LLaMA model weight

-   [13B LLaMA weight](https://huggingface.co/dongdongcui/DriveGPT-13B)
-   [7B LLaMA weight](https://huggingface.co/dongdongcui/DriveGPT)

## How to use/test this service
Note: change http://localhost:9000/query to http://localhost:8300/query If you are running the service in docker.

### Test the query endpoint:
Sending requests to the /query endpoint. 
Here is an example of using curl for service debuging (running locally):
```
curl -N -X POST 'http://localhost:9000/query' \
-H 'Content-Type: application/json' \
-d '{
    "messages": [
        {
            "role": "user",
            "perception":"perception", 
            "system_health":"system_health", 
            "weather":"weather", 
            "location":"location", 
            "vehicle_state":"vehicle_state",
            "control_command":"control_command",
            "command":"passenger_command"
        }
    ]
}'
```


## 🚀 Running the app in docker (recommended for deployment)
```
docker-compose up
```
Build the docker image and run the container.
```
docker-compose build
docker-compose up
```
If you need to completely shut down your environment or clean up your resources: 
```
docker-compose down 
```
stops running containers and remove them, along with their associated networks, volumes, and images.

Note: For docker, the service will now be accessible at [http://localhost:8300](http://localhost:8300).

## ✅ Running locally (recommended for developer)
1. Clone this repository
2. Install dependencies:
```
pip install -r requirements.txt
```
3. Create an .env file and add the following environment variables:
```
LOGGING_LEVEL=10 # 10-DEBUG, 20-INFO, 30-WARN, 40-ERROR
```
5. Run the application using Uvicorn:
```
uvicorn main:app --host 0.0.0.0 --port 9000
```
6. The service will now be accessible at [http://localhost:9000](http://localhost:9000).


