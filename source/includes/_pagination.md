# Pagination

Some endpoints that return collections are paginated. For these endpoints, the meta object will tell you the current page, count, total number of pages, and total count of the collection.

```shell--curl
curl "https://app.nusii.com/api/v2/proposals" \
  -H "Authorization: Token token=your_access_token"
```

```shell--cli
nusii proposals list --page 2 --per-page 10
```

```javascript
import { Nusii } from '@nusii/nusii';

const nusii = new Nusii({ apiKey: 'YOUR_API_KEY' });

const page = await nusii.proposals.list({ page: 2, per_page: 10 });
page.meta.total_pages; // 4

const next = await page.getNextPage();

// Or let the SDK fetch every page for you
for await (const proposal of nusii.proposals.listAll()) {
  console.log(proposal.title);
}
```


```json
{
  "data": [
    {...},
    {...}
  ],
  "meta": {
    "current_page": 2,
    "next_page": 3,
    "prev_page": 1,
    "total_pages": 4,
    "total_count": 89
  }
}
```

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Page number
per | 25 | Number of results per page
