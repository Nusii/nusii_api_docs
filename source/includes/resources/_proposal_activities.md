# Proposal Activities

## Get all proposal activities

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposal_activities"
```

```shell--cli
nusii activities list --proposal-id 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

activities = Nusii::ProposalActivity.list(
  page: 1,
  proposal_id: 100
)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposalActivities()->list(
    proposalId: 100,
    page: 1
);
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "259",
      "type": "proposal_activities",
      "attributes": {
        "activity_type": "user_send_proposal",
          "ip_address": "127.0.0.1",
          "additional_fields": {
          "to": "john@doe.com",
          "cc": "joh+cc@doe.com",
          "from": "your@email.com",
          "reply_to": "your@email.com",
          "subject": "You've received your proposal!"
        },
        "proposal_title": "Webdevelopment",
        "proposal_created_at": "2017-11-24T10:30:40.113Z",
        "proposal_sent_at": null,
        "proposal_status": "draft",
        "proposal_public_id": "FYp1S4oBLxbNpQ",
        "proposal_expires_at": null,
        "client_name": "John",
        "client_email": "john@doe.com",
        "client_surname": "Doe",
        "client_full_name": "John Doe",
        "client_business": "Company Name",
        "client_telephone": "1234567890",
        "client_locale": "en",
        "client_address": "Street Address",
        "client_postcode": "28017",
        "client_country": "Spain",
        "client_city": "Madrid",
        "client_state": "Madrid",
        "client_web": "example.com"
      }
    },
    {...}
  ],
  "meta": {
    "current_page": 1,
    "next_page": 2,
    "prev_page": null,
    "total_pages": 9,
    "total_count": 206
  }
}
```

This endpoint retrieves all proposal activities.

### HTTP Request

`GET https://app.nusii.com/api/v2/proposal_activities`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
proposal_id | null | Only get activities from a specific proposal
client_id | null | Only get activities from a specific client

## Get a Proposal Activity

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposal_activities/44"
```

```shell--cli
nusii activities list --proposal-id 44
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

activity = Nusii::ProposalActivity.get(44)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->proposalActivities()->get(44);
```

> The above command returns JSON structured like this:


```json
{
  "data": {
    "id": "44",
    "type": "proposal_activities",
    "attributes": {
      "activity_type": "user_send_proposal",
      "ip_address": "127.0.0.1",
      "additional_fields": {
        "to": "john@doe.com",
        "cc": "joh+cc@doe.com",
        "from": "your@email.com",
        "reply_to": "your@email.com",
        "subject": "You've received your proposal!",
        "bounce_type": "HardBounce",
        "bounced_email": "john@doe.com",
        "bounce_description": "The server was unable to deliver your message (ex: unknown user, mailbox not found)."
      },
      "proposal_title": "Design for clientwebsite.com",
      "proposal_created_at": "2016-11-28T15:00:58.794Z",
      "proposal_sent_at": "2017-01-12T12:46:33.396Z",
      "proposal_status": "draft",
      "proposal_public_id": "smaBXa7wa1Jv",
      "proposal_expires_at": null,
      "client_name": "John",
      "client_email": "john@doe.com",
      "client_surname": "Doe",
      "client_full_name": "John Doe",
      "client_business": "John Doe's Business",
      "client_telephone": "1234567890",
      "client_locale": "en",
      "client_address": "Street Address 29",
      "client_postcode": "28017",
      "client_country": "Spain",
      "client_city": "Madrid",
      "client_state": "Madrid",
      "client_web": "www.clientwebsite.com"
    }
  }
}
```

This endpoint retrieves a single proposal activity

### HTTP Request

`GET https://app.nusii.com/api/v2/proposal_activities/:id`

Parameter | Type | Description
--------- | ---- | -----------
activty_type | String | Type of activity. Possible values are: `client_view_proposal`, `client_view_pdf`, `user_create_proposal`, `user_view_proposal`, `user_send_proposal`, `user_manual_change_status_proposal`, `client_rejected_proposal`, `client_clarification_proposal`, `client_accepted_proposal`, `client_email_bounced`, `client_email_opened`, and `api_created_proposal`
ip_address | String | Ip address of the person that does the activity
additional_fields | Hash | An hash with additional information. Possible values are: `to` (email address where the proposal is sent), `cc` (cc email address where proposal is sent), `from` (email address where proposal is sent from), `reply_to` (reply to email address), `subject` (subject of email), `message` (the body of the email sent, or the reason of a proposal state change), `bounce_type` (set if email bounced), `bounce_description` (description why email bounced)
proposal_attributes | ... | Look at Proposal for information
client_attributes | ... | Look at Client for information
