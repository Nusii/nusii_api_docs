# Proposals

## Get all Proposals

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals"

# Get only accepted proposals
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals?status=accepted"

# Get only draft proposals
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals?status=draft"
```

```shell--cli
nusii proposals list

# Get only accepted proposals
nusii proposals list --status accepted

# Get only draft proposals
nusii proposals list --status draft
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

# Get all proposals
Nusii::Proposal.list(page: 1)

# Get only accepted proposals
Nusii::Proposal.list(page: 1, status: 'accepted')

# Get only draft proposals
Nusii::Proposal.list(page: 1, status: 'draft', archived: false)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

// Get all proposals
$nusii->proposals()->list(page: 1);

// Get only accepted proposals
$nusii->proposals()->list(status: 'accepted', page: 1);

// Get only draft proposals
$nusii->proposals()->list(status: 'draft', archived: false, page: 1);
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "126",
      "type": "proposals",
      "attributes": {
        "title": "Webdesign yourwebsite.com",
        "account_id": 3,
        "status": "draft",
        "public_id": "-NqDAkiqpiFLuuw",
        "prepared_by_id": 3,
        "client_id": 5,
        "sender_id": null,
        "currency": "USD"
      },
      "relationships": {
        "sections": {
          "data": [
            {
              "id": "414",
              "type": "sections"
            }
          ]
        }
      }
    }
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

This endpoint retrieves all proposals.

### HTTP Request

`GET https://app.nusii.com/api/v2/proposals`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
status | null | If not set retrieves all proposals, Possible states are `draft`, `pending`, `accepted`, `rejected`, or `clarification`
archived | false | If set to true, the result will only include archived proposals.

## Get a proposal

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals/:id"
```

```shell--cli
nusii proposals get 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Proposal.get(100)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposals()->get(100);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account_id": 3,
      "status": "draft",
      "public_id": "-NqDAkiqpiFLuuw",
      "prepared_by_id": 3,
      "client_id": 5,
      "sender_id": null,
      "currency": "USD"
    },
    "relationships": {
      "sections": {
        "data": [
          {
            "id": "414",
            "type": "sections"
          }
        ]
      },
      "recipients": {
        "data": [
          {
            "id": "1",
            "type": "recipients"
          }
        ]
      }
    }
  },
  "included": [
    {
      "id": "1",
      "type": "recipients",
      "attributes": {
        "id": 1,
        "name": "Alice",
        "email": "alice@example.com",
        "eligible_to_sign": true,
        "document_sent": false
      }
    }
  ]
}
```

This endpoint retrieves a single proposal

### HTTP Request

`GET https://app.nusii.com/api/v2/proposals/:id`


## Create a proposal

```shell--curl
curl -X POST \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"proposal": {"client_id": 100, "title": "Webdesign yourwebsite.com"}}' \
  "https://app.nusii.com/api/v2/proposals"
```

```shell--cli
nusii proposals create --client-id 100 --title "Webdesign yourwebsite.com"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Proposal.create(
  title: 'Webdesign yourwebsite.com',
  client_id: 100
)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposals()->create([
    'title' => 'Webdesign yourwebsite.com',
    'client_id' => 100,
]);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account_id": 3,
      "status": "draft",
      "public_id": "-NqDAkiqpiFLuuw",
      "prepared_by_id": 3,
      "client_id": 5,
      "sender_id": null,
      "currency": "USD"
    },
    "relationships": {
      "sections": {
        "data": [
          {
            "id": "414",
            "type": "sections"
          }
        ]
      }
    }
  }
}
```

This will return 201 Created and the current JSON representation of the proposal if the creation was a success.

### HTTP Request

`POST https://app.nusii.com/api/v2/proposals`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
title | no | String | Title of the proposal
client_id | no | ID | Client ID
client_email | no | String | Fetches the client associated with that email. It creates a new client if there is no client with that email. This is ignored when client_id is set.
template_id | no | ID | If set, all the sections are copied over from the template
document_section_title | no | String | Title of the documents section. Default: Documents
prepared_by_id | no | ID | Prepared by user
expires_at | no | DateTime | Date the proposal expires
display_date | no | DateTime | By Default the date displayed on the proposal is the sent date. This can be overwritten with the display_date
report | no | Boolean | This turns the proposal into a report. Default: false
exclude_total | no | Boolean | This excludes the total from the proposal. Default: false
exclude_total_in_pdf | no | Boolean | This excludes the total from the proposal. Default: false
theme | no | String | Theme of the proposal. Default: 'clean'

## Update a proposal

```shell--curl
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"title": "Webdesign yourwebsite.com"}' \
  "https://app.nusii.com/api/v2/proposals/:id"
```

```shell--cli
nusii proposals update 100 --title "Webdesign yourwebsite.com"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

proposal = Nusii::Proposal.get(100)
proposal.title = 'Webdesign yourwebsite.com'
proposal.save
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposals()->update(100, [
    'title' => 'Webdesign yourwebsite.com',
]);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account_id": 3,
      "status": "draft",
      "public_id": "-NqDAkiqpiFLuuw",
      "prepared_by_id": 3,
      "client_id": 5,
      "sender_id": null,
      "currency": "USD"
    },
    "relationships": {
      "sections": {
        "data": [
          {
            "id": "414",
            "type": "sections"
          }
        ]
      }
    }
  }
}
```

