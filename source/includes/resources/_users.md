# Users

## Get all Users

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/users"
```

```shell--cli
nusii users list
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::User.list(page: 1)
```

> The above command returns JSON structured like this:

```json
  "data": [
    {
      "id": "12",
      "type": "users",
      "attributes": {
        "email": "support@nusii.com",
        "name": "Michael",
      }
    }
  ],
  "meta": {
    "current-page": 2,
    "next-page": 3,
    "prev-page": 1,
    "total-pages": 4,
    "total-count": 52
  }
}
```

This endpoint retrieves all users.

### HTTP Request

`GET https://app.nusii.com/api/v2/users`
