# Clients

## Get all Clients


```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/clients"
```

```shell--cli
nusii clients list
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Client.list(page: 1)
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "12",
      "type": "clients",
      "attributes": {
        "email": "support@nusii.com",
        "name": "Michael",
        "surname": "Koper",
        "full_name": "Michael Koper",
        "currency": "EUR",
        "business": "Michael Koper BV",
        "locale": "nl",
        "pdf_page_size": "A4",
        "web": "www.michaelkoper.com",
        "telephone": "1234567890",
        "address": "Madrid Street 34",
        "city": "Madrid",
        "postcode": "28018",
        "country": "Spain",
        "state": "Madrid"
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

This endpoint retrieves all clients.

### HTTP Request

`GET https://app.nusii.com/api/v2/clients`

## Get a Client

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/clients/:id"
```

```shell--cli
nusii clients get 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Client.get(100)
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "4",
    "type": "clients",
    "attributes": {
      "email": "support@nusii.com",
      "name": "Michael",
      "surname": "Koper",
      "full_name": "Michael Koper",
      "currency": "EUR",
      "business": "Michael Koper BV",
      "locale": "nl",
      "pdf_page_size": "A4",
      "web": "www.michaelkoper.com",
      "telephone": "1234567890",
      "address": "Madrid Street 34",
      "city": "Madrid",
      "postcode": "28018",
      "country": "Spain",
      "state": "Madrid"
    }
  }
}
```

This endpoint retrieves a single client

### HTTP Request

`GET https://app.nusii.com/api/v2/clients/:id`

## Create a client

```shell--curl
curl -X POST \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"client": {"email": "john@doe.com", "name": "John", "surname": "Doe", "locale": "en"}}' \
  "https://app.nusii.com/api/v2/clients"
```

```shell--cli
nusii clients create --email "john@doe.com" --name "John" --surname "Doe"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Client.create(
  email: 'john@doe.com',
  name: 'John',
  surname: 'Doe'
)
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "104",
    "type": "clients",
    "attributes": {
      "email": "john@doe.com",
      "name": "John",
      "surname": "Doe",
      "full_name": "John Doe",
      "currency": "EUR",
      "business": "Michael Koper BV",
      "locale": "en",
      "pdf_page_size": "A4",
      "web": "www.michaelkoper.com",
      "telephone": "1234567890",
      "address": "Madrid Street 34",
      "city": "Madrid",
      "postcode": "28018",
      "country": "Spain",
      "state": "Madrid"
    }
  }
}
```

This will return 201 Created and the current JSON representation of the client if the creation was a success.

### HTTP Request

`POST https://app.nusii.com/api/v2/clients`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
email | yes | String | Email of the client.
name | yes | String | First name of the client.
surname | no | String | Surname of the client.
currency | no | String | Currency of the client. Default: Account's default currency or USD.
business | no | String | Company name of the client
locale | no | String | Locale of the client. The language of the client's proposal.
pdf_page_size | no | String | The pdf page size of the client's proposal. Default: A4
web | no | String | Website of the client.
telephone | no | String | Telephone number of the client.
address | no | String | Address of the client.
city | no | String | City of the client.
postcode | no | String | Postcode of the client.
country | no | String | Country name of the client
state | no | String | State name of the client.

## Update a client

```shell--curl
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"client": {"email": "john@doe.com", "name": "John Doe"}}' \
  "https://app.nusii.com/api/v2/clients/:id"
```

```shell--cli
nusii clients update 100 --email "john@doe.com" --name "John Doe"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

client = Nusii::Client.get(100)

client.email = 'john@doe.com'
client.save
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "email": "support@nusii.com",
      "name": "Michael",
      "surname": "Koper",
      "full_name": "Michael Koper",
      "currency": "EUR",
      "business": "Michael Koper BV",
      "locale": "nl",
      "pdf_page_size": "A4",
      "web": "www.michaelkoper.com",
      "telephone": "1234567890",
      "address": "Madrid Street 34",
      "city": "Madrid",
      "postcode": "28018",
      "country": "Spain",
      "state": "Madrid"
    }
  }
}
```

This will return 200 OK and the current JSON representation of the client if the creation was a success.

### HTTP Request

`PUT https://app.nusii.com/api/v2/clients/:id`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
email | yes | String | Email of the client.
name | yes | String | First name of the client.
surname | no | String | Surname of the client.
currency | no | String | Currency of the client. Default: Account's default currency or USD.
business | no | String | Company name of the client
locale | no | String | Locale of the client. The language of the client's proposal.
pdf_page_size | no | String | The pdf page size of the client's proposal. Default: A4
web | no | String | Website of the client.
telephone | no | String | Telephone number of the client.
address | no | String | Address of the client.
city | no | String | City of the client.
postcode | no | String | Postcode of the client.
country | no | String | Country name of the client
state | no | String | State name of the client.

## Delete a client

```shell--curl
curl -X DELETE \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/clients/:id"
```

```shell--cli
nusii clients delete 100
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

client = Nusii::Client.get(100)
client.destroy
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "12",
    "type": "clients",
    "attributes": {
      "email": "support@nusii.com",
      "name": "Michael",
      "surname": "Koper",
      "full_name": "Michael Koper",
      "currency": "EUR",
      "business": "Michael Koper BV",
      "locale": "nl",
      "pdf_page_size": "A4",
      "web": "www.michaelkoper.com",
      "telephone": "1234567890",
      "address": "Madrid Street 34",
      "city": "Madrid",
      "postcode": "28018",
      "country": "Spain",
      "state": "Madrid"
    }
  }
}
```

This endpoint deletes a specific client.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/clients/:id`
