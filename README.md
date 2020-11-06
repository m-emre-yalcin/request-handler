# Generate Url

install:

`npm i generate-url`

*This module is also compatible with `strapi.js` APIs*

## Example usages

Generate an url for making api request:

```javascript
import generateUrl from 'generate-url'

let url = generateUrl({
        path: 'sections',
        query: { // you can define queries according to your API
            _start: 0,
            _limit: 20,
            _where: { // _where query has a special setter for strapi APIs
                id_eq: 5
            },
            _sort: 'id:DESC'
        },
    })
/* url = /sections?_start=0&_limit=20&_where[id_eq]=5&_sort=id:DESC */
axios.get('localhost:1337/' + url)
```

Generate url without query string

```javascript
let url = index.generateUrl({
    path: 'sections',
    query: false // if you don't want to use the query, you need to pass it 'false'
})
/* url = /sections */
```

>if you dont define the `query` property, it will use the default query object:

```javascript
{
    _start: 0,
    _limit: 10,
    _sort: 'id:DESC',
}
```

Generate url with a `parameter` and default `query`

```javascript
let url = index.generateUrl({
    path: 'sections/:id',
    params: {
        id: 1
    },
})
/* url = /sections/1?_start=0&_limit=10&_sort=id:DESC */
```

Generate url with multiple `parameter` and `query`

```javascript
let url = index.generateUrl({
    path: 'sections/:sectionId/task/:taskId',
    params: {
        sectionId: 1,
        taskId: 2
    },
    query: {
        _start: 0,
        _limit: 20,
        _where: {
            id_eq: 5
        },
        _sort: 'id:DESC'
    },
})
/* url = /sections/1/task/2?_start=0&_limit=20&_where[id_eq]=5&_sort=id:DESC */
```