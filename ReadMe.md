# Comparison of VisionTransformer and EfficientNet families on CIFAR-10、CIFAR-100

WE trained several model on CIFAR-10 and CIFAR-100，with EffNet and ViT，the results are shown in the end，and some guidance  are given to help training.



### 1.Train Model with EffNet

```
python3 main.py --name cifar10-100_500 --dataset cifar10 --model_type B0 

```

CIFAR-10 and CIFAR-100 are automatically download and train. In order to use a different dataset you need to customize [data_utils.py](./utils/data_utils.py).

The default batch size is 512. When GPU memory is insufficient, you can proceed with training by adjusting the value of `--gradient_accumulation_steps`.

There are many Type of net as list below.

```
parser.add_argument("--model_type", choices=["B0", "B1", "B2", "B3", "B4", "B5","B6", "B7""L2",
                                                 "v2-s", "v2-m", "v2-l"],
                        default="B0",
                        help="Which variant to use.")
```



### 2.Train Model with ViT

```
python3 train.py --name cifar10-100_500 --dataset cifar10 --model_type ViT-B_16 --pretrained_dir checkpoint/ViT-B_16.npz
```

CIFAR-10 and CIFAR-100 are automatically download and train. In order to use a different dataset you need to customize [data_utils.py](./utils/data_utils.py).

The default batch size is 512. When GPU memory is insufficient, you can proceed with training by adjusting the value of `--gradient_accumulation_steps`.

Also can use [Automatic Mixed Precision(Amp)](https://nvidia.github.io/apex/amp.html) to reduce memory usage and train faster

```
python3 train.py --name cifar10-100_500 --dataset cifar10 --model_type ViT-B_16 --pretrained_dir checkpoint/ViT-B_16.npz --fp16 --fp16_opt_level O2
```





### 3.Results

| **Table1.1** The testing result of  several networks |           |                                |        |           |
| ---------------------------------------------------- | --------- | ------------------------------ | ------ | --------- |
| Model                                                | Dataset   | Acc.（our score/public score） | Params | Tain-time |
| ViT-B/16                                             | CIFAR-10  | 99.06/98.6                     | 83M    | 2         |
| ViT-H/14                                             | CIFAR-10  | 99.35/99.5                     | 632M   | 6         |
| ViT-B/16                                             | CIFAR-100 | 87.7/89.1                      | 83M    | 1         |
| ViT-H/14                                             | CIFAR-100 | -/94.5                         | 632M   | -         |
| EffNetv2-L                                           | CIFAR-10  | 99.08/99.1                     | 121M   | 2         |
| EffNetv2-M                                           | CIFAR-10  | 98.8/99.0                      | 55M    | 1         |
| EffNetv2-S                                           | CIFAR-10  | 98.5/98.7                      | 24M    | 0.5       |
| EffNet-B7                                            | CIFAR-10  | 98.7/98.9                      | 65M    | 0.5       |
| EffNetv2-L                                           | CIFAR-100 | 91.4/92.3                      | 121M   | 2         |
| EffNetv2-S                                           | CIFAR-100 | 91.7/92.2                      | 24M    | 0.75      |
| EffNet-B0                                            | CIFAR-100 | 87.4/-                         | 7M     | 0.5       |
| EffNet-B7                                            | CIFAR-100 | 90.8/91.7                      | 64M    | 1         |
| EffNet-L2                                            | CIFAR-100 | 95.9/96.0                      | 66M    | 1         |