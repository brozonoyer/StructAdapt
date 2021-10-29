# Structural Adapters in Pretrained Language Models for AMR-to-Text Generation

This repository contains the code for the [EMNLP 2021 paper](https://arxiv.org/pdf/2103.09120.pdf) "Structural Adapters in Pretrained Language Models for AMR-to-Text Generation". Please star the repository and cite the paper if you find it useful. 

**StructAdapt** is an adapter-based method that encodes graph structures into pretrained language models. Contrary to prior work, **StructAdapt** effectively models interactions among the nodes based on the graph connectivity, only training graph
structure-aware adapter parameters.

<p align="center">
<img src="img/figure1-adapter-paper.png" width="500">
</p>

Figure 1(a) shows a standard adapter, whereas Figure 1(b) illustrates **StructAdapt**.
<p align="center">
<img src="img/adapter.png" width="500">
</p>

## Datasets

In our experiments, we use the following datasets: [AMR2017](https://catalog.ldc.upenn.edu/LDC2017T10), [AMR2020](https://catalog.ldc.upenn.edu/LDC2020T02).

## Environment

The easiest way to proceed is to create a conda environment:
```
conda create -n structadapt python=3.6
```

Further, install PyTorch and PyTorch Geometric:

```
conda install -c pytorch pytorch=1.6.0
pip install torch-scatter==2.0.5 -f https://data.pyg.org/whl/torch-1.6.0+${CUDA}.html
pip install torch-sparse==0.6.8 -f https://data.pyg.org/whl/torch-1.6.0+${CUDA}.html
pip install torch-geometric==1.6.1
```
where `{CUDA}` is your CUDA version. Please, refer to [PyTorch Geometric installation page](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html) for more details.

Finally, install the packages required:

```
pip install -r requirements.txt
```

## Preprocess

Convert the dataset into the format required for the model:

```
./preprocess/preprocess_AMR.sh <dataset_folder>
```


## Finetuning

For training **StructAdapt** using the AMR dataset, execute:
```
./train.sh <model> <data_dir> <gpu_id> 
```
 
Options for `<model>` are `t5-small`, `t5-base`, `t5-large`. 

Example:
```
./train.sh t5-large data/processed_amr 0
```


## Decoding

For decoding, run:
```
./test.sh <model> <checkpoint_folder> <data_dir> <gpu_id>
```

Example:
```
./test.sh t5-base ckpt-folder data/processed_amr 0
```


## Traiened Model

A checkpoint of **StrutAdapt** (T5-large) trained on LDC2020T02 dataset can be found [here](https://public.ukp.informatik.tu-darmstadt.de/ribeiro/structadapt/ckpt_amr2020.tar.gz). This model achieves a _BLEU score_ of _48.21_. The outputs can be downloaded [here](https://raw.githubusercontent.com/UKPLab/StructAdapt/master/outputs/test_generations.txt).

## More
For more details regading hyperparameters, please refer to [HuggingFace](https://huggingface.co/).


**Contact person:** Leonardo Ribeiro, ribeiro@aiphes.tu-darmstadt.de

## Citation

```
@inproceedings{ribeiro-etal-2021-structadapt,
    title = "Structural Adapters in Pretrained Language Models for AMR-to-Text Generation",
    author = "Ribeiro, Leonardo F. R.  and
      Zhang, Yue  and
      Gurevych, Iryna",
    booktitle = "Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing (EMNLP)",
    month = nov,
    year = "2021",
    address = "Punta Cana, Dominican Republic",
    publisher = "Association for Computational Linguistics",
}
```