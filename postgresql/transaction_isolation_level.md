# Transaction Isolation Level

## get the isolation level

```
select current_setting('transaction_isolation');  
```

```Read committed``` is the default isolation level in PostgreSQL
http://www.postgresql.org/docs/9.4/static/transaction-iso.html

## Read Committed [Wikipedia](https://de.wikipedia.org/wiki/Isolation_(Datenbank)#Read_Committed)

Diese Isolationsebene setzt für die gesamte Transaktion Schreibsperren auf Objekten, die verändert werden sollen, setzt Lesesperren aber nur kurzzeitig beim tatsächlichen Lesen der Daten ein. Daher können Non-Repeatable Read und Phantom Read auftreten, wenn während wiederholten Leseoperationen auf dieselben Daten, zwischen der ersten und der zweiten Leseoperation, eine Schreiboperation einer anderen Transaktion die Daten verändert und committed.
