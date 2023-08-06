## train tutorial


```bash
nohup torchrun --nnodes 1 --nproc_per_node 1 llama_finetuning.py  --use_peft --peft_method lora --model_name ~/.cache/huggingface/hub/models--NousResearch--Llama-2-7b-hf/snapshots/42c97b7b5b132b46e5059f82850eaa6300ed6724/ --output_dir ~/autodl-tmp/PEFT/model -dataset alpaca_dataset --batch_size_training 80 --use_fp16 --quantization  > train.log  2>&1 &
```


## preprocess  
sed awk cat 我构造了一个30M的alpace数据集

## finetune  
https://github.com/facebookresearch/llama-recipes/
```bash
#first train
nohup python llama_finetuning.py --use_peft --peft_method lora --model_name ../Llama-2-7b-ms/ --use_fp16 --output_dir output/model --dataset alpaca_dataset --batch_size_training 32 --quantization  > train.log  2>&1 &
tail -f train.log 
```
## inference  
Llama 2上面微调这一点数据 几乎没有什么效果  
1. 和数据集的类型和大小可能有关 不是中文基座
2. 和lora配置相关

总体感觉不简单。
