# Sections

## Get all sections

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/sections"
```

```shell--cli
nusii sections list --proposal-id 126
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Section.list(page: 1)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->sections()->list(proposalId: 126, page: 1);
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "164",
      "type": "sections",
      "attributes": {
        "currency": "GBP",
        "account_id": 3,
        "proposal_id": 124,
        "template_id": null,
        "title": "Introduction",
        "name": null,
        "body": "Lorem ipsum",
        "position": 0,
        "reusable": false,
        "section_type": "cost",
        "created_at": "2017-03-03T12:23:37.686Z",
        "updated_at": "2017-03-03T12:23:45.828Z",
        "page_break": false,
        "optional": false,
        "selected": false,
        "include_total": false,
        "total_in_cents": 50000,
        "total_formatted": "£500.00"
      },
      "relationships": {
        "line_items": {
          "data": [
            {
              "id": "76",
              "type": "line_items"
            }
          ]
        }
      }
    },
    {...}
  ],
  "meta": {
    "current_page": 1,
    "next_page": 2,
    "prev_page": null,
    "total_pages": 2,
    "total_count": 48
  }
}
```

This endpoint retrieves all sections.

### HTTP Request

`GET https://app.nusii.com/api/v2/sections`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
proposal_id | null | If set retrieves all sections of the proposal.
template_id | null | If set retrieves all sections of the template.
include_line_items | false | If set to true, the result will have all the data of the line items in the "included" parameter.

## Get a section

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/sections/:id"
```

```shell--cli
nusii sections get 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Section.get(100)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->sections()->get(100);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "164",
    "type": "sections",
    "attributes": {
      "currency": "GBP",
      "account_id": 3,
      "proposal_id": 126,
      "template_id": null,
      "title": "Introduction",
      "name": null,
      "body": "<p>Hello {{ clientFirstName }}</p>",
      "position": 0,
      "reusable": false,
      "section_type": "cost",
      "created_at": "2017-03-03T12:23:37.686Z",
      "updated_at": "2017-03-03T12:23:45.828Z",
      "page_break": false,
      "optional": false,
      "selected": false,
      "include_total": false,
      "total_in_cents": 50000,
      "total_formatted": "£500.00"
    },
    "relationships": {
      "line_items": {
        "data": [
          {
            "id": "76",
            "type": "line_items"
          }
        ]
      }
    }
  }
}

```

This endpoint retrieves a single section

### HTTP Request

`GET https://app.nusii.com/api/v2/sections/:id`

## Create a section

```shell--curl
curl -X POST \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"section": {"title": "Introduction"}}' \
  "https://app.nusii.com/api/v2/sections"
```

```shell--cli
nusii sections create --proposal-id 126 --title "Introduction"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Section.create(
  title: 'Introduction'
)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->sections()->create([
    'proposal_id' => 126,
    'title' => 'Introduction',
]);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "164",
    "type": "sections",
    "attributes": {
      "currency": "GBP",
      "account_id": 3,
      "proposal_id": 126,
      "template_id": null,
      "title": "Introduction",
      "name": null,
      "body": null,
      "position": 0,
      "reusable": false,
      "section_type": "cost",
      "created_at": "2017-03-03T12:23:37.686Z",
      "updated_at": "2017-03-03T12:23:45.828Z",
      "page_break": false,
      "optional": false,
      "selected": false,
      "include_total": false,
      "total_in_cents": 50000,
      "total_formatted": "£500.00"
    },
    "relationships": {
      "line_items": {
        "data": [
          {
            "id": "76",
            "type": "line_items"
          }
        ]
      }
    }
  }
}

```

This will return 201 Created and the current JSON representation of the section if the creation was a success.

### HTTP Request

`POST https://app.nusii.com/api/v2/sections`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
proposal_id | no | ID | ID of the proposal
template_id | no | ID | ID of the template
title | no | String | Title of the section
body | no | Text | Body of the section
name | no | String | Internal name of the section
position | no | Integer | Position in the proposal or template.
reusable | no | Boolean | Default `false`. Reusable sections can be reused to any template / proposal you want.
section_type | no | String | Default `text`. Can be `text` or `cost`. A text section is just a section with a body. A `cost` section can have line items and has a total.
page_break | no | Boolean | Default `false`. PDF page break
optional | no | Boolean | Default `false`. Client can choose the price package when `true`. Price is fixed when `false`
include_total | no | Boolean | Default `false`. Include a subtotal within the section. Not just the end of the proposal.

## Update a section

```shell--curl
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"section": {"title": "Introduction"}}' \
  "https://app.nusii.com/api/v2/sections/:id"
```

```shell--cli
nusii sections update 100 --title "Introduction"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

section = Nusii::Section.get(100)
section.title = 'Introduction'
section.save
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->sections()->update(100, [
    'title' => 'Introduction',
]);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "sections",
    "attributes": {
      "currency": "GBP",
      "account_id": 3,
      "proposal_id": 126,
      "template_id": null,
      "title": "Introduction",
      "name": null,
      "body": null,
      "position": 0,
      "reusable": false,
      "section_type": "cost",
      "created_at": "2017-03-03T12:23:37.686Z",
      "updated_at": "2017-03-03T12:23:45.828Z",
      "page_break": false,
      "optional": false,
      "selected": false,
      "include_total": false,
      "total_in_cents": 50000,
      "total_formatted": "£500.00"
    }
  }
}
```

This will return 200 OK and the current JSON representation of the section if the update was a success.

### HTTP Request

`PUT https://app.nusii.com/api/v2/sections/:id`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
proposal_id | no | ID | ID of the proposal
template_id | no | ID | ID of the template
title | no | String | Title of the section
body | no | Text | Body of the section
name | no | String | Internal name of the section
position | no | Integer | Position in the proposal or template.
reusable | no | Boolean | Default `false`. Reusable sections can be reused to any template / proposal you want.
section_type | no | String | Default `text`. Can be `text` or `cost`. A text section is just a section with a body. A `cost` section can have line items and has a total.
page_break | no | Boolean | Default `false`. PDF page break
optional | no | Boolean | Default `false`. Client can choose the price package when `true`. Price is fixed when `false`
include_total | no | Boolean | Default `false`. Include a subtotal within the section. Not just the end of the proposal.

## Delete a section

```shell--curl
curl -X DELETE \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/sections/:id"
```

```shell--cli
nusii sections delete 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

section = Nusii::Section.get(100)
section.destroy
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->sections()->delete(100);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "164",
    "type": "sections",
    "attributes": {
      "currency": "GBP",
      "account_id": 3,
      "proposal_id": 126,
      "template_id": null,
      "title": "Introduction",
      "name": null,
      "body": null,
      "position": 0,
      "reusable": false,
      "section_type": "cost",
      "created_at": "2017-03-03T12:23:37.686Z",
      "updated_at": "2017-03-03T12:23:45.828Z",
      "page_break": false,
      "optional": false,
      "selected": false,
      "include_total": false,
      "total_in_cents": 50000,
      "total_formatted": "£500.00"
    }
  }
}
```

This endpoint deletes a specific section.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/sections/:id`
