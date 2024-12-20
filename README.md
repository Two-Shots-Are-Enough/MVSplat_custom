<p align="center">
  <h1 align="center">MVSplat: Efficient 3D Gaussian Splatting <br> from Sparse Multi-View Images</h1>
  <p align="center">
    <a href="https://donydchen.github.io/">Yuedong Chen</a>
    &nbsp;·&nbsp;
    <a href="https://haofeixu.github.io/">Haofei Xu</a>
    &nbsp;·&nbsp;
    <a href="https://chuanxiaz.com/">Chuanxia Zheng</a>
    &nbsp;·&nbsp;
    <a href="https://bohanzhuang.github.io/">Bohan Zhuang</a> <br>
    <a href="https://people.inf.ethz.ch/marc.pollefeys/">Marc Pollefeys</a>
    &nbsp;·&nbsp;
    <a href="http://www.cvlibs.net/">Andreas Geiger</a>
    &nbsp;·&nbsp;
    <a href="https://personal.ntu.edu.sg/astjcham/">Tat-Jen Cham</a>
    &nbsp;·&nbsp;
    <a href="https://jianfei-cai.github.io/">Jianfei Cai</a>
  </p>
  <h3 align="center">ECCV 2024 Oral</h3>
  <h3 align="center"><a href="https://arxiv.org/abs/2403.14627">Paper</a> | <a href="https://donydchen.github.io/mvsplat/">Project Page</a> | <a href="https://drive.google.com/drive/folders/14_E_5R6ojOWnLSrSVLVEMHnTiKsfddjU">Pretrained Models</a> </h3>
</p>
<h4 align="center">customized by yoomimi

## Installation

To get started, clone this project, create a conda virtual environment using Python 3.10+, and install the requirements:

```bash
git clone https://github.com/Three-Shots-Are-Enough/MVSplat_custom.git
cd MVSplat_custom
conda create -n mvsplat python=3.10
conda activate mvsplat
pip install torch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 --index-url https://download.pytorch.org/whl/cu118
pip install -r requirements.txt
```

```bash
# download the backbone pretrained weight from unimath and save to 'checkpoints/'
wget 'https://s3.eu-central-1.amazonaws.com/avg-projects/unimatch/pretrained/gmdepth-scale1-resumeflowthings-scannet-5d9d7964.pth' -P checkpoints
```

## Inference script

```bash
python -m src.main +experiment=mipnerf \
checkpointing.load=checkpoints/re10k.ckpt \
mode=test \
dataset/view_sampler=evaluation \
dataset.view_sampler.index_path=assets/evaluation_index_mipnerf.json \
test.compute_scores=true \
output_dir=outputs/test/mipnerf
```

## Wandb Parameter Sweep Script

```bash
wandb login # You need your own wandb workspace API Key to login
wandb init
wandb sweep script/sweep.yaml

## After getting the sweep ID, you should change the ID in sweep_cloud.sh
bash script/sweep_cloud.sh
```

#### Caution

- You need to change the wandb config setting on scripts

```bash
# config/experiments/coustom.yaml
wandb:
  project: yaicon-3-5gs
  name: custom
  tags: [custom, 512x512]
  mode: online
  entity: <your-entity>
```

## Acknowledgements

The project is largely based on [pixelSplat](https://github.com/dcharatan/pixelsplat) and has incorporated numerous code snippets from [UniMatch](https://github.com/autonomousvision/unimatch). Many thanks to these two projects for their excellent contributions!
