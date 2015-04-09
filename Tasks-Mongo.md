# Задания к лабораторной работе 5 MongoDB

1. Загрузить датасет, указанный в задании.
2. Составить запрос в соответствии с заданием.

### Датасет 1. Переписка Enron.

Этот датасет содержит переписку примерно 150 пользователей, в основном руководителей компании Enron. Поскольку полный датасет занимает в распакованном виде около 1,5 Гб, мы удалили из него поле `body` для уменьшения размера.

[Ссылка для скаивания](https://yadi.sk/d/3l92O1G6fJst5).

Исходный датасет находится [здесь](http://mongodb-enron-email.s3-website-us-east-1.amazonaws.com/)
Подробное описание, откуда этот датасет взялся , можно найти [здесь](http://www.cs.cmu.edu/~enron/)

Датасет содержит 501513 документов следующего вида:
```
{
    "_id" : ObjectId("4f16fc97d1e2d32371003e30"),
    "subFolder" : "notes_inbox",
    "mailbox" : "bass-e",
    "filename" : "459.",
    "headers" : {
        "X-cc" : "",
        "From" : "luis.mena@enron.com",
        "Subject" : "",
        "X-Folder" : "\\Eric_Bass_Dec2000\\Notes Folders\\Notes inbox",
        "Content-Transfer-Encoding" : "7bit",
        "X-bcc" : "",
        "To" : "eric.bass@enron.com",
        "X-Origin" : "Bass-E",
        "X-FileName" : "ebass.nsf",
        "X-From" : "Luis Mena",
        "Date" : "Tue, 14 Nov 2000 03:00:00 -0800 (PST)",
        "X-To" : "Eric Bass",
        "Message-ID" : "<296353.1075854677622.JavaMail.evans@thyme>",
        "Content-Type" : "text/plain; charset=us-ascii",
        "Mime-Version" : "1.0"
    }
}
```

### Датасет 2. Пьесы Шекспира.

Датасет получен с сайта [http://shakespeare.mit.edu](http://shakespeare.mit.edu) и содержит 36 пьес Уильяма Шекспира.

[Ссылка для скаивания](https://yadi.sk/d/ZX6Z0n-FfJst9).

Каждый документ пьесы содержит в себе коллекцию актов, состощих из сцен, каждая сцена содержит коллекцию реплик, разбитых на предложения например:

```
{
    "_id" : "Romeo and Juliet",
    "acts" : [ 
        {
            "title" : "ACT I",
            "scenes" : [ 
                {
                    "title" : "SCENE I. Verona. A public place.",
                    "action" : [ 
                        {
                            "character" : "SAMPSON",
                            "says" : [ 
                                "Gregory, o' my word, we'll not carry coals."
                            ]
                        }, 
                        {
                            "character" : "GREGORY",
                            "says" : [ 
                                "No, for then we should be colliers."
                            ]
                        }, 
						// ...
                        {
                            "character" : "GREGORY",
                            "says" : [ 
                                "To move is to stir; and to be valiant is to stand:", 
                                "therefore, if thou art moved, thou runn'st away."
                            ]
                        }, 
                        {
                            "character" : "SAMPSON",
                            "says" : [ 
                                "A dog of that house shall move me to stand: I will", 
                                "take the wall of any man or maid of Montague's."
                            ]
                        }, 
                        {
                            "character" : "GREGORY",
                            "says" : [ 
                                "That shows thee a weak slave; for the weakest goes", 
                                "to the wall."
                            ]
                        }, 
						// ...
				},
				// ...
			]
		},
		// ...
	]
}	
```

## Варианты заданий
1. Датасет 1. Для каждого дня недели посчитайте, сколько писем было отправлено на адрес `ebass@enron.com`?
1. Датасет 2. Найдите сцену с самым большим количеством реплик в сцене (надо указать название пьесы, акт и сцену)
2. Датасет 1. Покопаемся в переписке Shanna Husser и Eric Bass. Сколько писем каждый из них отправил другому?
1. Датасет 2. Количество актов и сцен в каждой пьесе
3. Датасет 1. Laurie Ellis иногда посылает письма с одинаковыми темами. Для каждой темы письма использованной в 2000 году, посчитайте, сколько раз она была использована.
1. Датасет 2. Список персонажей для каждой пьесы, отсортированный по алфавиту.
4. Датасет 1. Сколько человек отправляют письма сами себе?
1. Датасет 2. Сколько реплик у Джульетты?
4. Датасет 1. В какой папке больше всего писем?
1. Датасет 2. Количество персонажей в "Отелло"?
4. Датасет 1. Сколько различных отправителей в датасете?
1. Датасет 2. Какие персонажи встречаются больше чем в одной пьесе?
1. Датасет 1. В какой день недели отправлено максимальное количество писем?

1. * Датасет 2. Для каждой пьесы найдите персонажа, у которого самое большое количество реплик.
