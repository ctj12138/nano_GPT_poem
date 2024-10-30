
# nanoGPT_poem

使用来自[chinese-poetry](https://github.com/chinese-poetry/chinese-poetry)中的唐诗训练集训练

使用`data/tangpoem/generate_poem.py`对原数据集进行处理，得到符合要求的.txt训练数据

## install

```
pip install torch numpy transformers datasets tiktoken wandb tqdm
```

Dependencies:

- [pytorch](https://pytorch.org) <3
- [numpy](https://numpy.org/install/) <3
-  `transformers` for huggingface transformers <3 (to load GPT-2 checkpoints)
-  `datasets` for huggingface datasets <3 (if you want to download + preprocess OpenWebText)
-  `tiktoken` for OpenAI's fast BPE code <3
-  `wandb` for optional logging <3
-  `tqdm` for progress bars <3

## quick start

使用以下指令对数据集进行划分
```
python data/tangpoem/prepare.py
```
然后使用划分好的数据集进行训练

由于我使用的设备Pytorch版本<2，因此我使用的完整命令如下：
```
python train.py config/train_poem_char.py --compile=False --eval_iters=200 --log_interval=1 --block_size=64 --batch_size=32 --n_layer=4 --n_head=4 --n_embd=128 --max_iters=5000 --lr_decay_iters=2000 --dropout=0.0
```
训练结果如下所所示
```
step 5000: train loss 4.2475, val loss 4.9031
iter 5000: loss 4.3615, time 1258.92ms, mfu 0.72%
```
然后使用sample去采样训练后模型的输出

```
python sample.py --out_dir=out-poem-char
```
部分输出结果如下所示
```
六月方分界，無因理法身。法覺心如此，真如地覺方。
中生佛佛界，不用可忘却。心如自破時，法法非見理。
三更難說學，絕氣靜先生。不知天地間，相看不可聞。
人意當事事，無計是真名。不學有大用，會見我有閑。
日夜忽不在，何言還不來。因君莫驚夢，歸鳥不同來。
此夜起心起，我今猶在城。吾今問山老，此事不自嗟。
十年六字少，再覺又年年。不是青青耳，須教玉縷人。
二月來方遠，真園獨樂居。閑緣不可見，西浦不無源。
春來心自閑，日暮雨相望。但見春風吹，聊以空幽幽。
萬里山無去，遥無大主人。思他兩路去，醉客不相開。
朝來月上上，暮嶺水長流。何處望千里，雲煙下一舟。
山下春水早，春來競去歸。小天有幽處，東北幾時時。
落月花殘月，留金意更深。不知春雨過，欲逐舞花來。
青青如湖水，不惜江林開。何見桃花塢，千花落落花。
清溪發清晨，影影亂閒日。何處起書舟，此處明月月。
清燈徹空落，落葉無一步。誰看月落日，不待月中夕。
一線出圓圓，清臺千尺石。千山歸不眠，一夜起方路。
開手垂雙眼，黄昏在此身。只今無限事，不及下秋時。
春來多老淚，風味带輕春。不似春風好，何妨落落花。
幽懷因酒事，共與別病心。人歸一家意，何處惜春來。
```