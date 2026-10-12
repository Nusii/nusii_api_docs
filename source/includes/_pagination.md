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

```python
from nusii import Nusii

nusii = Nusii(api_key="YOUR_API_KEY")

page = nusii.proposals.list(page=2, per_page=10)
page.total_pages  # 4

next_page = page.get_next_page()

# Or let the SDK fetch every page for you
for proposal in nusii.proposals.list_all():
    print(proposal["title"])
```

```go
import "github.com/nusii/nusii-go"

n, err := nusii.New(nusii.WithAPIKey("YOUR_API_KEY"))

page, err := n.Proposals.List(ctx, &nusii.ProposalListParams{Page: 2, PerPage: 10})
fmt.Println(page.Meta.TotalPages) // 4

nextPage, err := page.NextPage(ctx)

// Or let the SDK fetch every page for you
for proposal, err := range n.Proposals.ListAll(ctx, nil) {
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(*proposal.Title)
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
