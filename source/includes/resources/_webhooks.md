# Webhooks

With Nusii webhooks we can send your application requests when something interesting happens, like `Proposal Accepted`, `Proposal Viewed` etc.

## Webhook endpoint format

Every webhook uses the same structure. It will always be in a standard `POST` request with the object in the body.

The target url needs to be able to accept `Content Type`: `application/json` and `POST` requests. Everything other than a 2xx request will be concidered an error and we will try will retry 25 times. If we receive a `410 GONE` response, we will delete the webhook entirely.

Parameter | Description
--------- | -------
event_name | The name of the event. `proposal_created`, `client_updated` etc.
The object | An hash that represents the object. The key is always the name of the object. "proposal", "client" etc

```json
  {
    "event_name": "proposal_created",
    "proposal": {
      "id": 30,
      "title": "Webdevelopment",
      ...
    }
  }
```

## Webhook endpoint errors

We concider all responses with `2xx` as successful. Other than that we concider it as an error and we will retry the request 24 times. If we receive a `410 GONE`, the enpoint will get removed from our database.

## Available webhooks

Event | Description
--------- | -------
proposal_created | Sends when a proposal is created
proposal_updated | Sends when a proposal is updated
proposal_destroyed | Sends when a proposal is deleted
proposal_accepted | Sends when a proposal is accepted
proposal_rejected | Sends when a proposal is rejected
proposal_sent | Sends when a proposal is sent
proposal_activity_client_viewed_proposal | Sends when your client views a proposal
client_created | Sends when client is created
client_updated | Sends when client is updated
client_destroyed | Sends when client is deleted


## Get all webhook endpoints

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/webhook_endpoints"
```

```shell--cli
nusii webhooks list
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::WebhookEndpoint.list(page: 1)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->webhookEndpoints()->list();
```

> The above command returns JSON structured like this:


```json
{
  "data": [
    {
      "id": "26",
      "type": "webhook_endpoints",
      "attributes": {
        "events": [
          "proposal_created",
          "client_updated"
        ], "target_url": "http://example.com/webhooks"
      },
    },
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

This endpoint retrieves all webhooks endpoints.

### HTTP Request

`GET https://app.nusii.com/api/v2/webhook_endpoints`

## Get a webhook endpoint

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/webhook_endpoints/:id"
```

```shell--cli
nusii webhooks get 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::WebhookEndpoint.get(100)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->webhookEndpoints()->get(100);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "33",
    "type": "webhook_endpoints",
    "attributes": {
      "events": [
        "proposal_created",
        "client_created"
      ],
      "target_url": "http://example.com/webhooks"
    }
  }
}
```

This endpoint retrieves a single webhook endpoint

### HTTP Request

`GET https://app.nusii.com/api/v2/webhook_endpoints/:id`


## Create a webhook endpoint

```shell--curl
curl -X POST \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"webhook_endpoint":{"target_url": "http://example.com","events": ["proposal_created", "client_created"]}}' \
  "https://app.nusii.com/api/v2/webhook_endpoints"
```

```shell--cli
nusii webhooks create --target-url "http://example.com" --events "proposal_created,client_created"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::WebhookEndpoint.create(
  target_url: http://example.com,
  events: ['proposal_created', 'client_created']
)
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->webhookEndpoints()->create([
    'target_url' => 'http://example.com',
    'events' => ['proposal_created', 'client_created'],
]);
```

> The above command returns JSON structured like this:


```json
{
  "data": {
    "id": "34",
    "type": "webhook_endpoints",
    "attributes": {
      "events": [
        "proposal_created",
        "client_created"
      ],
      "target_url": "http://example.com"
    }
  }
}
```

This will return 201 Created and the current JSON representation of the webhook endpoint if the creation was a success.

### HTTP Request

`POST https://app.nusii.com/api/v2/webhook_endpoints`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
target_url | yes | String | Destination url of the webhook request.
events | yes | String[] | An Array of string that represents the events you want to subscribe to.


## Delete a webhook endpoint

```shell--curl
curl -X DELETE \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/webhook_endpoints/:id"
```

```shell--cli
nusii webhooks delete 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

endpoint = Nusii::WebhookEndpoint.get(100)
endpoint.destroy
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->webhookEndpoints()->delete(100);
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "34",
    "type": "webhook_endpoints",
    "attributes": {
      "events": [
        "proposal_created",
        "client_created"
      ],
      "target_url": "http://example.com"
    }
  }
}
```

This endpoint deletes a specific webhook_endpoint.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/webhook_endpoints/:id`
