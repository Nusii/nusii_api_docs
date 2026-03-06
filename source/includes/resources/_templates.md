# Templates

## Get all Templates

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/templates"

# Get only public templates
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/templates?public_templates=true"
```

```shell--cli
nusii templates list

# Get only public templates
nusii templates list --public-templates
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Template.list(page: 1)
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "12",
      "type": "templates",
      "attributes": {
        "name": "Web Design Proposal",
        "created_at": "2024-01-15T10:30:00.000Z",
        "public_template": false
      }
    }
  ],
  "meta": {
    "current_page": 1,
    "next_page": null,
    "prev_page": null,
    "total_pages": 1,
    "total_count": 1
  }
}
```

This endpoint retrieves all templates.

### HTTP Request

`GET https://app.nusii.com/api/v2/templates`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
public_templates | false | If set to true, returns only public templates instead of your account's templates.

## Get a Template

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/templates/:id"
```

```shell--cli
nusii templates get 12
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Template.get(12)
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "12",
    "type": "templates",
    "attributes": {
      "name": "Web Design Proposal",
      "account_id": 3,
      "created_at": "2024-01-15T10:30:00.000Z",
      "public_template": false,
      "dummy_template": false
    }
  }
}
```

This endpoint retrieves a single template.

### HTTP Request

`GET https://app.nusii.com/api/v2/templates/:id`
