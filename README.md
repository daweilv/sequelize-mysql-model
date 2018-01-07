# sequelize-mysql-model

modify from [SequelizeAuto - 0.4.29](https://github.com/sequelize/sequelize-auto)
Automatically generate models for [SequelizeJS](https://github.com/sequelize/sequelize).

** Programmatic API Only **
** Mysql Only **

add some feature

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

var auto = new SequelizeAuto('database', 'user', 'pass', {
    host: 'localhost',
    dialect: 'mysql'|'mariadb'|'sqlite'|'postgres'|'mssql',
    directory: false, // prevents the program from writing to disk
    port: 'port',
    additional: {
        timestamps: false
      },
      tables: ['users', 'topics'],
      camelCase:false,
      camelCaseForFileName:true,
      indentation:2,
      modelNameResolve: function (table_name) {
        if (table_name.indexOf("t_") !== -1) {
          return table_name.substring(2)
        } else {
          return table_name
        }
      },
      fileNameResolve:function (table_name) {
        if (table_name.indexOf("t_") !== -1) {
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
