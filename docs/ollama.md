# Ollama
# Installation
Ollama is an open source project make ease running a large language model easier. [Ollama project](https://ollama.com) supports many models, such as Llama 3, Phi3, Mistral and Gemma 2. If you use linux, user can download ollama this command
```bash
curl -fsSL https://ollama.com/install.sh | sh
```
After the download process is complete, we can verify the installation with this command
```bash
ollama -v
// ollama version is 0.1.48
```
Or, we can also use `systemctl` command family to administrate the ollama. We can run `systemctl status ollama.service`. This is the example output
```bash
● ollama.service - Ollama Service
     Loaded: loaded (/etc/systemd/system/ollama.service; disabled; preset: enabled)
     Active: active (running) since Sun 2024-06-30 14:21:37 WIB; 1min 47s ago
   Main PID: 17207 (ollama)
      Tasks: 14 (limit: 18848)
     Memory: 797.2M (peak: 809.3M)
        CPU: 18.284s
     CGroup: /system.slice/ollama.service
             └─17207 /usr/local/bin/ollama serve

Jun 30 14:21:37 T{{HostName}} systemd[1]: Started ollama.service - Ollama Service.
Jun 30 14:21:37 T{{HostName}} ollama[17207]: 2024/06/30 14:21:37 routes.go:1064: INFO server config env="map[CUDA_VISIBLE_DEVICES: GPU_DEVICE_ORDINAL: HIP_VISIBLE_DEVICES: HSA_OV>
Jun 30 14:21:37 T{{HostName}} ollama[17207]: time=2024-06-30T14:21:37.282+07:00 level=INFO source=images.go:730 msg="total blobs: 6"
Jun 30 14:21:37 T{{HostName}} ollama[17207]: time=2024-06-30T14:21:37.282+07:00 level=INFO source=images.go:737 msg="total unused blobs removed: 0"
Jun 30 14:21:37 T{{HostName}} ollama[17207]: time=2024-06-30T14:21:37.283+07:00 level=INFO source=routes.go:1111 msg="Listening on 127.0.0.1:11434 (version 0.1.48)"
Jun 30 14:21:37 T{{HostName}} ollama[17207]: time=2024-06-30T14:21:37.284+07:00 level=INFO source=payload.go:30 msg="extracting embedded files" dir=/tmp/ollama3308212990/runners
Jun 30 14:21:43 T{{HostName}} ollama[17207]: time=2024-06-30T14:21:43.918+07:00 level=INFO source=payload.go:44 msg="Dynamic LLM libraries [cpu cpu_avx cpu_avx2 cuda_v11 rocm_v60>
Jun 30 14:21:44 T{{HostName}} ollama[17207]: time=2024-06-30T14:21:44.946+07:00 level=INFO source=types.go:98 msg="inference compute" id=GPU-e1da0a62-ba9b-9b83-5c9b-f9928c39660f >
Jun 30 14:21:49 T{{HostName}} ollama[17207]: [GIN] 2024/06/30 - 14:21:49 | 200 |      66.589µs |       127.0.0.1 | GET      "/api/version"
```
## Usage
Ollama support various models, we can refer supported models from this [website](https://ollama.com/library). For this document, lets start with a small LLM model, moondream 2. We can pull the models with this command
```bash
ollama pull moondream
```
This command will pull model from ollama's registry. This process will takes several minutes, depending to your network speed. After the pulling process is complete. We can check the model with this command
```bash
ollama list
# NAME            	ID          	SIZE  	MODIFIED    
# moondream:latest	55fc3abd3867	1.7 GB	2 hours ago
```
For curious user, we can print general information about the Large Language Model (LLM), with this command:
```bash
ollama show moondream
#   Model                             
#   	arch            	phi2	              
#   	parameters      	1B  	              
#   	quantization    	Q4_0	              
#   	context length  	2048	              
#   	embedding length	2048	              
  	                                  
#   Projector                         
#   	arch                     	clip   	  
#   	parameters               	454.45M	  
#   	projector type           	mlp    	  
#   	embedding length         	1152   	  
#   	projection dimensionality	2048   	  
  	                                  
#   Parameters                        
#   	stop       	"<|endoftext|>"	        
#   	stop       	"Question:"    	        
#   	temperature	0              	        
  	                                  
#   License                           
#   	Apache License           	         
#   	Version 2.0, January 2004
```
Finally, we can use the LLM model with this command. This command will start an interactive terminal where we can input our prompt.
```bash
ollama run moondream
```
Let's use the LLM to answer a question. Let's start with a simple question. The question is a zero shot prompt.
```bash
>>> What is the capital city of Indonesia?
   Jakarta
>>> What is the capital city of Singapore?
 Singapore
>>> What is the capital city of Malaysia?
  Kuala Lumpur
```
## Ollama's API
Ollama provides a REST API to interact with it. Let's say we want to check what kind of model is loaded into host memory. We can call to this endpoint.
```bash
curl http://localhost:11434/api/ps
```
This command will returns the following response
```json
{
  "models": [
    {
      "name": "moondream:latest",
      "model": "moondream:latest",
      "size": 2803922432,
      "digest": "55fc3abd386771e5b5d1bbcc732f3c3f4df6e9f9f08f1131f9cc27ba2d1eec5b",
      "details": {
        "parent_model": "",
        "format": "gguf",
        "family": "phi2",
        "families": [
          "phi2",
          "clip"
        ],
        "parameter_size": "1B",
        "quantization_level": "Q4_0"
      },
      "expires_at": "2024-06-30T15:42:53.061550284+07:00",
      "size_vram": 1859286528
    }
  ]
}
```
For further information, we can refer to this [ollama's documentation](https://github.com/ollama/ollama/blob/main/docs/api.md).
## What I learnt
In this document, I learn how to use basic command of ollama application. I also learn on how to run and administrate ollama application using its command.
## What's Next
We can continue our exploration by building an application that wraps around ollama cli.
![Proposed Application Architecture](<Proposed Architecture Ollama Serving.drawio.png>)
