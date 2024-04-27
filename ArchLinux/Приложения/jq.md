### Запрос строк без ковычек
~~~~
jq -r '.[].name' "fruits.json"
~~~~

### Поиск по имени
~~~~
jq -r ".[] | select(.name==\"$name\")" "fruits.json"
~~~~

#jq #json