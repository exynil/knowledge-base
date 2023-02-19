# grep

### Поиск слова в файлах
~~~~
grep -rnw '/path/to/somewhere/' -e 'pattern'
~~~~

-r or -R is recursive

-n is line number, and

-w stands for match the whole word.

-l (lower-case L) can be added to just give the file name of matching files.

-e is the pattern used during the search

### Поиск трэйлинг вайтспейсов
~~~~
grep -r "[[:blank:]]$" -I . --exclude-dir=node_modules --exclude-dir=media --exclude-dir=postres-data --exclude-dir=__pycache__
~~~~

### хештеги: #grep