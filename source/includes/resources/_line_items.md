# Line Items

## Get all line items

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/line_items"
```

```shell--cli
nusii line-items list
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::LineItem.list(page: 1)
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "154",
      "type": "line_items",
      "attributes": {
        "section_id": 458,
        "name": "Redesign website",
        "position": 1,
        "cost_type": "fixed",
        "recurring_type": null,
        "per_type": null,
        "quantity": null,
        "updated_at": "2017-11-24T10:30:40.282Z",
        "created_at": "2017-11-24T10:30:40.282Z",
        "currency": "GBP",
        "amount_in_cents": 150000,
        "amount_formatted": "£1,500.00",
        "total_in_cents": 150000,
        "total_formatted": "£1,500.00"
      }
    },
    {...}
  ],
  "meta": {
    "current_page": 1,
    "next_page": 2,
    "prev_page": null,
    "total_pages": 5,
    "total_count": 115
  }
}
```

This endpoint retrieves all line items.

### HTTP Request

`GET https://app.nusii.com/api/v2/line_items`

## Get all line items from section

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/sections/100/line_items"
```

```shell--cli
nusii line-items list --section-id 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::LineItem.list(section_id: 100)
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "154",
      "type": "line_items",
      "attributes": {
        "section_id": 458,
        "name": "Redesign website",
        "position": 1,
        "cost_type": "fixed",
        "recurring_type": null,
        "per_type": null,
        "quantity": null,
        "updated_at": "2017-11-24T10:30:40.282Z",
        "created_at": "2017-11-24T10:30:40.282Z",
        "currency": "GBP",
        "amount_in_cents": 150000,
        "amount_formatted": "£1,500.00",
        "total_in_cents": 150000,
        "total_formatted": "£1,500.00"
      }
    },
    {...}
  ]
}
```

This endpoint retrieves all line items from a given section. This response doesn't support pagination.

### HTTP Request

`GET https://app.nusii.com/api/v2/sections/100/line_items`

## Create a line item

```shell--curl
curl -X POST \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"line_item": {"name": "Development Costs"}}' \
  "https://app.nusii.com/api/v2/sections/100/line_items"
```

```shell--cli
nusii line-items create --section-id 100 --name "Development Costs"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::LineItem.create(
  section_id: 100,
  name: 'Development Costs'
)
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "157",
    "type": "line_items",
    "attributes": {
      "section_id": 458,
      "name": "",
      "position": 2,
      "cost_type": "fixed",
      "recurring_type": null,
      "per_type": null,
      "quantity": null,
      "updated_at": "2017-11-27T10:45:09.919Z",
      "created_at": "2017-11-27T10:45:09.919Z",
      "currency": "GBP",
      "amount_in_cents": null,
      "amount_formatted": "£0.00",
      "total_in_cents": 0,
      "total_formatted": "£0.00"
    }
  }
}
```

This will return 201 Created and the current JSON representation of the line item if the creation was a success.

### HTTP Request

`POST https://app.nusii.com/api/v2/sections/100/line_items`

### Attributes

Parameter | Mandatory | Type | Description
--------- | --------- | -----| -----------
name | no | Text | Body of the line item
cost_type | no | String | Default `fixed`. Possible values are `fixed`, `recurring` or `per`
recurring_type | no | String | Possible values are `yearly`, `semiannually`, `trimester`, `monthly`, `weekly`, `daily` or `hourly`
per_type | no | String | Possible values are `year`, `month`, `week`, `day`, `hour`, `item` or `unit`
position | no | Integer | Position of the line item within the section
quantity | no | Integer | If `cost_type` is `per` then total of the line item is calculated by `quantity` multiplied by `amount`
amount | no | Integer | Amount in cents

## Update a line item

```shell--curl
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"line_item": {"amount": 10000}}' \
  "https://app.nusii.com/api/v2/line_items/:id"
```

```shell--cli
nusii line-items update 100 --amount 10000
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

line_item = Nusii::LineItem.get(100)

line_item.amount = 10000
line_item.save
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "157",
    "type": "line_items",
    "attributes": {
      "section_id": 458,
      "name": "",
      "position": 2,
      "cost_type": "fixed",
      "recurring_type": null,
      "per_type": null,
      "quantity": null,
      "updated_at": "2017-11-27T10:45:09.919Z",
      "created_at": "2017-11-27T10:45:09.919Z",
      "currency": "GBP",
      "amount_in_cents": 10000,
      "amount_formatted": "£100.00",
      "total_in_cents": 10000,
      "total_formatted": "£100.00"
    }

  }
}
```

This will return 200 OK and the current JSON representation of the line item if the creation was a success.

### HTTP Request

`PUT https://app.nusii.com/api/v2/line_items/:id`

or

`PUT https://app.nusii.com/api/v2/sections/458/line_items/:id`

### Attributes

Parameter | Mandatory | Type | Description
--------- | --------- | -----| -----------
name | no | Text | Body of the line item
cost_type | no | String | Default `fixed`. Possible values are `fixed`, `recurring` or `per`
recurring_type | no | String | Possible values are `yearly`, `semiannually`, `trimester`, `monthly`, `weekly`, `daily` or `hourly`
per_type | no | String | Possible values are `year`, `month`, `week`, `day`, `hour`, `item` or `unit`
position | no | Integer | Position of the line item within the section
quantity | no | Integer | If `cost_type` is `per` then total of the line item is calculated by `quantity` multiplied by `amount`
amount | no | Integer | Amount in cents

## Delete a line item

```shell--curl
curl -X DELETE \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/line_items/:id"
```

```shell--cli
nusii line-items delete 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

line_item = Nusii::LineItem.get(100)
line_item.destroy
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "157",
    "type": "line_items",
    "attributes": {
      "section_id": 458,
      "name": "",
      "position": 2,
      "cost_type": "fixed",
      "recurring_type": null,
      "per_type": null,
      "quantity": null,
      "updated_at": "2017-11-27T10:45:09.919Z",
      "created_at": "2017-11-27T10:45:09.919Z",
      "currency": "GBP",
      "amount_in_cents": 10000,
      "amount_formatted": "£100.00",
      "total_in_cents": 10000,
      "total_formatted": "£100.00"
    }

  }
}
```

This endpoint deletes a specific line item.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/line_items/:id`
