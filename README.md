# sequelize-mysql-model

Modify from [SequelizeAuto - 0.4.29](https://github.com/sequelize/sequelize-auto).
Automatically generate models for [SequelizeJS](https://github.com/sequelize/sequelize).

**Programmatic API Only**

**Mysql Only**

## Feature Support

1. comment support

2. modelNameResolve function support

    open this option will disable model camelCase

3. fileNameResolve function support

    open this option will disable camelCaseForFileName



## Install

    npm install --save-dev sequelize-mysql-model



## Prerequisites

You will need to run `npm install --save mysql` before using sequelize-mysql-model.


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

Produces a file/files such as ./models/article.js which looks like:

```js
module.exports = function (sequelize, DataTypes) {
    return sequelize.define('article', {
        id: {
            allowNull: false,
            primaryKey: true,
            type: DataTypes.STRING(30),
            title: "id",
            formType: "TEXT"
        },
        article_category_id: {
            allowNull: false,
            type: DataTypes.STRING(30),
            title: "分类id",
            formType: "TEXT"
        },
        name: {
            allowNull: false,
            type: DataTypes.STRING(50),
            title: "名称",
            formType: "TEXT"
        },
        author: {
            allowNull: false,
            type: DataTypes.STRING(10),
            title: "作者",
            formType: "TEXT"
        },
        content: {
            allowNull: false,
            type: DataTypes.TEXT,
            title: "内容",
            formType: "TEXT"
        },
        content_md: {
            allowNull: false,
            type: DataTypes.TEXT,
            title: "markdown源格式",
            formType: "TEXT"
        },
        brief: {
            allowNull: false,
            type: DataTypes.STRING(400),
            title: "摘要",
            formType: "TEXT"
        },
        cover: {
            allowNull: false,
            type: DataTypes.STRING(100),
            title: "封面",
            formType: "TEXT"
        },
        is_show_cover: {
            allowNull: false,
            defaultValue: '0',
            type: DataTypes.INTEGER(4),
            title: "是否显示封面",
            formType: "SELECT",
            formValue: {0: "不显示", 1: "显示"}
        },
        is_show_comment: {
            allowNull: false,
            defaultValue: '1',
            type: DataTypes.INTEGER(4),
            title: "是否显示评论",
            formType: "SELECT",
            formValue: {0: "不显示", 1: "显示"}
        },
        is_publish: {
            allowNull: false,
            defaultValue: '1',
            type: DataTypes.INTEGER(4),
            title: "是否发布",
            formType: "SELECT",
            formValue: {0: "未发布", 1: "已发布"}
        },
        is_show: {
            allowNull: false,
            defaultValue: '1',
            type: DataTypes.INTEGER(4),
            title: "是否可见",
            formType: "SELECT",
            formValue: {0: "不可见", 1: "可见"}
        },
        tag: {
            allowNull: true,
            type: DataTypes.STRING(100),
            title: "标签",
            formType: "TEXT"
        },
        seo_url: {
            allowNull: true,
            type: DataTypes.STRING(50),
            title: "SEO链接",
            formType: "TEXT",
            unique: true
        },
        seo_keywords: {
            allowNull: true,
            type: DataTypes.STRING(200),
            title: "SEO关键词",
            formType: "TEXT"
        },
        seo_description: {
            allowNull: true,
            type: DataTypes.STRING(200),
            title: "SEO描述",
            formType: "TEXT"
        },
        publish_at: {
            allowNull: true,
            type: DataTypes.STRING(24),
            title: "发布日期",
            formType: "TEXT"
        },
        create_at: {
            allowNull: true,
            type: DataTypes.STRING(24),
            title: "创建日期",
            formType: "TEXT"
        },
        create_by: {
            allowNull: true,
            type: DataTypes.STRING(30),
            title: "创建人",
            formType: "TEXT"
        },
        update_at: {
            allowNull: true,
            type: DataTypes.STRING(24),
            title: "更新日期",
            formType: "TEXT"
        },
        update_by: {
            allowNull: true,
            type: DataTypes.STRING(30),
            title: "更新人",
            formType: "TEXT"
        },
        delete_at: {
            allowNull: true,
            type: DataTypes.STRING(24),
            title: "删除日期",
            formType: "TEXT"
        },
        delete_by: {
            allowNull: true,
            type: DataTypes.STRING(30),
            title: "删除人",
            formType: "TEXT"
        }
    }, {
        tableName: 'f_article',
        timestamps: false
    });
};


```