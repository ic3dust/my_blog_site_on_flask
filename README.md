# Welcome to my microblog project.

The project you are currently looking at is the remake of it's first version(because I am still
struggling to understand Git rebases T_T). I'm making it with the help
of the article, written by Miguel Grinberg on "Microblog on flask".
Enjoy looking through it and feel free to explore functions I add on my own(I am
planning to do so).

## Run the app

You run

```bash
chmod +x setup.sh
./setup.sh
```

You do not need to run this every time you want to
run the app,

```bash
source venv/bin/activate
```

will be sufficient. All dependencies is stored there, which means you can run whatever you want without excessive installations.

To run the app you need to set an environmental variable file with all the credentials:

```bash
echo .env >> "FLASK_APP=microblog.py
MAIL_SERVER=localhost
MAIL_PORT=8025"
```

and than you can throw

```bash
flask run
```

to finally run the app.

Everytime before I push anything, I make sure I modificated .env file and config accordingly, and also init.py to keep the local secret keys and be able to use them, while working with the features of the application. Beforehand, I make changes to those 3 files as I push the examples and to be able to run the flask server I have to include those "sample" files, as the app can not work without them.

The app stores the database locally in the app.db file in the basedir, so to try all the app features you have to
create the table of users and posts manually. Don't worry, you can do it likewise on the website after you run flask.

## Dealing with database directly

If you want to deal with info in database via console:

1. Run shell(python or flask)

```bash
flask shell
```

in venv first;

2. Import necessities:

```bash
from app.models import User,Post,...
import sqlalchemy as sa
from app import db
```

3. Then make your query:

```bash
queryU=sa.select(User)
queryP=sa.select(Post)
```

# Display all posts:

```bash
queryP=sa.select(Post)
db.session.scalars(queryP).all()
```

# Create posts:

````bash
u=db.session.get(User 1)
p=Post(body="I'm user 1", author=u)
db.session.add(p)
db.session.commit()
# Remove posts:

```bash
post = db.session.get(Post,1)
db.session.delete(post)
db.session.commit()
````

or remove all of them:

```bash
db.session.query(Post).delete()
db.session.commit()
```

# Get users/posts

```bash
user = db.session.get(User,1)
print(user)
```

or get all of them:

```bash
posts = db.session.query(Post).all()
```

OR get their id's/posts:

```bash
for user in User:
...     print(user.id,user.username)
...
```

# Set a password for a user and check it like that:

```bash
u=User(username='johnny', email='johhnythebest@gmail.com')
u.set_password('hashme!')
u.checkpassword('hash!') #False
u.checkpassword('hashme!') #True
db.session.add(u)
db.session.commit()
```

# Example of DB language for queries in shell:

```bash
query = sa.select(User).where(User.username.like('s%'))
```

When you add new columns, change existing, rename tables or changing relationships
you need to upgrade database(but do not after adding a row)[Changing a schema of the DB to say]:

```bash
 flask db upgrade
```

after

```bash
flask db migrate -m "description of what you've changed"
```

Attention: the first migration will contain posts column as well as the users' one, because the MODELS.PY file
already contains models for posts.

Once all the changes have been registered you can use a

```bash
db.session.commit()
```

To remove commit use:

```bash
db.session.rollback()
```

or remove the object from the session:

```bash
db.session.expunge(user)

```

Use

```bash
flask db downgrade base
```

to reset the database to it's initial state.

, which writes all the changes atomically.

### Example(acting in database directly):

> > > u = User(username='susan', email='susan@example.com')
> > > u.set_password('your password')
> > > db.session.add(u)
> > > db.session.commit()

The answer to the query "select all users":

> > > query = sa.select(User)
> > > users = db.session.scalars(query).all()
> > > users
> > > [<User john>, <User susan>]

If you would use flask shell, py, python or python3 interpreters, to exit just press CTRL+Z.
