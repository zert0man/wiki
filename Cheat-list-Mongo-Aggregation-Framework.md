# Aggregation Framework � MongoDB

[��������� ������������](http://docs.mongodb.org/manual/reference/operator/aggregation/)

**�����!** ������ ����������� �������� ����� ������� ����������. ����������, ���������� � ������������.

��� ����������� ������� �������� � MongoDB ������� ���������� Aggregation Framework. ������ ����������� ������� `db.collectionname.agregate()`. ��������, ����������� � �������, ����������� � ������� ���������� ���������. 

���������� �������� ������:

- `$project`
	
	������ ������ ����� � ��������� SQL `select`. ��������� �������� ����� ���� ��� ������ ������������.
	
	���������:
	```
	{ $project: { <specifications> } }
	```
	
	�������� �������� �����:
	- `<field>: <1 or true>` - ���������, ��� ������ ���� �������� ���������� �������� � �������.
	- `_id: <0 or false>` - ������� �� ������� ���� `_id` (�� ��������� ��� ���� ���������� �� ��� �������, ������� ������ ���� ����� �������� ������).
	- `<field>: <expression>` - ���������� ������ ����, �������� ��� � �������� ������ ��� ��������� �������� ������������� ����.
	
- `$match`
	
	������ SQL-����������� `where`. ������ �������, �� ������� ����������� ���������. ���������� �������� � ������ `find()`.

	���������:
	```
	{ $match: { <query> } }
	```
	
- `$limit`
	
	������ SQL-����������� `limit`. ������������ ���������� ���������� ����������.

	���������:
	```
	{ $limit: <positive integer> }
	```

- `$skip`

	������ SQL-����������� `offset`. ��������� ���������� ��������� ������� ����������.

	���������:
	```
	{ $skip: <positive integer> }
	```

- `$unwind`

	��������� ����, ���������� ������.
	
	���������:
	```	
	{ $unwind: <field path> }
	```

	������:

	�������� ������:
	
	```		
	{ "_id" : 1, "item" : "ABC1", sizes: [ "S", "M", "L"] }
	```	
	
	�������:
	
	```	
	db.inventory.aggregate( [ { $unwind : "$sizes" } ] )
	```	

	���������:
	
	```	
	{ "_id" : 1, "item" : "ABC1", "sizes" : "S" }
	{ "_id" : 1, "item" : "ABC1", "sizes" : "M" }
	{ "_id" : 1, "item" : "ABC1", "sizes" : "L" }
	```	
	
- `$group`

	���������� ��������� �� ��������, ��������� � ��������� `_id` � ��������� �������������� ��������� (�����, ��������� � ��������, ������ ��� ��������� ��������, �������� �������� �� ���������� ���������� � ���� ������ � �.�.)
	
	���������:
	```	
	{ $group: { _id: <expression>, <field1>: { <accumulator1> : <expression1> }, ... } }
	```	
	
- `$sort`

	��������� ����������, ������ SQL-����������� `order by`.

	���������:
	```	
	{ $sort: { <field1>: <sort order>, <field2>: <sort order> ... } }
	```	

## �������

���������� ������ ���������� �� ������� ��������, ����������� �������� ������� ������� ���. ������� �������� ������ ������ ����:

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

- `_id` - ������ � ���� ������.
- `city` - �������� ������, � ������ ����� ���� ������ ������ �������.
- `state` - ����������� ����������� �����.
- `pop` - ����������� ���������.
- `loc` - �������������� ����������.

 
������ � ������������ ������ 10 ���.

```
db.zipcodes.aggregate( [
   { $group: { _id: "$state", totalPop: { $sum: "$pop" } } },
   { $match: { totalPop: { $gte: 10*1000*1000 } } }
] )
```

������� �� ������:

```
db.zipcodes.aggregate( [
   { $group: { _id: { state: "$state", city: "$city" }, pop: { $sum: "$pop" } } },
   { $group: { _id: "$_id.state", avgCityPop: { $avg: "$pop" } } }
] )
```

����� ������� � ����� ��������� �����:

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

