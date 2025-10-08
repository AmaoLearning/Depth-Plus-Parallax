## Depth Anything V2 + Parallax Effect

This software project is based on the research paper:
**[Depth Anything V2](https://arxiv.org/abs/2406.09414)**,
*Lihe Yang, Bingyi Kang, Zilong Huang, Zhen Zhao, Xiaogang Xu, Jiashi Feng, Hengshuang Zhao*.

Thanks for their work on precise depth estimation. Baesd on this, I implement a simple parallax effect. This effect is made up with a depth-based pixel movement estimation, a back-to-forth pixel assignment and  Telea's traditional image-restoring algorithm (Alexandru Telea, 2004). The code is low in optimization.

This project is soly available on Windows.

## Getting Started

We recommend setting up a virtual environment. Using e.g. miniconda, the environment can be installed via:

```bash
conda create -n depth-parallax -y python=3.10.18
conda activate depth-parallax

pip install -r requirements.txt

mkdir checkpoints
# get pretrained model, 'base' for example
wget https://huggingface.co/depth-anything/Depth-Anything-V2-Base/resolve/main/depth_anything_v2_vitb.pth?download=true
```

Besides Depth Anything V2, additional packages in need are also supplemented in this installation.

### How to run

Following `get_parallax.bat`, simply run the command below on Windows PowerShell or other terminals.
```bash
.\get_parallax.bat
```

### How to use Depth Anything V2

To download pretrained checkpoints, click links below:

| Model | Params | Checkpoint |
|:-|-:|:-:|
| Depth-Anything-V2-Small | 24.8M | [Download](https://huggingface.co/depth-anything/Depth-Anything-V2-Small/resolve/main/depth_anything_v2_vits.pth?download=true) |
| Depth-Anything-V2-Base | 97.5M | [Download](https://huggingface.co/depth-anything/Depth-Anything-V2-Base/resolve/main/depth_anything_v2_vitb.pth?download=true) |
| Depth-Anything-V2-Large | 335.3M | [Download](https://huggingface.co/depth-anything/Depth-Anything-V2-Large/resolve/main/depth_anything_v2_vitl.pth?download=true) |
| Depth-Anything-V2-Giant | 1.3B | Coming soon |

```bash
python run.py \
  --encoder <vits | vitb | vitl | vitg> \
  --img-path <path> --outdir <outdir> \
  [--input-size <size>] [--pred-only] [--grayscale]   
```

Options:
- `--encoder`: Signals which pretrained weights you are going to use, where 'vits' is for 'small', 'vitb' for 'base' and so on. 
- `--img-path`: You can either 1) point it to an image directory storing all interested images, 2) point it to a single image, or 3) point it to a text file storing all image paths.
- `--input-size` (optional): By default, we use input size `518` for model inference. ***You can increase the size for even more fine-grained results.***
- `--pred-only` (optional): Only save the predicted depth map, without raw image.
- `--grayscale` (optional): Save the grayscale depth map, without applying color palette.
