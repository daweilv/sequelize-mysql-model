# sequelize-mysql-model

modify from [SequelizeAuto - 0.4.29](https://github.com/sequelize/sequelize-auto)
Automatically generate models for [SequelizeJS](https://github.com/sequelize/sequelize).

**Programmatic API Only**

**Mysql Only**

more feature support

1. comment support

2. modelNameResolve

open this option will disable model camelCase

3. fileNameResolve

open this option will disable camelCaseForFileName



## Install

    npm install --save sequelize-mysql-model

## Prerequisites

You will need to install the correct dialect binding globally before using sequelize-auto.

Example for MySQL/MariaDB

`npm install -g mysql`

## Programmatic API

```js
var SequelizeAuto = require('sequelize-mysql-model')

var db = {
    host: 'host',
    user: 'user',
    password: 'password',
    database: 'database',
    port: '3306'
};

var auto = new SequelizeAuto(db.database, db.user, db.password, {
    host: db.host,
    dialect: 'mysql',
    port: db.port,
    directory: './models',
    additional: {
        timestamps: false
    },
    tables: ['f_user', 'f_article', 'f_article_category'],
    modelNameResolve: function (table_name) {
        if (table_name.indexOf("f_") !== -1) {
            return table_name.substring(2)
        } else {
            return table_name
        }
    },
    fileNameResolve: function (table_name) {
        if (table_name.indexOf("f_") !== -1) {
            return table_name.substring(2)
        } else {
            return table_name
        }
    }
});

auto.run(function (err) {
    if (err) throw err;

    console.log(auto.tables); // table list
    console.log(auto.foreignKeys); // foreign key list
});
```
