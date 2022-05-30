# Hetero-center-loss-for-cross-modality-person-re-id
Code for paper "Hetero-center loss for cross-modality person re-identification"

## Update:
2020-06-03：
Because pytorch  split the data of a batch to each gpu when using multi-gpus, the loss may be incorrectly computed. The users may need to use single gpu to reproduce the experimental results in the paper.

2020-01-07:
we fix up a bug in learning rate schedule, before that only the first three parameter group's learning rate will be correctly decay to 1/10. However, after fixing up the bug, the model's performance still stay the same. The updated model and code have been upload.

## Requirments:
**pytorch: 0.4.1(the higher version may lead to performance fluctuation)**

torchvision: 0.2.1

numpy: 1.17.4

python: 3.7


## Dataset:
**SYSU-MM01**

**Reg-DB**


## Run:
### SYSU-MM01:
1. prepare training set
```
python pre_process_sysu.py
```
2. train model
```
python train.py --dataset sysu --lr 0.008 --drop 0.0 --trial 1 --gpu 0 --epochs 60 --w_hc 0.6 --per_img 8 
```
* (Notice that you need to set the 88 line in train.py to your SYSU-MM01 dataset path)

3. evaluate model(single-shot all-search)
```
python test.py --dataset sysu --lr 0.01 --drop 0.0 --trial 1 --gpu 1 --low-dim 512 --resume 'Your model name' --w_hc 0.5 --mode all --gall-mode single --model_path 'Your model path'
```

### Reg-DB:
1. train model
```
python train.py --dataset regdb --lr 0.0098 --drop 0.0 --trial 1 --gpu 0 --epochs 80 --w_hc 0.58 --per_img 8
```

2. evaluate model
```
python test.py --dataset regdb --lr 0.01 --drop 0.0 --trial 1 --gpu 1 --low-dim 512 --resume 'Your model name' --w_hc 0.5  --model_path 'Your model path'
```

## Results:
 Dataset | Rank1  | mAP | model
 ---- | ----- | ------  | -----
 SYSU-MM01  | ~56% | ~54% | [BaiduYun(code:y2em)](https://pan.baidu.com/s/1Ty1WCBVUZvzGk-cQLK432w)
 RegDB | ~83% | ~72%  | [BaiduYun(code:y2em)](https://pan.baidu.com/s/1Ty1WCBVUZvzGk-cQLK432w)

## Tips:
Because this is the first time I use Github to release my code, maybe this project is a little difficult to read and use. If you have any question, please don't hesitate to contact me (zhuyuanxin98@outlook.com). I will reply to you as soon as possible.

Most of the code are borrowed from https://github.com/mangye16/Cross-Modal-Re-ID-baseline. I am very grateful to the author (@[mangye16](https://github.com/mangye16)) for his contribution and help.

**If you think this project useful, please give me a star and cite following papers:**

[1] Zhu Y, Yang Z, Wang L, et al. Hetero-Center Loss for Cross-Modality Person Re-Identification[J]. Neurocomputing, 2019.

[2] Ye M, Lan X, Wang Z, et al. Bi-directional Center-Constrained Top-Ranking for Visible Thermal Person Re-Identification[J]. IEEE Transactions on Information Forensics and Security, 2019.

