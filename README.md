# IT-School

Методы import/export'а модулей.

```js
// ES6 modules
import express from 'express';
export express;
```

```js
// Commonjs
const express = require('express');
module.exports = express
```

Пример GET запроса
```js
router
    .route("/popular")
    /**
     * @api {get} /tags/popular Popular Tags
     * @apiName GetPopularTags
     * @apiGroup Tags
     * @apiVersion 1.0.0
     *
     * @apiParam {Number} skip
     * @apiParam {Number} limit
     * @apiParam {Boolean} updateCache
     * @apiParam {String} interval
     */
    .get(
        async (
            {
                query: { skip = 0, limit = 5, updateCache },
                locals: { currentUserId },
            },
            res
        ) => {
            const query = { limit, skip };
            const options = { currentUserId, updateCache };

            const tags = [];

            return res.status(!tags || tags.error).json(tags);
        }
    );
```
