# Aggregation Framework в MongoDB

[Подробная документация](http://docs.mongodb.org/manual/reference/operator/aggregation/)

**Важно!** Данное руководство содержит очень краткую информацию. Пожалуйста, обратитесь к документации.

Для составления сложных запросов в MongoDB имеется встроенный Aggregation Framework. Запрос выполняется методом `db.collectionname.aggregate()`. Действия, выполняемые в запросе, описываются с помощью операторов агрегации. 

Рассмотрим основные стадии:

- `$project`
	
	Аналог списка полей в операторе SQL `select`. Позволяет добавить новые поля или убрать существующие.
	
	Синтаксис:
	```
	{ $project: { <specifications> } }
	```
	
	Варианты описания полей:
	- `<field>: <1 or true>` - указывает, что данное поле датасета необходимо включить в выборку.
	- `_id: <0 or false>` - удаляет из выборки поле `_id` (по умолчанию это поле включается во все выборки, удалять другие поля таким способом нельзя).
	- `<field>: <expression>` - добавление нового поля, которого нет в исходных данных или изменение значения существующего поля.
	
- `$match`
	
	Аналог SQL-конструкции `where`. Задает условия, по которым фильтруются документы. Аналогичен условиям в методе `find()`.

	Синтаксис:
	```
	{ $match: { <query> } }
	```
	
- `$limit`
	
	Аналог SQL-конструкции `limit`. Ограничивает количество выбираемых документов.

	Синтаксис:
	```
	{ $limit: <positive integer> }
	```

- `$skip`

	Аналог SQL-конструкции `offset`. Позволяет пропустить несколько первыйх документов.

	Синтаксис:
	```
	{ $skip: <positive integer> }
	```

- `$unwind`

	Разбивает поле, содержащее массив.
	
	Синтаксис:
	```	
	{ $unwind: <field path> }
	```

	Пример:

	Исходные данные:
	
	```		
	{ "_id" : 1, "item" : "ABC1", sizes: [ "S", "M", "L"] }
	```	
	
	Команда:
	
	```	
	db.inventory.aggregate( [ { $unwind : "$sizes" } ] )
	```	

	Результат:
	
	```	
	{ "_id" : 1, "item" : "ABC1", "sizes" : "S" }
	{ "_id" : 1, "item" : "ABC1", "sizes" : "M" }
	{ "_id" : 1, "item" : "ABC1", "sizes" : "L" }
	```	
	
- `$group`

	Группирует документы по признаку, заданному в параметре `_id` и вычисляет аккумулирующие выражения (суммы, максимумы и минимумы, первое или последнее значение, собирает свойства из нескольких документов в один массив и т.д.)
	
	Синтаксис:
	```	
	{ $group: { _id: <expression>, <field1>: { <accumulator1> : <expression1> }, ... } }
	```	
	
- `$sort`

	Сортитует результаты, аналог SQL-конструкции `order by`.

	Синтаксис:
	```	
	{ $sort: { <field1>: <sort order>, <field2>: <sort order> ... } }
	```	

## Примеры

Рассмотрим работу фреймворка на примере датасета, содержащего почтовые индексы городов США. Датасет содержит записи такого вида:

```
{
  "_id": "10280",
  "city": "NEW YORK",
  "state": "NY",
  "pop": 5574,
  "loc": [
    -74.016323,
    40.710537
  ]
}
```

- `_id` - индекс в виде строки.
- `city` - название города, у города может быть больше одного индекса.
- `state` - сокращенное обозначение штата.
- `pop` - численность населения.
- `loc` - географические координаты.

 
Города с численностью больше 10 млн.

```
db.zipcodes.aggregate( [
   { $group: { _id: "$state", totalPop: { $sum: "$pop" } } },
   { $match: { totalPop: { $gte: 10*1000*1000 } } }
] )
```

Среднее по штатам:

```
db.zipcodes.aggregate( [
   { $group: { _id: { state: "$state", city: "$city" }, pop: { $sum: "$pop" } } },
   { $group: { _id: "$_id.state", avgCityPop: { $avg: "$pop" } } }
] )
```

Самый большой и самый маленький город:

```
db.zipcodes.aggregate( [
   { $group:
      {
        _id: { state: "$state", city: "$city" },
        pop: { $sum: "$pop" }
      }
   },
   { $sort: { pop: 1 } },
   { $group:
      {
        _id : "$_id.state",
        biggestCity:  { $last: "$_id.city" },
        biggestPop:   { $last: "$pop" },
        smallestCity: { $first: "$_id.city" },
        smallestPop:  { $first: "$pop" }
      }
   },

  // the following $project is optional, and
  // modifies the output format.

  { $project:
    { _id: 0,
      state: "$_id",
      biggestCity:  { name: "$biggestCity",  pop: "$biggestPop" },
      smallestCity: { name: "$smallestCity", pop: "$smallestPop" }
    }
  }
] )
```

