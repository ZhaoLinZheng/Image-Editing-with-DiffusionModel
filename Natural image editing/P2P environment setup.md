## P2P environment setup

### 1 official version：
```
https://github.com/google/prompt-to-prompt
```
### 2 reading "readme.md" file carefully
### 3 python virtual environment
```python
conda create -n p2p python==3.8
conda activate p2p
```
### 4 torch environment
```python
pip install torch==1.11
pip install -r requirements.txt
conda install torchvision==0.12.0 torchaudio==0.11.0 cudatoolkit=11.3 -c pytorch
```
Refer the pytorch official website：https://pytorch.org/get-started/previous-versions/
### 5 pretrained model downloading (taking LDM as an example)
To download the pretrained models efficiently, follow these steps:
First download the diffusers.
```python
pip install diffusers
```
Then, install huggingface_hub to download the SD and LDM pretrained model
```python
pip install -U huggingface_hub
```
Since the large size of the pre-trained model, it is recommended to  run the following instructions  to use "tmux" to download the model in case of the remote connection lost.
```shell
tmux new -s p2p
tmux attach -t p2p
huggingface-cli download --resume-download CompVis/ldm-text2im-large-256 --local--dir ldm-text2im-large-256
```
### 6 run the jupyter LDM
Before running the Jupyter notebook, ensure to update the "model_id" to your local path instead of the Hugging Face path.
Just like 
```
 changing "CompVis/ldm-text2im-large-256" to "/home/zzl/ldm-text2im-large-256"
```
### 7 Supplement
For detailed instructions on running and operating Jupyter locally on a remote server, follow the steps below. 
First, set up jupyter  in our virtual environment with "conda install ipykernel".
Then before  running Jupyter,  add the specific virtual environment you setup before to the Jupyter kernel.
```shell
python -m ipykernel install --user --name [ your virtual python environment] --display-name [name which is up to your own]
```
For example, python -m ipykernel install --user --name p2p --display-name p2p
Finally,  run Jupyter notebook  by 
```shell
jupyter notebook [your/path/to/your/notebook/file] --no-browser --ip=0.0.0.0 --port=8888
```

