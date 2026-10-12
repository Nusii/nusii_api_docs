# Themes

## Get all Themes

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/themes"
```

```shell--cli
nusii themes list
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->themes()->list();
```

```javascript
import { Nusii } from '@nusii/nusii';

const nusii = new Nusii({ apiKey: 'YOUR_API_KEY' });

const themes = await nusii.themes.list();
```

```python
from nusii import Nusii

nusii = Nusii(api_key="YOUR_API_KEY")

themes = nusii.themes.list()
```

```go
import "github.com/nusii/nusii-go"

n, err := nusii.New(nusii.WithAPIKey("YOUR_API_KEY"))

themes, err := n.Themes.List(ctx)
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "clean",
    "name": "Modern Theme"
  },
  {
    "id": "classic",
    "name": "Classic Theme"
  }
]
```

This endpoint retrieves all available themes.

### HTTP Request

`GET https://app.nusii.com/api/v2/themes`
