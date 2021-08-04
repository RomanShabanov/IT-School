# IT-School

[Работа с Модулями](#работа-с-модулями)

[Маршрутизация](#маршрутизация)
- [GET Запрос](#пример-get-запроса)
- [POST Запрос](#пример-post-запроса)
- [PUT Запрос](#пример-put-запроса)
- [DELETE Запрос](#пример-delete-запроса)

## Работа с Модулями
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

## Маршрутизация

#### Пример GET запроса
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

#### Пример POST запроса
```js
router
    .route("/")
    /**
     * @api {post} /communities Create new community
     * @apiName CreateCommunity
     * @apiGroup Communities
     * @apiVersion 1.0.0
     */
    .post(authorized, async ({ body, locals: { currentUserId } }, res) => {
        const data = { ...body, userId: currentUserId };
        const options = { currentUserId };

        const community = await communitiesController.createCommunity(
            data,
            options
        );

        return res.status(community.error ? 400 : 200).json(community);
    });
```

#### Пример PUT запроса
```js
router
    .route("/:id")
    /**
     * @api {put} /communities/:id Update Community Details
     * @apiName UpdateCommunity
     * @apiGroup Communities
     * @apiVersion 1.0.0
     */
    .put(
        authorized,
        validator.updateCommunity,
        async ({ params: { id }, body, locals: { currentUserId } }, res) => {
            const data = { id, userId: currentUserId, ...body };
            const options = { currentUserId };

            const result = await communitiesController.updateCommunity(
                data,
                options
            );

            return res.status(result.error ? 400 : 200).json(result);
        }
    );
```

#### Пример DELETE запроса
```js
router
    .route("/:id")
    /**
     * @api {delete} /communities/:id/join Join Community
     * @apiName JoinCommunity
     * @apiGroup Communities
     * @apiVersion 1.0.0
     */
    .delete(
        authorized,
        async ({ params: { id }, locals: { currentUserId } }, res) => {
            const query = { id };
            const options = { currentUserId };

            const community = await communitiesController.deleteCommunity(
                query,
                options
            );

            return res.status(community.error ? 400 : 200).json(community);
        }
    );
```
