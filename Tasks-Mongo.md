# ������� � ������������ ������ 5 MongoDB

1. ��������� �������, ��������� � �������.
2. ��������� ������ � ������������ � ��������.

### ������� 1. ��������� Enron.

���� ������� �������� ��������� �������� 150 �������������, � �������� ������������� �������� Enron. ��������� ������ ������� �������� � ������������� ���� ����� 1,5 ��, �� ������� �� ���� ���� `body` ��� ���������� �������.

[������ ��� ���������](https://yadi.sk/d/3l92O1G6fJst5).

�������� ������� ��������� [�����](http://mongodb-enron-email.s3-website-us-east-1.amazonaws.com/)
��������� ��������, ������ ���� ������� ������ , ����� ����� [�����](http://www.cs.cmu.edu/~enron/)

������� �������� 501513 ���������� ���������� ����:
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

### ������� 2. ������ ��������.

������� ������� � ����� [http://shakespeare.mit.edu](http://shakespeare.mit.edu) � �������� 36 ����� ������� ��������.

[������ ��� ���������](https://yadi.sk/d/ZX6Z0n-FfJst9).

������ �������� ������ �������� � ���� ��������� �����, �������� �� ����, ������ ����� �������� ��������� ������, �������� �� ����������� ��������:

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

## �������� �������
1. ������� 1. ��� ������� ��� ������ ����������, ������� ����� ���� ���������� �� ����� `ebass@enron.com`?
1. ������� 2. ������� ����� � ����� ������� ����������� ������ � ����� (���� ������� �������� ������, ��� � �����)
2. ������� 1. ���������� � ��������� Shanna Husser � Eric Bass. ������� ����� ������ �� ��� �������� �������?
1. ������� 2. ���������� ����� � ���� � ������ ������
3. ������� 1. Laurie Ellis ������ �������� ������ � ����������� ������. ��� ������ ���� ������ �������������� � 2000 ����, ����������, ������� ��� ��� ���� ������������.
1. ������� 2. ������ ���������� ��� ������ ������, ��������������� �� ��������.
4. ������� 1. ������� ������� ���������� ������ ���� ����?
1. ������� 2. ������� ������ � ���������?
4. ������� 1. � ����� ����� ������ ����� �����?
1. ������� 2. ���������� ���������� � "������"?
4. ������� 1. ������� ��������� ������������ � ��������?
1. ������� 2. ����� ��������� ����������� ������ ��� � ����� ������?
1. ������� 1. � ����� ���� ������ ���������� ������������ ���������� �����?

1. * ������� 2. ��� ������ ������ ������� ���������, � �������� ����� ������� ���������� ������.