This will return 200 OK and the current JSON representation of the proposal if the update was a success.

### HTTP Request

`PUT https://app.nusii.com/api/v2/proposals/:id`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
title | no | String | Title of the proposal
client_id | no | ID | Client ID
client_email | no | String | Fetches the client associated with that email. It creates a new client if there is no client with that email. This is ignored when client_id is set.
document_section_title | no | String | Title of the documents section. Default: Documents
prepared_by_id | no | ID | Prepared by user
expires_at | no | DateTime | Date the proposal expires
display_date | no | DateTime | By Default the date displayed on the proposal is the sent date. This can be overwritten with the display_date
report | no | Boolean | This turns the proposal into a report. Default: false
exclude_total | no | Boolean | This excludes the total from the proposal. Default: false
exclude_total_in_pdf | no | Boolean | This excludes the total from the proposal. Default: false
theme | no | String | Theme of the proposal. Default: 'clean'

## Delete a proposal

```shell--curl
curl -X DELETE \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals/:id"
```

```shell--cli
nusii proposals delete 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

proposal = Nusii::Proposal.get(100)
proposal.destroy
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposals()->delete(100);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account_id": 3,
      "status": "draft",
      "public_id": "-NqDAkiqpiFLuuw",
      "prepared_by_id": 3,
      "client_id": 5,
      "sender_id": null,
      "currency": "USD"
    }
  }
}
```

This endpoint deletes a specific proposal.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/proposals/:id`

## Archive a proposal

```shell--curl
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals/:id/archive"
```

```shell--cli
nusii proposals archive 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

# TODO not implemented yet
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposals()->archive(100);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account_id": 3,
      "status": "draft",
      "public_id": "-NqDAkiqpiFLuuw",
      "prepared_by_id": 3,
      "client_id": 5,
      "sender_id": null,
      "currency": "USD",
      "archived_at": "2019-01-01T10:00:00.000Z"
    }
  }
}
```

This endpoint deletes a specific proposal.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/proposals/:id`

## Send a proposal

> Send to a single email (legacy):

```shell--curl
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"email": "your_client@email.com", "subject": "Your Proposal"}' \
  "https://app.nusii.com/api/v2/proposals/:id/send_proposal"
```

```shell--cli
nusii proposals send 100 --email "your_client@email.com" --subject "Your Proposal"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

# TODO not implemented yet
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposals()->send(100,
    email: 'your_client@email.com',
    subject: 'Your Proposal'
);
```

> Send to multiple recipients:

```shell--curl
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{
    "subject": "Your Proposal",
    "message": "Please review the attached proposal.",
    "sender_email": "sender@example.com",
    "recipients": [
      { "name": "Alice", "email": "alice@example.com", "eligible_to_sign": true },
      { "name": "Bob", "email": "bob@example.com", "eligible_to_sign": false }
    ]
  }' \
  "https://app.nusii.com/api/v2/proposals/:id/send_proposal"
```

```shell--cli
nusii proposals send 100 \
  --subject "Your Proposal" \
  --message "Please review the attached proposal." \
  --sender-email "sender@example.com" \
  --recipients '[{"name": "Alice", "email": "alice@example.com", "eligible_to_sign": true}, {"name": "Bob", "email": "bob@example.com", "eligible_to_sign": false}]'
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

# TODO not implemented yet
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

// Send to multiple recipients is not yet
// supported in the PHP library.
// Use the single email method above instead.
```

> The above command returns JSON structured like this:

```json
{
  "status": "sent",
  "sent_at": "2026-03-02T17:27:54.000Z",
  "sender_id": 42,
  "sender_name": "Michael Koper"
}
```

This will return 200 OK and the current JSON representation.

If you have reached the active proposal limit for your plan, the API will return a `402 Payment Required` error:

```json
{
  "error": "You have reached your active proposal limit. Please upgrade your plan to continue sending proposals."
}
```


You can send a proposal to a single email using the `email` parameter, or to multiple recipients using the `recipients` array. When `recipients` is provided, `email` is ignored. A maximum of 10 recipients can be specified per request.

If neither `sender_id` nor `sender_email` is provided, the sender defaults to the account owner.

### HTTP Request

`PUT https://app.nusii.com/api/v2/proposals/:id/send_proposal`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
email | no | String | Email of the client. Required when `recipients` is not provided.
recipients | no | Array | Array of recipient objects (see below). When provided, `email` is ignored. Maximum 10 recipients.
cc | no | String | CC Email recipients. Need to be comma separated if contains multiple emails.
bcc | no | String | BCC Email recipients. Need to be comma separated if contains multiple emails.
subject | no | String | Subject of the email
message | no | String | Body of the email
save_email_template | no | Boolean | Overwrite email template. Default: false
sender_id | no | ID | ID of the sender
sender_email | no | String | Fetches the Sender associated with that email. This is ignored when sender_id is set.

### Recipient Object

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
name | yes | String | Recipient's display name
email | yes | String | Recipient's email address
eligible_to_sign | no | Boolean | Whether this recipient can sign the proposal. Default: false
