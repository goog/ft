## train tutorial


```bash
nohup torchrun --nnodes 1 --nproc_per_node 1 llama_finetuning.py  --use_peft --peft_method lora --model_name ~/.cache/huggingface/hub/models--NousResearch--Llama-2-7b-hf/snapshots/42c97b7b5b132b46e5059f82850eaa6300ed6724/ --output_dir ~/autodl-tmp/PEFT/model -dataset alpaca_dataset --batch_size_training 80 --use_fp16 --quantization  > train.log  2>&1 &
```
