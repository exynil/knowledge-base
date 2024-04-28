### Дамп `json` с кириллицей

~~~~python
import json

dictionary = {}

json_object = json.dumps(dictionary, indent=4, ensure_ascii=False)

with open("sample.json", "w") as outfile:
    outfile.write(json_object)
~~~~