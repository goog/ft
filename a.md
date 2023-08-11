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
