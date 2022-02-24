title: CRUD in MongoDB
date: 2021-03-16 17:46:38
tags:
---
CRUD operations in MongoDB, i.e. Create, Read, Update, Delete.

The code is for Pymongo.


Preparation
```python
import datetime
from pymongo import MongoClient

client = MongoClient()
db = client.test_database
collection = db.test_collection

post = {'author': 'Mike',
        'text': 'My first blog post!',
        'tags': ['mongodb', 'python', 'pymongo'],
        'date': datetime.datetime.utcnow()}
```

CREATE:
```python
def create_lines():
    collection.insert_one(post)
    # if we have multiple posts (an array of dictionaries)
    collection.insert_many(posts)
```

READ:
```python
def read_lines():
    collection.find_one({'author': 'Mike'})
    # if we want to find multiple records at the same time
    collection.find_many({'author': 'Mike'})
```

UPDATE:
```python
def update_lines():
    collection.update_one({'author': 'Mike'},
                          {'$set': {'text': 'My second blog post!'}})
    # if we want to update all the relevant records at the same time
    collection.update_many({'author': 'Mike'},
                          {'$set': {'text': 'My second blog post!'}})
```

DELETE:
```python
def delete_lines():
    collection.delete_one({'author': 'Mike'})
    # if we want to delete the matched records all at once
    collection.delete_many({'author': 'Mike'})
```

I would say MongoDB is designed in a way that is very user-friendly.

Check out the pymongo website for more detailed instructions.
https://pymongo.readthedocs.io/en/stable/tutorial.html