```py
import json



# Open the file for reading
with open('sentence1-10000.json', 'r') as file, open('file2.json', 'w') as wrfile:
    # Iterate through each line in the file
    count = 0
    for line in file:
        # Process the line (here we're just printing it)
        line = line.strip()

        # Parse the JSON string
        original_json = json.loads(line)

        # Extract and split the name field
        name_parts = original_json['name'].split('，')

        # filter
        if len(name_parts[0]) < 5:
            continue

        # Create a new JSON object
        try:
            new_json = {
                "instruction": name_parts[0],
                "input": "",
                "output": name_parts[1].replace('。', '')
            }
        except Exception as e:
            print(f'发生错误: {e}')
            print("cttt cut ", name_parts)
            #exit()

        # Print the new JSON object
        output = json.dumps(new_json, ensure_ascii=False)
        output = output + ', \n'
        print(output)
        wrfile.write(output)
        count += 1

    print("all lines count:", count)
```

微调了一个古诗句的接龙  效果还可以见 https://huggingface.co/googcheng/7b-lora  
1 经典的古诗句拆分成alpaca格式(file3.json)  
2 训练大概10 epoch loss才可以很小  
3 测试  

```python
python src/cli_demo.py     --model_name_or_path baichuan-inc/Baichuan-7B     --template default     --finetuning_type lora     --checkpoint_dir path_to_sft_checkpoint/
```
