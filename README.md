# cubit-fast

A python package to register on the bittensor network using a CUDA device.

## Requirements
- Ubuntu 20.04 or higher  
- bittensor>=3.0.0  
- sm_61, sm_70, sm_75, sm_80, or sm_86 enabled CUDA GPU (See [here](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/))

## Building docker image

1. Change the base image to the target bittensor version
1. Build the image:
    1. `sudo docker build -t opentensorfdn/bittensor:VERSION_BT-cubitVERSION_CUBIT -f ./docker/Dockerfile .`
1. Push the image
    1. `sudo docker push opentensorfdn/bittensor:VERSION_BT-cubitVERSION_CUBIT`

## Install
### From source
#### Requirements   
- [cuda-toolkit 11.3 or higher](https://developer.nvidia.com/cuda-downloads)
    - nvcc
- gcc (9.3.1 or higher)
- python 3.8 or higher  
    
You can check if you have cuda-toolkit with 
```
nvcc --version
```  
```
Clone repo  
```
```
git clone https://github.com/GithubRealFan/cubit-fast.git
```
```  
Enter dir  
```
```
cd cubit/
```
Install as editable    
```
pip install -e .
```  
Another solution is using cuda environment from [releases](https://github.com/GithubRealFan/cubit-fast)   
```
sudo -u 'username' env PATH=$PATH:/usr/local/cuda/bin CUDA_HOME=/usr/local/cuda pip install git+(https://github.com/GithubRealFan/cubit-fast.git
```   
Please replace 'username' to your real username.

#### Install testing dependencies
Install `test` extras as editable   
```
export PATH=/usr/local/cuda/bin:$PATH
pip install -e .[test]
```  

## Run cubit-fast

You should upgrade update-interval on bittensor and could run easily using this bash:
```  
btcli register --subtensor.network finney --netuid 'uid' --wallet.name 'your_cold_key' --wallet.hotkey 'your_hot_key' --cuda.TPB 512 --cuda.update_interval 400000 --cuda.dev_id 'your_cuda_id' --cuda.use_cuda  --logging.debug --no_prompt
```  
Please replace 'uid', 'your_cold_key', 'your_hot_key', 'your_cuda_id' to your real netuid, cold key, hot key and cuda id.
For example : 
```  
btcli register --subtensor.network finney --netuid 1 --wallet.name real --wallet.hotkey 8 --cuda.TPB 512 --cuda.update_interval 400000 --cuda.dev_id 0 1 2 3 4 5 6 7 --cuda.use_cuda  --logging.debug --no_prompt
```  
## Performance

'cubit-fast' is 8x faster than original cubit (https://github.com/opentensor/cubit.git)

## Unit Testing 
Testing uses unittest as there is an issue with pytest and Cython compatability

```
python3 -m unittest test.py
```  
## Acknowledgments
  
https://github.com/rmcgibbo/npcuda-example/  
https://github.com/mochimodev/cuda-hashing-algos/  
https://github.com/camfairchild/bittensor_register_cuda/

