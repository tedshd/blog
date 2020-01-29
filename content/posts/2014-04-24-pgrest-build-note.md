---
layout: post
title: 'PgREST - build note'
date: 2014-04-24
comments: true
categories: [PostgreSQL]
---
## PgREST - build note

### [GitHub](https://github.com/pgrest/pgrest/)

## <strong style="color:red">This is Mac OS X build</strong>

### install PostgreSQL
[postgres.app](http://postgresapp.com/)
[PostgreSQL Tutorial](http://www.tutorialspoint.com/postgresql/index.htm)

1. set PATH in shell(.bashrc, .zshrc, ...)
```sh
PATH="/Applications/Postgres.app/Contents/Versions/9.3/bin:$PATH"
```

2. create the plv8 extension
```sh
-> psql -U Ted_Shiu -c "create extension plv8"
CREATE EXTENSION
```

### install PgREST(Must install node.js before)
```sh
npm i -g pgrest
```


[Refer - PgREST: Node.js in the Database](http://pgre.st/)
