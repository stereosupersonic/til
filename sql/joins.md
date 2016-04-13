# Joins

[good overview](https://de.wikibooks.org/wiki/Einf%C3%BChrung_in_SQL:_Mehr_zu_JOIN)

### Example

**users**

| id | name |
|--- |   ---|
|  1 |  Huber |
|  2 |  Maier |
|  3 |  Otto |

**trainings**

| id | user_id | points |
|---|---| ---|
|  1 | 1  |4 |
|  2 | 1  |5 |
|  3 | 2  |6 |

## inner joins

Der INNER JOIN führt Datensätze aus der linken und rechten Tabelle genau dann zusammen, wenn die angegebenen Kriterien alle erfüllt sind. Ist eines oder mehrere der Kriterien nicht erfüllt, so entsteht kein Datensatz in der Ergebnismenge

```
select * from users INNER JOIN  trainings ON (trainings.user_id = users.id)
```

| users.id  | name   | points |
|        ---|     ---|     ---|
|  1        |  Huber |      4 |
|  1        |  Huber |      5 |
|  2        |  Maier |      6 |

*the same as*
```
select * from users, trainings where trainings.user_id = users.id
```

## outer joins

Jeder Datensatz der rechten und der linken Tabelle kommt in die Ergebnismenge. Findet sich über das ON-Kriterium ein passendes Training werden beide zusammengefügt,
andernfalls wird die jeweils fehlende Seite mit NULL aufgefüllt.

```
select * from users LEFT OUTER JOIN trainings ON (trainings.user_id = users.id)
```


| users.id  | name   | points |
|        ---|     ---|     ---|
|  1        |  Huber |      4 |
|  1        |  Huber |      5 |
|  2        |  Maier |      6 |
|  3        |  Otto  |   NULL |
