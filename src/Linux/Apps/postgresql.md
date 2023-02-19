# PostgreSQL

Сброс счетчика автоинкрементирования
~~~~
TRUNCATE work_types_worksection RESTART IDENTITY
~~~~

Сброс счётчика на определенный номер
~~~~
ALTER SEQUENCE product_id_seq RESTART WITH 88
~~~~

### хештеги:  #postgresql