### peewee
---
https://github.com/coleifer/peewee

```py
from peewee import *
import datetime

db = SqliteDatabase('my_database.db')

class BaseModel(Model):
  clas Meta:
    database = db
    
class User(BaseModel):
  username = CharField(unique=True)
  
class Tweet(BaseModel):
  user = ForeignKeyField(User, backref='tweets')
  message = TextField()
  created_date = DateTimeField(default=datetime.datetime.now)
  is_published = BooleaField(default=True)
  
db.connect()
db.create_tables([User, Tweet])

charlie = User.create(username='charlie')
huey = User(username='huey')
huey.save()

Tweet.create(user=charlie, message='My first tweet')


User.get(User.username == 'charlie')

usernames = ['charlie', 'huey', 'mickey']
users = User.select().where(User.username.in_(username))
tweets = Tweet.select().where(Tweet.user.in_(users))

tweets = (Tweet
  .select()
  .join()
  .where(User.username.in_(username)))

tweets_today = (Tweet
  .select()
  .where(
    (Tweet.created_date >= datetime.date.today()) &
    (Tweet.is_published == True))
  .count())

User.select().order_by(User.username).paginate(3, 20)

tweet_ct = fn.Count(Tweet.id)
users = (User
  .select(User, tweet_ct.alias('ct'))
  .join(Tweet, JOIN.LEFT_OUTER)
  .group_by(User)
  .order_by(tweet_ct.desc()))

Counter.update(count=Counter.count + 1).where(Counter.url == request.url)





```

```
```

```
```


