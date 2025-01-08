
## Pinal: Toward De Novo Protein Design from Natural Language


The repository is an official implementation of Pinal: [Toward De Novo Protein Design from Natural Language](https://www.biorxiv.org/content/10.1101/2024.08.01.606258)

Quickly try our online server [here](http://www.denovo-pinal.com/)

If you have any question about the paper or the code, feel free to raise an issue!


### Environment setup

Create and activate a new conda environment with Python 3.8.
```shell
conda create -n pinal python=3.8 --yes
conda activate pinal
pip install -r requirements.txt
```


### Download model weights

We provide a scripts to download the pre-trained model weights, as is shown below. Please download all files and put them in the `weight` directory, e.g. `weights/T2struc-15B/...`


```shell
huggingface-cli download westlake-repl/Pinal \
                         --repo-type model \
                         --local-dir weights/
```


### Inference with Pinal

Design protein from natural language instruction with only 3 lines of code!

```python
from utils.design_utils import load_pinal, PinalDesign
load_pinal()
res = PinalDesign(desc="Actin.", num=10)
# res is a list of designed proteins, sorted by the probability per token. 
```

The above code will generate 10 de novo designed proteins based on the input description "Actin.", inferenced by 1.2B T2struc and SaProt-T. If you want inference with T2struc-15B, you can set the environment variable `T2struc_NAME` before calling `load_pinal()`, as is shown below.
> Warning: Inferencing with T2struc-15B requires at least 40GB GPU memory.

```python
import os
os.environ["T2struc_NAME"] = "T2struc-15B"
```

### Computational evaluation of the de novo designed proteins

For texutal alignment, we recommend use [ProTrek](https://github.com/westlake-repl/ProTrek) to calculate the sequence-text similarity score.

For foldability, we recommend use pLDDT and PAE, outputed by [Alphafold series](https://golgi.sandbox.google.com/) or [ESMFold](https://github.com/facebookresearch/esm).


### Other resources

- [ProTrek](https://www.biorxiv.org/content/10.1101/2024.05.30.596740v2) and its [online server](http://search-protrek.com/)
- [Evola](https://www.biorxiv.org/content/10.1101/2025.01.05.630192v1) and its [online server](http://www.chat-protein.com/)

