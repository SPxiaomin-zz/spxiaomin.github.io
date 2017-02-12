---
title: hexo置顶功能
date: 2017-02-12 21:14:40
categories: ['技术']
tags: ['hexo']
---

按如下的步骤进行操作就可以了。

## 动手操作步骤

1. 安装 `hexo-generator-index`

    `npm i --save hexo-generator-index`

2. 将如下的代码加入 `node_modules/hexo-generator-index/lib/generator.js`

    ```javascript
    posts.data = posts.data.sort(function(a, b) {
        if(a.top && b.top) { // 两篇文章top都有定义
            if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
            else return b.top - a.top; // 否则按照top值降序排
        }
        else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
            return -1;
        }
        else if(!a.top && b.top) {
            return 1;
        }
        else return b.date - a.date; // 都没定义按照文章日期降序排
    });
    ```

    最终的 `node_modules/hexo-generator-index/lib/generator.js` 代码

    ```javascript
    'use strict';

    var pagination = require('hexo-pagination');

    module.exports = function(locals) {
        var config = this.config;
        var posts = locals.posts.sort(config.index_generator.order_by);
        var paginationDir = config.pagination_dir || 'page';

        posts.data = posts.data.sort(function(a, b) {
            if(a.top && b.top) { // 两篇文章top都有定义
                if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
                else return b.top - a.top; // 否则按照top值降序排
            }
            else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
                return -1;
            }
            else if(!a.top && b.top) {
                return 1;
            }
            else return b.date - a.date; // 都没定义按照文章日期降序排
        });

        return pagination('', posts, {
            perPage: config.index_generator.per_page,
            layout: ['index', 'archive'],
            format: paginationDir + '/%d/',
            data: {
              __index: true
            }
        });
    };
    ```

3. 在需要设置置顶的博文文章 `front-matter` 中设置 `top` 值，值越大排在越前面，举例如下：

    ```yaml
    title: hexo置顶功能
    date: 2017-02-12 21:14:40
    top: 1    
    ```

## 参考

[解决hexo置顶问题](http://www.netcan666.com/2015/11/22/%E8%A7%A3%E5%86%B3Hexo%E7%BD%AE%E9%A1%B6%E9%97%AE%E9%A2%98/)
