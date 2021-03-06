# ������� CRUD � MongoDB

� ������ ����������� ��������� ����� ������� ��������. ����� ����������� ������������ ��� ��������� �������������� ���������� � ��������.

## ������ � ��������� ����

�� ������� MongoDB ����� ���� ��������� ��������� ��� ������.

`use mydatabase` - ����� ������� ����. `mydatabase` - ��� ����� ����. ���� ���� �� ����������, ��� ����� �������. ����� ���������� `use` ��������� ����������� ������ � ������ `db`, ����� ������� �������������� ������ � ������� ����.

������ ��� ������, ������� ����� ��������� � �����, ����� ��������, ��������� ������� `db.help()`.

������ ���� ������� �� ��������� ����������. ��������� - ��� ������ ������� � ����������� ����. ������� �������� �������� ���������� �������������� ������ �������. ������� `db.getCollectionNames()` �������� �������� ������ ���� ��������� � ����.���������� � ��������� ���������� ��������� `collectionname` ����� ���: `db.collectionname`.

��������� ������� �� ����������. �������� - ��� ������ ������ � ����������� ����. �������� �������� ������������ ����� �����, � ��� ����� ��������� �� ��� ����� ���� ��������� � ���������. ����� �������� ����������� �������� ���� `_id`, �������� �������� ������ ���� ���������� � �������� ���������. ����� �������� ������ �������� �������� ����� ���� ������. �� ������ ���� ��������� ��� ����. ���� ��� �������� ������ �� �� ������� �������� ���� `_id`, �� ��� ����� �������������� �������������.
  
## �������

[��������� ������������](http://docs.mongodb.org/manual/reference/method/db.collection.insert)

`db.collectionname`.insert(doc)` - ��������� ���� ��� ��������� ���������� � ���������. �������� ������ ���� ����������� � ������� JSON.

��������:

```
db.unicorns.insert({
	name: 'Aurora', 
	gender: 'f', 
	weight: 450})
```

## ������� ������

[������������ �� �������](http://jsman.ru/mongo-book/Glava-3-Osvaivaem-Find.html)

[��������� ������������](http://docs.mongodb.org/manual/reference/method/db.collection.find/)

`db.collectionname.find(query, projection)` - ���������� ������ SQL-��������� `select`. �������� `query` ������ ������� �������; `projection` - ������ ����� � �������.

������: ������� ������ ���� ����������, ������� ������ ������ 50.

```
db.unicorns.count(
	{
		weight: {$gt: 50}
	},
	{
		id:0,
		name:1
	})
```

��������� ������� �������������� � ���� ������������ ������� - �������. ���� ������ ������������� ����������� ��������� �� �������.

�������� ������� ������� �� ������ ����� � [������������](http://docs.mongodb.org/manual/reference/method/js-cursor/).

## ���������

[��������� ������������](http://docs.mongodb.org/manual/reference/method/db.collection.update)

 `db.collection.update(query, update, options)` - �������� ���������, ��������������� ������� `query` (���������� ����, ��� ������������ � `find`).
 
 �������� `update` ����� ���������:
- ��������, �� ������� ����� �������� ��� ��������� ���������,
- �������� ��������� ��������� � ������� ���������� `$inc` � `$set`.
 
������ ��������� ������ � `_id=1`:

```
db.books.update(
   { _id: 1 },
   {
     $inc: { stock: 5 },
     $set: {
       item: "ABC123",
       "info.publisher": "2222",
       tags: [ "software" ],
       "ratings.1": { by: "xyz", rating: 3 }
     }
   }
)
```

## ��������

[��������� ������������](http://docs.mongodb.org/manual/reference/method/db.collection.remove)

`db.collectionname.remove(query)` - ������� ���������, ��������������� �������. �������� `query` ���������� ���������������� ��������� � ������ `find()`.

������ �������� ���� ������� � ���������:

```
db.unicorns.remove( { } )
```

������ �������� ������� ���������� (����, � ���� ��� ������ 300):

```
db.unicorns.remove( { weight: { $gt: 300 } } )
```
