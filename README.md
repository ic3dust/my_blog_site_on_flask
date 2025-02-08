# Welcome to my microblog project.

The project you are currently looking at is the remake of it's first version(because I am still
struggling to understand Git rebases T_T). I'm making it with the help
of the article, written by Miguel Grinberg on "Microblog on flask".
Enjoy looking through it and feel free to explore functions I add on my own(I am
planning to do so).

## First, make sure

You run

```bash
chmod +x setup.sh
./setup.sh
```

in the directory, where you did unpack this app to.
No worries, no malware. You do not need to run this every time you want to
run the app.

```bash
source venv/bin/activate
```

will be sufficient. All dependencies is stored there, which means you can run whatever you wont without excessive installations.

## Dealing with database

If you want to play with the database you need to:

1. Make sure you are initializing flask database with

```bash
flask db init
```

in venv first;

2. Then, when you create users, etc. make sure you do

```bash
 flask db upgrade
```

after

```bash
flask db migrate -m "migration"
```

3. Once all the changes have been registered you can use a

```bash
db.session.commit()
```

4. Use

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
