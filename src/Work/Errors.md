# Ошибки

## Превышен лимит одновременного подключения к бд
~~~~
conn = Database.connect(connstr,
django.db.utils.OperationalError: ('08001', '[08001] [Microsoft][ODBC Driver 17 for SQL 
Server]Client unable to establish connection because an error was encountered during 
handshakes before login. Common causes include client attempting to connect to an 
unsupported version of SQL Server, server too busy to accept new connections or a 
resource limitation (memory or maximum allowed connections) on the server. (26) 
(SQLDriverConnect)')
~~~~

Решение: Отключить все сторонние подключения к бд


## Нет доступа к папке
~~~~
/opt/mssql/bin/sqlservr: Error: The system directory [/.system] could not be 
created.  Errno [13]
~~~~
Решение: Дать права на монтируемый раздел
~~~~
sudo chown -R 10001 *
~~~~

## Ошибка с staticfiles
~~~~
'staticfiles' is not a registered tag library. Must be one of:
~~~~

Решение: Заменить `staticfiles` на `static`
