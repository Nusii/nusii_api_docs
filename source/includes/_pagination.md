# Pagination

Some endpoints that return collections are paginated. For these endpoints, the meta object will tell you the current page, count, total number of pages, and total count of the collection.

```shell--curl
curl "https://app.nusii.com/api/v2/proposals" \
  -H "Authorization: Token token=your_access_token"
```

```shell--cli
nusii proposals list --page 2 --per-page 10
```


```json
{
  "data": [
    {...},
    {...}
  ],
  "meta": {
    "current-page": 2,
    "next-page": 3,
    "prev-page": 1,
    "total-pages": 4,
    "total-count": 89
  }
}
```

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Page number
per | 25 | Number of results per page
